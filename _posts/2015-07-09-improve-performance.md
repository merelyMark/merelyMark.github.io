---
layout: post
title: "Improving performance ideas"
author: mark_kim
modified:
#excerpt: "A post to test author overrides using a data file."
date:   2015-07-09 15:00
tags: []
---

Using OMP to parallelize on the GPU:

{% highlight python %}
(3.35976 + 3.56259 + 3.58258) / 3 = 3.5016
{% endhighlight %}

This is eight threads on an i7-4720HQ (4 cores with hyperthreading), and
looking at top, it's nearly 100% multithreaded.

So, CUDA is not much faster. I think the fact that it speeds up as we decrease
the block per thread means, among other things, that there's a lot of serialization
going on. So, how do I improve performance.

1. Right now each step has a call to CUDA. Could combine them all
into one call.

2. Unroll the the first loop encode_ints and assign a thread.

That's all I've got. I still haven't figure out how to logically parallelize
the encode across threads because it's a dynamic programming problem.
