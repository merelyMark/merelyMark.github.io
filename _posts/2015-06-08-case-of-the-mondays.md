---
layout: post
title: "Update about Nebo and ZFP"
author: mark_kim
modified:
#excerpt: "A post to test author overrides using a data file."
date:   2015-06-08 10:00
tags: []
---

Two weeks ago I was on vacation in Dublin.

Last week on Tuesday, Peter, Chris and I met and we hashed out some stuff about ZFP and
Nebo. I agreed to quickly try to hack ZFP into Nebo. We thought it would be easy, 
(looking at you line 605 in NeboLHS.h) but it wasn't that simple. NeboLHS and
NeboRHS aren't persistent with memory, i.e. the memory comes from a memory manager.

So, my idea to just instantiate ZFP right in NeboLHS
and NeboRHS didn't really work. To test my hypothesis that it was about
not using the memory manager (MemoryWindow) I save everything first to ZFP and then 
save it to "base_" memory as well in seqwalk_assign. Then, A more correct answer is the result.

So, while I wait for Peter to give me the updated version of ZFP (with more powah!)
I'll continue to try to hack ZFP into Nebo. This time, I'm putting ZFP 
directly into SpatialField.h.




