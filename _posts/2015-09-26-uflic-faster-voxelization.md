---
layout: post
title: "UFLIC: Faster voxelization"
author: mark_kim
modified:
date:   2015-09-26 16:00
tags: []
---

Previously, I changed the CudaMemThrust so they only do cudaMalloc for the device and got a good speedup. But, I want to completely overlap the voxelization with octree building on the CPU. So nothing can call synchronize, which means no cudaMalloc calls.

So, I unburied my CudaMemThrustPool. I forgot though that it can only work for similar sized types, so no float3 and uint64 with uint. Bummer.

But really, I just wanted to speed-up cudaRun. So, I put it in there. There were some weird things. For instance, the CMTPMaster would have type unsigned char, but CMTPool would have type unsigned int. I couldn't instantiate more than 2GB of memory for the pool, otherwise casting a pool memory location would cause it to return 0. Changing the CMTPMaster to unsigned int though (but keeping the memory pool the same size as unsigned char) allowed for 2GB or larger. How much larger I don't know though. These are the issues with scaling.

But now on the K6000 and Xeon 5140 the voxelization for the edelta takes 2.5s. I don't think I have previous timing results, but that just seems fast.

But it's slower (???) than before using the ICE train at 512^3? It's 0.615 vs 0.28. That doesn't make sense though. If I were to take a guess, I used 2^8 which is what I normally test on, but that translated in my head to 512^3.

And wouldn't you know, it's 0.27. For a whole days worth of work to get CudaMemThrustPool in. *sigh* But, one more step to no sychronization calls.  