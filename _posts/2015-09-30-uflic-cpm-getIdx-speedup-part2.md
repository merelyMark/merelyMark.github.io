---
layout: post
title: "speedup UFLIC"
author: mark_kim
modified:
date:   2015-09-30 12:00
tags: []
---
Previous, I would project a particle back to the surface to continue advecting through the surface. However, I think this is redundant. Since we're already advecting a particle starting with every cell, including the cells that are "off" the surface, since the values off the surface are really "on" the surface, these are all legitimate advections. Further, as these values cross over the surface and "deposit" onto the surface, we're building the surface UFLIC as well.

In other words, once a particle leaves the thin shell, there's no point in bringing it back to the surface. So, we stop. 

Previously, projecting particles to the surface using the laptop CPU (i7-4720HQ) with the edelta dataset at 4096^3, running the prep stage "val" took <del>208.537s</del> 186.232s. It looks like:

![edelta, 4096, projection bresenham](/images/2015-09-30/edelta-4096-proj-bresenham.png)


Without projecting the particles to the surface it takes 108.848s and looks like:

![edelta, 4096, no projection bresenham](/images/2015-09-30/edelta-4096-no-proj-bresenham.png)