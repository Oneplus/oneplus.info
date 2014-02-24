---
layout: note
title : "Core Dump总结"
categories: "Linux"
tags: ["Shell"]
author: Oneplus
---
### 查看现在系统dump core的情况
~~~
ulimit -c
~~~
结果表示core文件的大小。如果显示0，则不会dump core，显示unlimited不限制core文件大小

### 打开dump core
只要指定core文件大小不是0，系统就会打开dump core的功能。通过命令在~/.bash_profic中添加
~~~bash
ulimit -S -c unlimited > /dev/null 2>&1
~~~

就可以指定dump core了。

### 指定core文件包含进程pid

/proc/sys/kernel/core_uses_pid控制core文件是否包含进程pid。cat这个文件，如果是0，则不会包含pid扩展名，否则包含。

我遇到一个问题，即使在root下，用vi无法编辑这个文件。所以在root下用

~~~bash
echo "1" > /proc/sys/kernel/core_uses_pid
~~~

### 使core文件花样更多

`/proc/sys/kernel/core_pattern`这个文件制定了core文件保存位置和文件格式。可以在core文件中添加一些比较友好的信息，比如产生core的进程，core产生的时间等等。
具体也是在root下。

~~~bash
echo "./core-%e-%p-%t" > /proc/sys/kernel/core_pattern
~~~

至于更多奇怪的play，可以参考最后一个link。

### 参考
* [Linux上Core Dump文件的形成和分析](http://stblog.baidu-tech.com/?p=1684)
* [linux下生成core dump文件方法及设置](http://www.cppblog.com/kongque/archive/2011/03/07/141262.html)
* [打开系统core dump及其配置](http://www.ms2006.com/archives/151)

