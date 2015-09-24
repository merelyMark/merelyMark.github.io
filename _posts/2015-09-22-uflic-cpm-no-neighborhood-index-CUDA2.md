---
layout: post
title: "Bresenham and Laplacian without ngh_idx in CUDA: more timing"
author: mark_kim
modified:
date:   2015-09-22 19:30
tags: []
---
Xeon 5140 with an Nvidia K6000
2048^3 with F6 dataset.

Number of threads to run UFLIC (12955018 voxels):
2^22: 78s (3 iterations)
2^23: 50s (2 iterations)
2^24: 40s (1 iteration)


4096^3 with F6 dataset.
Number of threads to run UFLIC ():
2^24 Sometimes timed out.

