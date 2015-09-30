---
layout: post
title: "speedup UFLIC CUDA"
author: mark_kim
modified:
date:   2015-09-30 12:00
tags: []
---
On the desktop with projection Bresenham, 87.04s (Xeon 5140 with K6000). With CUDA, 8s.

![edelta, 4096 projection, CUDA](/images/2015-09-30/edelta-4096-projection-bresenham-cuda.png)

![edelta, 4096 no projection, CUDA](/images/2015-09-30/edelta-4096-no-proj-bresenham-cuda.png)