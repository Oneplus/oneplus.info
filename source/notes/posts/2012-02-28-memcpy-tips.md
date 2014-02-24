---
layout: note
title: "memcpy用法小Tips"
categories: "Programming"
tags: ["C/C++"]
---
根据cpp reference中，`memcpy`的函数形式是：

~~~c
void * memcpy(void *src, void *dst, sitze_t size);
~~~

其中size应该包含类型大小，使用时注意这个值是num*sizeof(type)。

另外，这个函数把dst返回了回来，一般用不上。
