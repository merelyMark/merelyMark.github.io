---
layout: post
title: "Don't get it"
author: mark_kim
modified:
#excerpt: "A post to test author overrides using a data file."
date:   2015-05-21 19:00
tags: []
---

Read three papers Peter referred to get me familiarized with the compression stuff.

Looking at the new code Peter sent me, I still don't quite get what's being
accomplished. It would help if I knew what data was coming in. :p

So, I'm just walking through the diffusion example.


I really need to go back and review my bit operations.  

{% highlight c++ %}
for (mask = minsize ? minsize - 1 : 1; mask & (mask + 1); mask |= mask + 1);
{% endhighlight %}

In this line, mask starts at 49. The conditional, 

{% highlight c++ %}mask & (mask+1){% endhighlight %}

checks the value of mask, \\(0x110001\\), the value of mask+1 ( \\(0x110010\\) ) and 
does a logical and $$\land$$, which keeps bits that match between the two values.
 In this case, 32 and 16. However, when the mask is \\(2^d-1\\), where d is a any integer,
 then the logical and $$\land$$ is null. The incrementor is a logical or, $$\lor$$,
just keeps filling in the 0s, 

$$
0x110001\\

0x110011\\

0x110111\\

0x111111
$$

Nice. This could take a while though.	
