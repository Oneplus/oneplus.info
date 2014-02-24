---
layout: post
status: publish
published: true
title: Python对象的动态成员与__dict__
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "在写一些python脚本时，我很喜欢用optparse module中的OptionParser对象来解析一些命令行参数。一个简单的例子如下，\r\nparser = OptionParser()\r\nparser.add_option(\"-f\", \"--file\", dest=\"filename\")\r\n(options, args) = parser.parse_args()\r\n然后，使用options.filename可以调用--file指定的参数，这似乎也没什么神奇的。但是，在第一次用OptionParser时，我那个充满C惯性思维的大脑却很严重地shock了。因为，options对象的成员在调用期间才产生，这不科学啊。\r\n"
wordpress_id: 530
wordpress_url: http://blog.oneplus.info/?p=530
date: 2012-04-29 10:19:02.000000000 +08:00
categories:
- 可以控制
- 挨踢民工
tags:
- python
- 动态语言
comments:
- id: 2363
  author: peroinuinee
  author_email: sabatqj314@aol.com
  author_url: http://genericlevitranowonline.com/#rfssb
  date: !binary |-
    MjAxMy0wNC0xMCAxMjoxMzo1MSArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wNC0xMCAwNDoxMzo1MSArMDgwMA==
  content: ! '[url=http://genericlevitranowonline.com/#kxqii]levitra 40 mg[/url] -
    <a href="http://genericlevitranowonline.com/#rxppc" rel="nofollow">cheap levitra</a>
    , http://genericlevitranowonline.com/#wttyk order generic levitra'
- id: 3666
  author: skip
  author_email: xavierskip@gmail.com
  author_url: http://xavierskip.com
  date: !binary |-
    MjAxMy0xMC0xNyAxNjozMTo1MyArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0xMC0xNyAwODozMTo1MyArMDgwMA==
  content: ! "难道不可以直接添加的么？\r\n\r\na.x=1\r\na.z=2\r\n\r\n什么的"
---
在写一些python脚本时，我很喜欢用optparse module中的OptionParser对象来解析一些命令行参数。一个简单的例子如下，

~~~python 
parser = OptionParser()
parser.add_option("-f", "--file", dest="filename")
(options, args) = parser.parse_args()
~~~

然后，使用options.filename可以调用--file指定的参数，这似乎也没什么神奇的。但是，在第一次用OptionParser时，我那个充满C惯性思维的大脑却很严重地shock了。因为，options对象的成员在调用期间才产生，这不科学啊。

结果这个问题被搁置了大半年，今天早上又想起来，心血来潮看了一眼optparse的源代码，

~~~
self.__dict__.update(dict)
~~~

然后一下子，我似乎明白了什么。

首先，每个python对象中都用一个字典来保存其命名空间，也就是`__dict__`。举栗来讲，C.x实际上是被翻译成`C.__dict__["x"]`。那么，runtime地向C中添加一些成员就是小case了。一个栗子程序如下：

~~~python 
class C:
    def __init__(self):
        self.x = 1
        self.y = 2

    def regist(self, key, val):
        self.__dict__[key] = val

c = C()
print c.__dict__
c.regist("z", 3)
c.regist("func", lambda x: "".join(["=>", str(x), "<="]))
print c.__dict__
print c.x, c.y, c.z, c.func("__dict__")
~~~

运行结果是

~~~
{'y': 2, 'x': 1}
{'y': 2, 'x': 1, 'z': 3, 'func': <function <lambda> at 0x2b55c97de668>}
1 2 3 =>__dict__<=
~~~


不过问题就这样解决了，真是不甘心。所以发个博客吧。
P勒个S：这之前，还看过C中实现命令行解析的类库，<a href="http://argtable.sourceforge.net/">argtable</a>。C语言真是好难啊。

参考：
<ul>
<li><a href="http://docs.python.org/reference/datamodel.html">http://docs.python.org/reference/datamodel.html</a></li></ul>

