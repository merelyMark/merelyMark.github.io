---
layout: post
title: "Bresenham and Laplacian without ngh_idx in CUDA: more timing"
author: mark_kim
modified:
date:   2015-09-23 20:00
tags: []
---
Neighborhood lookup is back in CUDA. Unfortunately, it's still slow.
F6 @ 512^3

860M: 7.9s to run with DEBUG_SWITCH ON
4720HQ: 2.2s to run with DEBUG_SWITCH OFF

That's a tragedy. The Bresenham still has to do a tree lookup to find anything that's not directly a neighbor. So, not much savings with a neighborhood lookup.

Perhaps a small cube (64^3 for a 512^3) with indices into the ndata. 

So, if it's n^3 and we choose it to be (n-3)^3, then a 8192^3 is 2^13 and it's 'smaller' cube would be 2^10. 1 GB? That's pretty good, let's try that. 