---
layout: post
status: publish
published: true
title: 使用CodeIgniter框架编写Web应用
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "<div>### 总结\r\n总的来讲，这次软件工程的课设收获是挺大的。学到的东西包括\r\n<ul>\r\n\t<li>MVC的一些思想</li>\r\n\t<li>CodeIgniter框架</li>\r\n\t<li>简单应用了一下jQuery
  UI</li>\r\n\t<li>一点Ajax(最后没用上)</li>\r\n\t<li>用JavaScript将本地文件内容放到textarea中</li>\r\n\t<li>SVN和Google
  Code</li>\r\n</ul>\r\n"
wordpress_id: 319
wordpress_url: http://blog.oneplus.info/?p=319
date: 2011-06-23 15:15:51.000000000 +08:00
categories:
- 可以控制
- 挨踢民工
tags:
- PHP
- CodeIgniter
- 软件工程
- jQuery
- Google Code
- SVN
- MVC
comments:
- id: 165
  author: 上海运输发票
  author_email: u3sujw@126.com
  author_url: http://www.shfapiao.net
  date: !binary |-
    MjAxMS0wNi0yNyAwMDozNDozNyArMDgwMA==
  date_gmt: !binary |-
    MjAxMS0wNi0yNiAxNjozNDozNyArMDgwMA==
  content: 路过,支持一下！！！
- id: 2212
  author: replicaralphlaurenchea
  author_email: byyhckm@aol.me
  author_url: http://exquisite-ralph
  date: !binary |-
    MjAxMy0wMy0xNyAyMzoyNjozNSArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wMy0xNyAxNToyNjozNSArMDgwMA==
  content: Fascinating blog! Is your theme custom made or did you download it from
    somewhere? A theme like yours with a few simple tweeks would really make my blog
    stand out. Please let me know where you got your theme. Thanks replica ralph lauren
    cheap http://exquisite-ralph-lauren-polo-for-sale.webs.com
---
### 总结

总的来讲，这次软件工程的课设收获是挺大的。学到的东西包括

* MVC的一些思想
* CodeIgniter框架
* 简单应用了一下jQuery UI
* 一点Ajax(最后没用上)
* 用JavaScript将本地文件内容放到textarea中
* SVN和Google Code

因为一开始时觉得组里其他几位没写过php，要是再套一套框架进来，预计花在学习上的时间要大于花在工作的时间上。而且，代码还是自己的比较好控制，所以就鲁莽地决定淡化合作这件事，自己从内部逻辑到前端一并做了。整个软件工作量还不太大，所以也不是很有压力。课设的几天说说笑笑，再看了一天漫画，还好。

### 关于MVC

对于MVC，我个人的一些体会是

1. 软件的各模块在这样的框架下耦合得比较轻，对于某一部分的修改可以相对独立地进行而不伤及其他部分。
2. 通过MVC，软件可以比较容易实现层次模型。
3. 一些面向对象的设计思想在MVC的框架下也比较容易实现。
4. 比较重要的是程序员的头脑中，软件不是那么一坨。

这些感触，一方面是我个人做过硬编程的网站，另一方面是很长一段时间都在面对一个硬编程的网站-HOJ，对于那一坨的感觉比较清晰。说实话，整个课设都按自己的思路，非常清楚软件在什么地方应该放什么东西，写完还可以回顾一下，如果觉得哪个地方不爽了就删了重写，还是有一点小激动的。

### CodeIgniter

起初是打算用Zend Framework来做的，但是从网上把那30多M的开发框架下下来，我就湿了。恐怕第一次就要玩高难度动作也是这感觉吧>:D。

ZF不可靠，只好重新规划。搜索“敏捷开发、PHP、轻量级框架”后，CodeIgniter被选中。（实际上是，没有别的可选-，-）然后用半天时间来熟悉，发现确实挺敏捷的。这篇是总结文不是技术文，所以不在如何开发上画太多笔墨。CI的官方论坛说得挺清楚的。

