---
layout: post
title: "Bresenham and Laplacian without ngh_idx in CUDA: more timing"
author: mark_kim
modified:
date:   2015-09-22 15:30
tags: []
---
I can no load/save closest point (morton, surface, triangle idx, and node data) to file and load it again.

Without a neighborhood lookup, 8192 is stupid slow. I will look to make it better.

