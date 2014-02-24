---
layout: note
title: "Python module中的全局变量"
categories: "Programming"
tags: ["Python"]
---

我想要实现一个python module，这个module中有一些配置项，这些配置项可以被读取，被修改。一个可行的方案是把这些配置项写到一个叫settings.py的文件中。

现在我有一个叫zz的module，它的文件结构是这样的：

\_\_init\_\_.py

~~~python
__all__=['sleep', 'wake', 'settings']

from sleep import fall_asleep
from wake import wake_up
~~~


settings.py

~~~python
z=-1
zz=-1
zzz=-1
~~~


sleep.py

~~~python
import zz.settings

def fall_asleep():
    zz.settings.z=1
    zz.settings.zz=2
    zz.settings.zzz=3
~~~

wake.py

~~~python
import zz.settings

def wake_up():
    print "%d %d %d" % (zz.settings.z,
        zz.settings.zz, zz.settings.zzz)
~~~

测试文件是这样的：

test.py

~~~python
import zz

zz.wake_up()
zz.fall_sleep()
zz.wake_up()
~~~

实验结果是这样的

~~~bash
-1 -1 -1
1 2 3
~~~

