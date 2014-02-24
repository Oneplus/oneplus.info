---
layout: note
title: "Matlab求三重积分"
categories: "Programming"
tags: ["Matlab"]
---

求 `\(\int_0^1 \int_0^1 \int_0^1 sin(\pi x_1 x_2 x_3) dx_1 dx_2 dx_3\)`

代码是:

~~~matlab
triplequad(@(x,y,z)sin(pi*x*y*z), 0,1,0,1,0,1)
~~~
