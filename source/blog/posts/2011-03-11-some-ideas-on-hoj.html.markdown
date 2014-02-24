---
layout: post
status: publish
published: true
title: 关于HOJ以及Online Judge系统的一些胡诌
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "今天上体系结构溜号的时候突然想到了<a href=\"http://acm.hit.edu.cn\">HOJ</a>的问题。虽然喊HOJ需要修，喊了也有挺长时间，不过似乎真的没有认真考虑一下HOJ要修成或者重写成什么样。
  \r\n"
wordpress_id: 132
wordpress_url: http://blog.oneplus.info/?p=132
date: 2011-03-11 14:50:22.000000000 +08:00
categories:
- 不可控制
- 胡蒙胡诌和胡思乱想
tags:
- ACM Group
- 不靠谱
- HOJ
- Online Judge
comments:
- id: 58
  author: GTmac
  author_email: gtmacchc@gmail.com
  author_url: http://gtmac.info
  date: !binary |-
    MjAxMS0wMy0xMiAwMDoxMjo1MSArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0xMSAxNjoxMjo1MSArMDgwMA==
  content: YM作者&amp;LS所有&amp;LX所有
- id: 60
  author: xiaodao
  author_email: lychees67@gmail.com
  author_url: http://www.shuizilong.com/house
  date: !binary |-
    MjAxMS0wMy0xMyAyMzozNTowNCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0xMyAxNTozNTowNCArMDgwMA==
  content: ! "resources 和 service 的分离似乎只在理论上可行。。\r\n目前是这样的没错。。。）\r\n先把必备条目修复之前讨论一下方向也不错。。\r\n\r\nHOJ
    目前的架构是仿 UVA .. ？ 但似乎社交向... 诸如 Blog Entry、Group、Download Code （坏）...  久而久之渐渐没有人用，部分
    Link 也一直坏链 ... 以及那个重口味的 Discuss 。。。 ... 如果这几个项目不能脱蛹，大可砍掉重练。。。"
- id: 65
  author: ZhangQida
  author_email: takanoter@gmail.com
  author_url: http://takanoter.me
  date: !binary |-
    MjAxMS0wMy0xNyAxOToyODowNCArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0xNyAxMToyODowNCArMDgwMA==
  content: 把题目质量上去了，就好了。
- id: 69
  author: Lancelot
  author_email: lycanlancelot@gmail.com
  author_url: http://NONE
  date: !binary |-
    MjAxMS0wMy0yMyAyMDoxNjoxMyArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wMy0yMyAxMjoxNjoxMyArMDgwMA==
  content: 学长的画面做的让人敬畏，我看了这么多blog，您是头一个外观看起来很有范的
---
今天上体系结构溜号的时候突然想到了<a href="http://acm.hit.edu.cn">HOJ</a>的问题。虽然喊HOJ需要修，喊了也有挺长时间，不过似乎真的没有认真考虑一下HOJ要修成或者重写成什么样。 

如果只是修内核的bug，再把UI作得漂亮一些，真的不如不修，直接下一个北大开发的Open Judge搭上就行了。DaLord曾经强调搞OJ要有自主的东西，所以我们再开发一个Open Judge，搞微学习，除了恶趣味就没有别的趣味了。 

想到HUST的Virtual Judge，现在这么火，大大小小的学校、大大小小的比赛在上面搞得不亦乐乎。实际上，VJudge做的工作只是将提交到上面的代码再提交到别的Judge上，根据别人的返回结果返回。技术上是没有什么创新之处，即使没有Web开发经验的人如我也大概能猜到用什么样的手段、什么样的函数实现。不过他确实在国内ACM/ICPC圈子中很火。 

最近在一直在做Language Grid的调研，满脑袋都是一坨一坨的Java代码，在今天溜号时，突然对于VJudge的事好像有点明白了。 

包括HOJ在内的Online Judge系统，都可以归纳为三个层次，users、service、resources。这里的service可以理解成运行在OJ服务器上的服务器程序，而resources是保存在服务器上的标准输入数据和标准输出数据。users提交题目的行为实际上是通过service，调用resources。而现在国内众多Online Judge系统，普遍的模式是：service与resources放在同一个服务器上。如图

<div align="center"><img src="http://blog.oneplus.info/wp-content/uploads/2011/03/1.png" width="40%"/></div>

而VJudge做的则是在users和service中再加入了一个service，这种做法在只有一个server的时候是很荒唐的。但是，在server的数量非常多的时候，就变得非常牛了。

<div align="center"><img src="http://blog.oneplus.info/wp-content/uploads/2011/03/2.png" width="60%"/></div>
通过一个VJudge，就可以实现一场在线比赛中，即有国内OJ的题目，又有国外OJ的题目。 

现在OJ系统中面临的一些问题：一个是，资源的重复，一道题目，HOJ有、HDOJ有、POJ也有、ZOJ也有、NKUOJ、HUSTOJ、FOJ都有。另一个是，不同的OJ系统速度不同。一份在HOJ要跑1000ms的代码，可能在HDOJ只用500ms。所以，我在想，既然VJudge把users和server分开了，能不能将resources和service分开，将service分成若干层次，如图。

<div align="center"><img src="http://blog.oneplus.info/wp-content/uploads/2011/03/3.png" width="80%"/></div>

这样，powerful server的用作完成传统意义上的Judge service，保证了统一，提供题目的接口，而题库、比赛系统以及用户系统可以保存在各学校的node上，node通过server的接口获得传统意义上的在线评测。 

丫丫到这里，发现以及严重跑题，最关键的还是不能解决HOJ要修成什么样这个问题。哎，算了，回去读代码吧。
