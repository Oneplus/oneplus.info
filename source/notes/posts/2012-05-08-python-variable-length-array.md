---
layout: note
title: "Python的变长参数"
categories: Programming
tags: "Python"
---

~~~python
def foo1(*args):
    for arg in args: print arg

def foo2(**kargs):
    for key in kargs:
        print key, kargs[key]

def foo3(*args, **kargs):
    print "args:"
    for arg in args:
        print arg

    print "kargs":
    for key in kargs:
        print key, kargs[key]
~~~

这里面有`*args`,`**kargs`并存的问题

调用一下试试看

~~~python
if __name__=="__main__":
    foo1("a", "b", "c")
    print "==========="
    foo2(a=1,b=2,c=3)
    print "==========="
    foo3("a", "b", "c", a=1, b=2, c=3)
~~~

得到结果是

~~~bash
a
b
c
=========
a 1
c 3
b 2
=========
args:
a
b
c
kargs:
a 1
c 3
b 2
~~~
