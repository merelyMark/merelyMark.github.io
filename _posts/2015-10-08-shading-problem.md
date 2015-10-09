---
layout: post
title: "Shading problem is a shading problem"
author: mark_kim
modified: 2015-10-08 13:00
date:   2015-10-08 12:00
tags: [todo]
---

So, I'm trying to figure out why I'm getting noisy black spots. I created a picker to sample the normals and returned values from hits in the octree. The image above highlights where I sampled a few adjacent pixels.

![edelta 2048 noise](/images/2015-10-08/edelta-2048-noisy-highlight.png)

The first number is the morton number from the screen space: this always returns zero from the picker because it's broken. The next tuple is the image space number while the next two triplets are the decoded morton code (wrong because the original morton code is wrong) and the hit_pt returned by the eye.

The next line has the normal.

The line after that has the morton number decoded, the value returned for that voxel, and the computed cosTheta for the voxel.

As you can see we get some very different normals for some pretty close voxels. I don't know. I do know that I could average them to get rid of the noise, but is that really correct?

```
0 (477, 507) (0, 0, 0)(2.73961, 2.81897,0.128205)
n: (-0.629017 -0.0316313 -0.776748)
morton: (1059 1150 887) val 0.496961 cosTheta 0.776748
0 (481, 576) (0, 0, 0)(2.83659, 10.3001,0.128205)
n: (-0.912533 -0.395399 0.104607)
morton: (1061 1124 894) val 0.501067 cosTheta 0.104607
0 (481, 572) (0, 0, 0)(2.83659, 8.92674,0.128205)
n: (-0.750453 -0.133241 0.647354)
morton: (1061 1125 895) val 0.436701 cosTheta 0.647354
0 (481, 577) (0, 0, 0)(2.83659, 10.7121,0.128205)
n: (-0.912533 -0.395399 0.104607)
morton: (1061 1124 894) val 0.501067 cosTheta 0.104607
0 (482, 578) (0, 0, 0)(2.86192, 11.1584,0.128205)
n: (0.967088 0.203721 -0.15244)
morton: (1061 1123 895) val 0.539679 cosTheta 0.15244
```
So, perhaps it's not that it's a flickering normal.  I picked a different area and printed out the neighboring normals as well:

![edelta 2048 noise](/images/2015-10-08/edelta-2048-noisy-other-highlight.png)

The layout it the octree index, the morton index, the screen space (x,y), the morton decoded, the parametric space location (x,y,z), the vals of the the voxel plus its neighbors, the morton decode of the neighbors, the normals of the neighbors and cosTheta.  Picking near the first image:

```
476910 6594466764 (494, 572) (1061, 1124, 894)(0.0906443, 0.0863919,0.093828)
0.117901 0.131676 0.796835 0.274207 0.962673 0.965998 0.221097 0.249578 
(1061,1124,894) (1062,1124,894) (1061,1125,894) (1062,1125,894) (1061,1124,895) (1062,1124,895) (1061,1125,895) (1062,1125,895) 
(-0.912533,-0.395399,0.104607) (0.967088,0.203721,-0.15244) (-0.912533,-0.395399,0.104607) (0.967088,0.203721,-0.15244) (-0.912533,-0.395399,0.104607) (-0.787511,0.0143994,0.616132) (-0.750453,-0.133241,0.647354) (-0.750453,-0.133241,0.647354) 
0.104607
```
There are fluctuations on the normal between the neighbors.

But, picking the new region,

```
981082 6599885068 (543, 484) (1077, 1152, 898)(0.0928557, 0.0898999,0.09368)
0.653093 0.775538 0.0758937 0.631325 0.842607 0.846115 0.378607 0.428631 
(1077,1152,898) (1078,1152,898) (1077,1153,898) (1078,1153,898) (1077,1152,899) (1078,1152,899) (1077,1153,899) (1078,1153,899) 
(0.0851233,-0.996258,-0.01494) (0.0940881,-0.974352,0.204416) (0.0851233,-0.996258,-0.01494) (0.0940881,-0.974352,0.204416) (0.0851233,-0.996258,-0.01494) (0.0940881,-0.974352,0.204416) (0.0851233,-0.996258,-0.01494) (0.0940881,-0.974352,0.204416) 
0.01494
```

there is no fluctuating normal. The normal just points orthogonal to the ray.