---
layout: post
title: "Faster Raycaster"
author: mark_kim
modified:
date:   2015-09-22 18:00
tags: []
---

Raycaster is faster, but the voxelizer is slower and uses sizeof(char) * # of voxels more memory. I'm okay with this. It's a good trade off for a ~5x speedup.

Previously, I would not keep track of the "surface." Now, I do keep track of voxels that intersect the surface, but only that it is the surface with a single char. 

With this information, when the raycaster casts through the volume I can query whether or not it's it's actually on the surface. This is in contrast to what I did before which was try to determine if the voxel was "close" to the surface, by some epsilon. 


 
 
