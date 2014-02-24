---
layout: note
title: "R语言中动态安装库"
categories: "Programming"
tags: ["R"]
---
在一个R脚本中，我们使用了某些library，但是发现运行环境中没有这个library，如果能检测一下有没有这个包，没有就自动安装该多好。而R中非常方便地支持这些，只要联网。

代码如下：

~~~r
site<-"http://cran.r-project.org"
if (!require("ggplot2")) { install.package("ggplot2", repos=site) }
~~~