简单统计了一下，整个软件大致在4000行左右，从开始到现在大约用了一周的有效时间，没有达到我预期7天的1万行的目标。一方面是因为开发框架比较好用，另一方面，我的代码风格一向比较紧凑，不撑场面，最大的一个控制器也就只有300多行。所以还像前面说的，工作量不算大。

### 关于sewiki

题目的名字是“基于wiki的协同写作系统”，名为“伪基写作”，就是又假又搞基的意思。整个软件实现的功能基本是版本控制和论坛的合体。现在的版本中，用到的最复杂的逻辑是一个拓扑排序判环，其他都是民工级代码。而且漏洞无数，毫无安全性可言。不知道有没有人有兴趣一起来改改，恐怕是没有人。

### 几个土鳖的地方

#### 添加无限个章节依赖盒

在添加章节依赖的功能上，用jQuery写了一个与Cpanel中“添加上传盒”功能类似的“添加章节依赖盒”。

<a href="http://blog.oneplus.info/wp-content/uploads/2011/06/01.jpg"><img src="http://blog.oneplus.info/wp-content/uploads/2011/06/01.jpg" alt="" title="01" width="347" height="138" class="aligncenter size-full wp-image-322" /></a>

基本思路是

* 需要一个num_rows表示盒子数。准备一个table，其中一个button占一行，命名其id为"buttonid"。还需要用一个"hidden"的input接num_rows的值
* 在页面被装载时将num_rows设置为1
* 在button上添加一个监听器。如果按下按钮，就用$("#buttonid").before()在表格中添加一行。
* 每次添加时，num_rows要加一，那个hidden的input的value用num_rows更新，以让后端知道用户一共添加了几个盒子。

现在看起来好像也没啥，不过这破玩意我搞了两个小时，摔！

#### 使用Ajax构建页面

目标是，在一个界面中搞定所有的业务逻辑。按照小雨说的，要注意的是控制器只能返回文本，不能跳转。杯具的是我的控制器里全是跳转。所以这个想法是失败了。

#### 从本地上传文件到textarea
这玩意也是用jQuery实现的，万能的JQ啊。

<a href="http://blog.oneplus.info/wp-content/uploads/2011/06/02.jpg"><img src="http://blog.oneplus.info/wp-content/uploads/2011/06/02.jpg" alt="" title="02" width="320" height="367" class="aligncenter size-full wp-image-323" /></a>

思路是：

1. 准备一个button，再准备一个不能显示的`<input id="file" type="file">`;
2. 给button添加一个监听器。如果按下按钮，就`$("#file").trigger('click')`，这下就弹出那个文件上传的框了。效果就好像是按button后弹出来的一样。
3. 然后，其实我也不知道然后怎么弄。就用firebug和alert胡乱调试，居然看到一条"data:text/plain;base64,"接着就是乱码。然后我就觉得可能是搞了base64加密，所以就写了一段我也说不清的非常鬼畜的代码，完全搞不懂他是怎么对的。

~~~javascript
$("#load_button").click(function(){
    $("#load_box").trigger('click').change(function(){
        var fobj = document.getElementById("load_box");
        if(fobj) {
            var file = fobj.files.item(0);
            if(file) {
                var filename = file.getAsDataURL();
                filename = filename.substring(23, filename.lenght);
                $("#edit_area").val($.base64Decode(filename));
            }
        }
    });
});
~~~

话说回来，好像整个开发中，纠结了的、花了时间的地方全在前端上，界面还那么难看…

### Google Code SVN

这件事上我是真圡了。在用过GIT的情况下，我还是搞了1天才搞懂SVN怎么用。具体怎么用，在前面的一张图里。

现在项目可以从<a href="http://code.google.com/p/sewiki">http://code.google.com/p/sewiki</a>那里，好像还有几处功能逻辑改变了但是没commit。

### 有关开发习惯

整个开发基本是按照issues、sub-issues、bugs的方式进行的，跟pureweb一起做HOJ时学到的，非常受用。

### 无聊的YY

这算是大学以来最大的程序了。想一想，自己从去年退役到现在，在web开发上面虽然长进不是很大，但是也算会了一点东西，掌握了一些做民工的技能，可以拿个写着“web开发”的小牌蹲道边了
