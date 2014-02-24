---
layout: note
title: "像'printf'一样打印变长参数"
categories: "Programming"
tags: ["C/C++"]
author: Oneplus
---

### 动机

我想实现一个可以像printf一样带参数模板的log打印函数，在调用

~~~c
line_count = 1000;
write_log("process %d lines", line_count);
~~~

打印出

~~~
process 1000 lines
~~~

### 方法

实现方法是使用stdarg.h中提供的变长参数接口。`vprintf`、`vsprintf`、`vfprintf`等等，我们可以用如下的方法实现`write_log`函数：

~~~c
void write_log(int lvl, char *fmt, ...){
    ...
    va_list list;
    va_start(list, fmt);
    vfprintf(stderr, fmt, list);
    va_end(list);
    ...
}
~~~
