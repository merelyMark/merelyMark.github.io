---
layout: post
title: "Raycasting problem"
author: mark_kim
modified: 
date:   2015-10-08 18:00
tags: [todo]
---

So, I have raycasting problem because of the flipping problem.

![4096 edelta](/images/2015-10-08/edelta-4096-raycasting.png)

```
2047564 52755733446 (382, 467) (2125, 2245, 1788)(0.0834946, 0.0831422,0.0834929)
idx:2392006 0.470789 idx:2392034 0.489495 idx:2392020 0.499744 idx:2392048 0.512534 idx:2392007 0.461684 idx:2392035 0.494278 idx:2392021 0.471646 idx:2392049 0.510473 
(2125,2245,1788) (2126,2245,1788) (2125,2246,1788) (2126,2246,1788) (2125,2245,1789) (2126,2245,1789) (2125,2246,1789) (2126,2246,1789) 
(0.946598,0.305105,-0.104229) (0.968664,0.247301,0.0230527) (0.946598,0.305105,-0.104229) (0.259585,0.787189,0.559419) (-0.787511,0.0143994,0.616132) (0.946598,0.305105,-0.104229) (-0.912533,-0.395399,0.104607) (0.946598,0.305105,-0.104229) 
0.104229
3425362 52770409398 (385, 466) (2127, 2247, 1896)(0.0806571, 0.0823047,0.082634)
idx:3973712 0.436599 idx:3980000 0.431067 idx:3974561 0.470642 idx:3980926 0.467678 idx:3973713 0.447507 idx:3980001 0.448303 idx:3974562 0.469414 idx:3980927 0.456854 
(2127,2247,1896) (2128,2247,1896) (2127,2248,1896) (2128,2248,1896) (2127,2247,1897) (2128,2247,1897) (2127,2248,1897) (2128,2248,1897) 
(-0.365648,-0.405451,0.837802) (-0.322118,-0.437337,0.839629) (-0.365648,-0.405451,0.837802) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.365648,-0.405451,0.837802) (-0.322118,-0.437337,0.839629) 
0.837802
3431005 52770423710 (391, 466) (2133, 2247, 1898)(0.0819472, 0.0823047,0.0826181)
idx:3980227 0.407473 idx:3980255 0.404806 idx:3981223 0.321177 idx:3981251 0.33671 idx:3980228 0.362973 idx:3980256 0.353872 idx:3981224 0.339722 idx:3981252 0.340952 
(2133,2247,1898) (2134,2247,1898) (2133,2248,1898) (2134,2248,1898) (2133,2247,1899) (2134,2247,1899) (2133,2248,1899) (2134,2248,1899) 
(-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) 
0.839629
3425362 52770409398 (385, 466) (2127, 2247, 1896)(0.0806571, 0.0823047,0.082634)
idx:3973712 0.436599 idx:3980000 0.431067 idx:3974561 0.470642 idx:3980926 0.467678 idx:3973713 0.447507 idx:3980001 0.448303 idx:3974562 0.469414 idx:3980927 0.456854 
(2127,2247,1896) (2128,2247,1896) (2127,2248,1896) (2128,2248,1896) (2127,2247,1897) (2128,2247,1897) (2127,2248,1897) (2128,2248,1897) 
(-0.365648,-0.405451,0.837802) (-0.322118,-0.437337,0.839629) (-0.365648,-0.405451,0.837802) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.322118,-0.437337,0.839629) (-0.365648,-0.405451,0.837802) (-0.322118,-0.437337,0.839629) 
0.837802
3133490 52770113920 (381, 468) (2124, 2244, 1792)(0.0833098, 0.0831983,0.0834611)
idx:3639885 0.462915 idx:3639889 0.462209 idx:3639887 0.479045 idx:3639891 0.475876 idx:3639886 0.495863 idx:3639890 0.499365 idx:3639888 0.436755 idx:3639892 0.437316 
(2124,2244,1792) (2125,2244,1792) (2124,2245,1792) (2125,2245,1792) (2124,2244,1793) (2125,2244,1793) (2124,2245,1793) (2125,2245,1793) 
(0.879365,0.443225,0.173979) (-0.787511,0.0143994,0.616132) (0.879365,0.443225,0.173979) (-0.787511,0.0143994,0.616132) (-0.787511,0.0143994,0.616132) (-0.787511,0.0143994,0.616132) (-0.787511,0.0143994,0.616132) (-0.787511,0.0143994,0.616132) 
0.173979
3424919 52770408660 (378, 467) (2121, 2246, 1892)(0.0826426, 0.0823687,0.0826659)
idx:3973204 0.490455 idx:3973232 0.514374 idx:3973206 0.516093 idx:3973234 0.523114 idx:3973205 0.516038 idx:3973233 0.540412 idx:3973207 0.513995 idx:3973235 0.519765 
(2121,2246,1892) (2122,2246,1892) (2121,2247,1892) (2122,2247,1892) (2121,2246,1893) (2122,2246,1893) (2121,2247,1893) (2122,2247,1893) 
(-0.380765,-0.439631,0.813476) (-0.380765,-0.439631,0.813476) (-0.365648,-0.405451,0.837802) (-0.365648,-0.405451,0.837802) (-0.380765,-0.439631,0.813476) (-0.365648,-0.405451,0.837802) (-0.365648,-0.405451,0.837802) (-0.365648,-0.405451,0.837802) 
0.813476
```

Picking in the dark, highlighted region produced a z (good values are around 1890, while bad values are around 1790). value different from the surrounding, correct region. I don't know why. It doesn't look like a grazing problem, i.e. hitting a seam between blocks. 

I think this will be the last problem I fix.