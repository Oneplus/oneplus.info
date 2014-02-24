---
layout: note
date: 2011-12-1
title : "使用cmake构建项目"
categories:
  - "Programming"
tags: ["C/C++", "cmake"]
author: Oneplus
---

### 动机

不用手写Makefile，够快速构建C/C++项目

### 方法

使用cmake工具可以很方便地构建项目，只需要简单地写几个CMakeLists.txt就可以了。我采用的文件夹构架为：

~~~bash
./
 |- ./bin/
 |- ./build/
 |- ./data/
 |- ./src/
~~~

在./src下面写CMakeLists.txt。它做的事情只有一件：指定将某些源文件编译成可执行程序，具体内容：

~~~bash
ADD_EXECUTABLE(wordseg, Alphabet.cpp, ...)
~~~

由于要写一堆x.cpp，最好的办法是写一个小脚本:

~~~bash
ls *.cpp | \
awk 'BEGIN{print "ADD_EXECUTABLE(wordseg,"}{print "\t"$0";"}'
~~~

同时还要在项目的根目录下写CMakeLists.txt，它做的事情有：

1. 指定./src是项目的子目录，这样cmake就会去./src中找CMakeLists.txt了，语句是：`ADD_SUBDIRECTORY(src)`
2. 指定编译的可执行程序在./bin，语句是：`SET(EXECUTABLE_OUTPUT_PATH,${PROJECT_SOURCE_DIR}/bin)`
3. 这里注意两个变量`${PROJECT_BINARY_DIR}`与`${PROJECT_SOURCE_DIR}`，第一个是运行cmake的路径，第二个是cmake [path]中的path
