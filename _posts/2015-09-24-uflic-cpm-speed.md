---
layout: post
title: "UFLIC: speed"
author: mark_kim
modified:
date:   2015-09-23 20:00
tags: []
---
So, the ICE train right now runs 0.88 for voxelization at 512^3. Nothing seems to make it faster. But, the load is very low, ~2000 triangles it seems per run. What if we run multiple kernels at the same time.

So, if we just shift stuff (not even completely, some copies still happen on the default stream) to another stream? ~0.78s

What if we actually run (not completely either) two stream? 0.62s

Looking at the profiler, cudaAllocHost is slow: one can take up to 12ms. So, what if we change CudaMemThrust to only instantiate device only for the temporary arrays we create in cuda.cu:cudaRun? 0.28s.



 