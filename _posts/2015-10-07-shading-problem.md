---
layout: post
title: "Shading problem is not a shading problem"
author: mark_kim
modified:
date:   2015-10-07 9:20
tags: [todo]
---
The shading problem is not a shading problem, it's a raycast problem. The raycaster I'm using can quickly find the surfaces that intersect the volume. However, it has no idea *how* the surface intersects the plane or what orientation the surface has.

So, what can we do? Stronger check by doing a binary search for the closest point surface?

