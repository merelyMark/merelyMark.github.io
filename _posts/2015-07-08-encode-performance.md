---
layout: post
title: "CUDA, zfp encoding and performance"
author: mark_kim
modified:
#excerpt: "A post to test author overrides using a data file."
date:   2015-07-08 15:00
tags: []
---

So, it has been a month since I last updated. I've converted the new
ZFP encoder to CUDA. Huzzah! And everything seems to work. Huzzah!

Once the initial port was done, I tested the performance. 


CUDA 6.0 with a Core i7-4720 and an Nvidia GTX-860m with 4GB of RAM (Maxwell)
in release with no copy back recorded during timing.

No shared memory.

{% highlight python %}
(3091.52 + 3105.43 + 3108.58)/3 = 3101.84
{% endhighlight %}

Having the Bit class use shared memory.

{% highlight python %}
(2799.91 + 2805.14 + 2803.31)/3 = 2802.79
{% endhighlight %}

Running through nvcc profiler, it appears that global load/stores are 
only running at 25% capability. Further, changing a frequently used unsigned long long (the variable that turns the 64x64 matrix
sideways, x) to shared memory results in:

{% highlight python %}
(2796.56 + 2786.94 + 2773.43)/3 = 2785.64
{% endhighlight %}

The profiler doesn't really change much though in regards to load/stores. 
And increasing the shared memory usage increased performance slightly. 
So, let's put more into shared memory, the precision.

{% highlight python %}
(3423.19 + 3449.73 + 3447.96)/3 = 3440.29
{% endhighlight %}

That's weird. This increases the occupancy of shared memory, but decreases 
performance. If I were to guess, I'd say that there's a resource constraint
between the number threads in a block and how much shared memory I'm requesting.
So, reducing the threads per block (from 32 to 16),

{% highlight python %}
(2826.13 + 2821.2 + 2803.23)/3 = 2816.85
{% endhighlight %}

So, there's obvious resource contention between the threads per block and
how much shared memory is requested. So, what happens if we don't have x
in shared memory, but we keep the threads per block at 16?

{% highlight python %}
(2315.37 + 2342.99 + 2339.93) / 3 = 2332.76
{% endhighlight %}

That's a nice improvement. But, the efficiency and occupancy are still pretty bad.

![My helpful screenshot]({{ site.url }}/images/screenshot.png)


Looking at the ptxas for cudaencode, we see that it uses 142 registers when run with 
x (the variable that pivots the 64x64 table). The max registers
for a thread is 255 for both Kepler and Maxwell. Using too many registers 
reduces occupancy (which reduces latency hiding). But, decreasing registers 
by putting precision in shared memory, reduced performance. Weird.

So, this appears to be the sweet spot for this particular card with this
particular setup. *sigh*
