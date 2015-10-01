---
layout: post
title: "speedup UFLIC CUDA 8192"
author: mark_kim
modified:
date:   2015-10-01 16:00
tags: []
---
Generating data today. I'm using the edelta from Cristoph, and the ICE train and f6 as verification. Measuring time to construct the octree and applying UFLIC for 256^3, 512^3, 1024^3, 2048^3 and 4096^3. For edelta alone, I'm running 8192^3.

I'm also running it all in one process to test for leaks as well. I spent a good chunk of time debugging the command line. Now, just run and wait. I think I may have broken cleopatra, but we'll see. I brought down my own machine badly enough that it didn't respond for 30 minutes. I could ping it, but it only stopped after crashing out.

Finally, I'm trying to figure out a *fast* way to do on the fly LOD. So far, it's proving elusive (the fast part, anyways).