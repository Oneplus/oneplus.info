---
layout: note
title : "ggplot2在一幅图上画两条曲线"
categories: "Programming"
tags: ["R", "ggplot2"]
author: Oneplus
---
print(data)后的结果是

~~~bash
C     BROWN.P   MI.P
0     0.9216 0.9282
30    0.9240 0.9282
100   0.9255 0.9282
~~~

现想要在一张图中画两条曲线。横轴为C，纵轴分别为BROWN.P和MI.P，如何做？

其实很简单

~~~r
p1<-ggplot(brown.results, aes(x=C)) + 
            geom_point(aes(y=BROWN.P), ) + 
            geom_line(aes(y=BROWN.P, , color="cyan")) +
            geom_point(aes(y=MI.P)) + 
            geom_line(aes(y=MI.P, color="red"))
~~~
