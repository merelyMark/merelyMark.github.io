---
layout: post
title: "speedup octree lookup"
author: mark_kim
modified:
date:   2015-09-30 12:00
tags: []
---
Changed the search for which sub-voxel from:

{% highlight c++%}
        if (find_z < mz){
            if (find_y < my){
                if ( find_x < mx ){
                    ch = 0; //000
                }
                else{
                    ch = 4; //100
                }
            }
            else{
                if ( find_x < mx ){
                    ch = 2; //010
                }
                else{
                    ch = 6; //110
                }
            }
        }
        else{
            if (find_y < my){
                if ( find_x < mx ){
                    ch = 1;   //001
                }
                else{
                    ch = 5;   //101
                }
            }
            else{
                if ( find_x < mx ){
                    ch = 3;   //011
                }
                else{
                    ch = 7;  //111
                }
            }
        }
{% endhighlight%}

to 

{% highlight c++ %}
        ch = !(find_z < mz);
        ch += !(find_y < my) << 1;
        ch += !(find_x < mx) << 2;
{% endhighlight%}

On my laptop (i7-4720HQ) using the multicore CPU version with 1024^3 of the ICE train, UFLIC went from taking 19.38s to 16.99s (vs 11.5774s with a neighborhood index).

Hopefully, the GPU will show even better performance increase because of reduced control flow.