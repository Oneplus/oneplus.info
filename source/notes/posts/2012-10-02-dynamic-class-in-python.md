---
layout: note
title: "Python中的动态类"
categories: "Programming"
tags: ["Python"]
---
有这样一个需求，我有`SegmentReader`、`PostagReader`、`ConllReader`这三个`Reader`，他们都继承于一个`Reader`类。在程序运行中，由用户通过`segment`、`postag`或`conll`决定读入哪一种数据，所以`XReader`的实例化也由用户决定。当然，我们可以写一连串的if判断，但是这往往不够美观。这里有一个python动态创建类的问题。

Python中有个一函数`globals()`返回当前全局的符号表，如果已经import了这三个类，他们就会出现在全局的符号表中。

~~~python
from corpusproc.io import SegmentReader, PostagReader, ConllReader

def createObject(className, * args):
    cls = globals()[className]

    if isinstance(cls, type) and isinstance(args[0], file):
        return cls(args[0])
    else:
        raise Exception("No such class")
~~~

测试一下

~~~python
format = "segment"
reader = createObject(format[0].upper() + format[1:])

format = "unknown"
reader = createObject(format[0].upper() + format[1:])
# Raise Exception "No such class"
~~~
