---
layout: post
title: "Bresenham and Laplacian without ngh_idx in CUDA: more timing"
author: mark_kim
modified:
date:   2015-09-23 20:00
tags: []
---
For Bresenham, I realized that every step in the function bresenham I take only one cell away, at most. This is by design so there are no gaps in the 3D line that's being drawn.

I can take advantage of this to save time. I can lookup neighbors of neighbors (of neighbors). Although this requires some control flow, I dont think it's more than looping through the octree.

Xeon 5140 with F6 @ 1024^3.

No ngh_idx: 40s
With indirect ngh_idx: 20s.

Not bad.

Is it better on the GPU? I hope so.
K6000
with indirect ngh_idx: 6.7s

But the laplacian is still doing a deep search. 
K6000
with indirect ngh_idx for bresenham and laplacian: 6.0s

 Edit: Also, I wasn't actually doing the new bresenham, I forgot to virtualize that function. The speed-ups listed earlier were simply because of updates with neighborhood lookups.  Pretty good speed-up.
