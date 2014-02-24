---
layout: note
title: "Automake简明用法"
categories: "Programming"
tags: ["Automake", "C/C++"]
---
Automake的使用方法请遵照以下步骤：

1. autoscan
2. 将configure.scan更名为configure.in，并修改内容
3. 添加NEWS、README、ChangeLog、AUTHORS文件
4. 将/usr/share/automake-1.X/目录下的depcomp和complie文件拷贝到本目录下
5. aclocal
6. autoconf
7. autoheader（这里原文有错）
8. automake -a
9. ./configure make

### 参考

* [例解autoconf和automake生成Makefile文件](http://www.ibm.com/developerworks/cn/linux/l-makefile/)
