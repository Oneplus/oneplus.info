---
layout: post
status: publish
published: true
title: 程序设计实践一 - 第一课
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "<div>\r\n<div id=\"outline\">\r\n### 课程提纲\r\n<ul>\r\n* 课程介绍\r\n* 算法复杂度分析\r\n* 程序的三种控制结构\r\n* 递推\r\n* 递归\r\n</ul>\r\n</div>\r\n"
wordpress_id: 118
wordpress_url: http://blog.oneplus.info/?p=118
date: 2011-03-02 19:26:40.000000000 +08:00
categories:
- 可以控制
- HIT ACM/ICPC Group
- 程序设计实践
tags:
- ACM Group
- 程序设计实践
- 不靠谱
comments:
- id: 45
  author: WyvernBai
  author_email: codefate1992@gmail.com
  author_url: http://asiteof.me
  date: !binary |-
    MjAxMS0wMy0wMiAxOTo1ODoxNiArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wMiAxMTo1ODoxNiArMDgwMA==
  content: 加了个油的！～
- id: 46
  author: Oneplus
  author_email: oneplus.lau@gmail.com
  author_url: http://blog.oneplus.info
  date: !binary |-
    MjAxMS0wMy0wMiAyMDozMjowNCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wMiAxMjozMjowNCArMDgwMA==
  content: 谢了个谢呀~
- id: 47
  author: nonleft
  author_email: qyorewang@gmail.com
  author_url: http://blog.nonleft.me
  date: !binary |-
    MjAxMS0wMy0wMiAyMTo0MzowNyArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wMiAxMzo0MzowNyArMDgwMA==
  content: 刘老湿的黄色网站……
- id: 48
  author: GTmac
  author_email: gtmacchc@gmail.com
  author_url: http://gtmac.info
  date: !binary |-
    MjAxMS0wMy0wMyAyMTo1MzowMCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wMyAxMzo1MzowMCArMDgwMA==
  content: +u~ 你要考T啊~~？
- id: 49
  author: KJlmfe
  author_email: kjlmfe@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMS0wMy0wMyAyMjoyNjo1NSArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wMyAxNDoyNjo1NSArMDgwMA==
  content: 支持学长 学长很给力啊 上课很诙谐幽默
- id: 50
  author: Oneplus
  author_email: oneplus.lau@gmail.com
  author_url: http://blog.oneplus.info
  date: !binary |-
    MjAxMS0wMy0wMyAyMjo0MDowMCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wMyAxNDo0MDowMCArMDgwMA==
  content: 是这样计划的。闲着无聊，找点事做。
- id: 51
  author: rukata
  author_email: stf9311@163.com
  author_url: ''
  date: !binary |-
    MjAxMS0wMy0wNiAyMzo1OToxOSArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wNiAxNTo1OToxOSArMDgwMA==
  content: 。。很可惜没有选。。。原来是你做TA。。。。
- id: 52
  author: Oneplus
  author_email: oneplus.lau@gmail.com
  author_url: http://blog.oneplus.info
  date: !binary |-
    MjAxMS0wMy0wNyAwODozNjowMyArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wNyAwMDozNjowMyArMDgwMA==
  content: 没选也可以去听啊：）
- id: 53
  author: rukata
  author_email: stf9311@163.com
  author_url: ''
  date: !binary |-
    MjAxMS0wMy0wOCAxODoyMzoxNyArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0wOCAxMDoyMzoxNyArMDgwMA==
  content: ! '....所以我来了。。。。。'
---

### 课程提纲

* 课程介绍
* 算法复杂度分析
* 程序的三种控制结构
* 递推
* 递归

### 简单的讲义
本次课程实在是太简单了，所以不计讲义了。课件下载请点<a href="http://acm.hit.edu.cn/~oneplus/design-2011/01.pdf">这里</a>

### 有关课程的一些丫丫
在开始准备第一课时，我尽力让自己保持一种轻松愉快的心情。结果内容非常不靠谱，或者说是weird。本意是用一些更贴近大一同学的方式使更多的同学对课程产生兴趣，不过反馈效果不明显，下节课还是正经点，多搞点动画什么的吧。

去二区的时候堵了一路车，无语。下次自己去，还要再早点。

本来是打算用自己的笔记本作演示，但由于堵车迟到，这件事就只好作罢。结果原来准备的用matlab画Sierpinski triangle的动画泡汤了。这里贴出土鳖的matlab代码，路过轻拍。

~~~matlab 
function Sierpinski(x, y, l, d)
if( d == 0 )
    axis off;
    hold on;
    triangle(x, y, l, 1);
end;
if( d < 6 )
    triangle(x, y, l / 2, -1);
    pause(0.001);
    Sierpinski(x - l / 4, y - l / 4 * sqrt(3) / 3, l / 2, d + 1 );
    Sierpinski(x + l / 4, y - l / 4 * sqrt(3) / 3, l / 2, d + 1 );
    Sierpinski(x, y + l / 2 * sqrt(3) / 3, l / 2, d + 1 );
end;

function triangle( x, y, l, d )
x1 = x - l / 2;
x2 = x + l / 2;
x3 = x;

y1 = y - d * l / 2 * sqrt(3) / 3;
y2 = y - d * l / 2 * sqrt(3) / 3;
y3 = y + d * l * sqrt(3) / 3;

fill([x1 x2 x3], [y1 y2 y3], 'w');
~~~

不能使用笔记本的另一个坏处就是，原计划进行的课程录音杯具了。下节课早点去二区，心平气和地把这件事做清楚吧。

第一课的难度实在是太简单了，所以我想当然地认为下次课的出勤还应该不错。不过这只是我个人的一些臆想。一周后再看结果吧。

作为一门选修课，而且是我承诺不点名的选修课，衡量其成败的唯一标准大概就是课程的出勤了。怎样分配难易，一个问题要讲多深才能把握大部分听众的兴趣又让人觉得有一定的趣味，希望我能撞大运把这件事做好吧。

### P勒个S

* 3月1日上午，与班长张晨同学一行前往计算机学院团委办公室上交
* -“那么请问，您对本次访问有很感想呢？” -“刘屁民诚惶诚恐，屁滚尿流，不敢草率了事啊。”<
* 按照车老师的想法，Language Grid的调研工作将要深入到系统的源码中，顿感压力巨大
* 本月结束前要将toefl词汇背完一遍，现在还有三十余个list。这不是坑爹吗！

