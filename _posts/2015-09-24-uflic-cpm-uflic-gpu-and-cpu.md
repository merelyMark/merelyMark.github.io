---
layout: post
title: "UFLIC: CPU vs GPU"
author: mark_kim
modified:
date:   2015-09-23 20:00
tags: []
---
So the CPU and GPU version doesn't match. Why? Well, they sum of the hitdata is off by a third, so atomics were added to bresenham, which brought the sum to parity.  But a 10% hit in performance.

So, now the intial image isn't noisy, but the next step is.

And the reason why the next step is noisy is because I accidentally changed an index from looking up to/from to nodes.

Also, I wasn't actually doing the new bresenham, I forgot to virtualize that function. The speed-ups listed earlier were simply because of updates with neighborhood lookups.  Pretty good speed-up.

The ngh_idx bresenham is a mess and doesn't work.

 