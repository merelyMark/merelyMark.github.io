---
layout: post
title: "Bresenham and Laplacian without ngh_idx in CUDA"
author: mark_kim
modified:
date:   2015-09-22 15:30
tags: []
---

Got UFLIC/Bresenham and Laplacian running on the GPU. It might have been a mismatched extern cudaLaplacian, but it also could have been the solution I used. Which was to refactor the classes Laplacian and Bresenham.

Problem though: it's painfully slow. For the F6 at 512^3, 
on the GPU (860M) it's 11s to run an iteration of UFLIC. Multicore 
on the CPU it takes 4.4s. 

That's not good. 

On the desktop with a K6000 and Xeon 5140, for the F6 at 1024^3, on the GPU it takes about 109s to do UFLIC. Multicore on the Xeon it takes 41s. Multicore on the laptop with an i7-4720HQ it takes 19.544s.

The tree lookup required for each neighbor lookup is killing the GPU.  
 
 
 
