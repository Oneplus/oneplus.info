---
layout: note
title: "Python sorted list的实现"
categories: "Programming"
tags: "Python"
---
具体思路是用二分保list有序+插入

~~~python
class SortedList(list):
    K = -1

    def __init__(self, K=-1):
        list.__init__(self)
        if K != -1: self.K = K

    def append(self, x):
        bisect.insort(self, x)
        if self.K != -1:
            if len(self)==self.K+1:
                self.pop(0)
~~~

这里还有一个限size的操作，之前写了一个`self=self[1:]`，结果不对。还不清楚是为什么，留一个问题在这里。

#### 参考

* [Python - sorted list of lists](http://stackoverflow.com/questions/5998368/python-sorted-list-of-lists)

