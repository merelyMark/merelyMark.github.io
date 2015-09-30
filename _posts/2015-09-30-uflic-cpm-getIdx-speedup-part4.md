---
layout: post
title: "speedup UFLIC CUDA 8192"
author: mark_kim
modified:
date:   2015-09-30 17:00
tags: []
---
edelta with 8192^3 grid size. On the desktop with no projection Bresenham, 2745s (Xeon 5140 with K6000). With CUDA, 391s. Also, because of memory constraints, this is without a neighborhood lookup. 

This is a far cry from when I started being able to run the 8192 on the CPU. It took over 3 hours.

![edelta, 8192 no projection, CUDA](/images/2015-09-30/edelta-8192-no-proj-bresenham-cuda.png)

