---
layout: note
title: "Python对象继承set类型"
categories: Programming
tags: "Python"
---

~~~python
class Feature(set):
    def __init__(self):
        set.__init__(self)
    # 这里演示将Feature类的加号重载成set.add方法
    def __add__(self, feature):
        set.add(self, feature)
~~~
