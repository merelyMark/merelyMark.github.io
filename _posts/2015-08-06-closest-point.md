---
layout: post
title: "Closest point in CUDA"
author: mark_kim
modified:
date:   2015-08-06 19:30
tags: []
---

Closest point embedding now works in CUDA while allowing for larger than 
1024^3. I just gutted a whole bunch of it because I was making it too complicated.

I realized over the summer that the fast out-of-core voxelization method
I wanted to use wasn't going to work because it relied on building 
the voxelization by going through each triangle and computing every 
voxel that intersects it. 

So, it's possible to construct the closest point from only the voxels that
are generated, but extending it off the surface is difficult because 
of how I was trying to construct everything. For every triangle, compute
the voxels that intersect with it, and mark that in an 3D array. With the 3D
array, create a compact index of the voxels. With the compact index, then 
build the closest point embedding. Expanding this by trying to bolt on extending the surface was difficult. Further, there were other issues with correctness, 
i.e. what happens if a different region has a surface that is closer to a 
cell that is 3 cells away from a triangle?

So, I gutted it because it was proving unwieldy. So, I went simple and 
marked every voxel that intersects a triangle as well as +-3 cells in 3D. 
Once I had this marked 3D array, create a compact list of indexes and
for any voxel that is marked, iterate through every triangle in the mesh
and compute the closest point. This proved painfully slow, with an Intel Core 
i7-4720HQ and an Nvidia GTX-860M it took 3.7s. I thought I could speed it up
with shared memory, but this proved futile.

When we build the region, we also build an array of indices for the triangles
in the region. If we only run this (which could lead to an incorrect result), 
it takes 0.45s. 

However, we can quickly rebuild the triangles within the region, but change
the boundary by +-3. This way, all the triangles that could possibly interact
with a cell would be included. With this adjustment, it takes 0.6s. That's a result
I can live with.



