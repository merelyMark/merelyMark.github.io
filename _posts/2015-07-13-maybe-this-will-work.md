---
layout: post
title: "Improving performance ideas"
author: mark_kim
modified:
#excerpt: "A post to test author overrides using a data file."
date:   2015-07-13 17:00
tags: []
---

How can we speed things up? Well, let's assume that my assumption is correct,
 that each warp is running serially in CUDA and that's what causes the slow
 performance. To increase performance, what if we run each each thread
 over each bit plane, but they all do the same thing. I realize that's a waste
 of compute power, but right now the threads are diverging and running 
 in serial anyway. Doing this at least parallelizes the computation at the 
 expense of redundant computation.

