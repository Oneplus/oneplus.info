---
layout: note
title: Shell的一些小技巧
author: Oneplus
category: ["Linux"]
tags:
    - "shell"
    - "sed"
    - "sort"
    - "uniq"
---

会逐步在这个note里面整理一些实用的shell小命令。解决的主要问题是自然语言处理。

### 将连续空格替换为,或回车

一般用来将切分的句子编程变成一个词一行(词列表)。

~~~
sed -r -e 's/[[:space:]]/\n/g'
~~~

### 对于无序的词列表按照词频排序

这个在做词频统计时特别有用

~~~
sort | uniq -c | sort -rn
~~~

### 让awk打印第一列之后的数据

原理是把第一列清空，然后打印全列

~~~
awk '{$1=""; print $0}'
~~~

### 统计词列表中最长的词

~~~
awk '{print $0" "length}' | sort -k2 -nr | head -1
~~~

### 去掉符合模式的某些行

`grep -v`已经提供这个功能了

~~~
grep -v
~~~
