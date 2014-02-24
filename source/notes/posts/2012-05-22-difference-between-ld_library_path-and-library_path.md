---
layout: note
title: "LD_LIBRARY_PATH与LIBRARY_PATH的区别"
categories: "Programming"
tags: ["Linux", "Compiling & Linking"]
---

看起来很像，但是完全是两码事。

> LIBRARY_PATH is used by gcc before compilation to search for directories containing libraries that need to be linked to your program.

LIBRARY_PATH是编译时候用的

> LD_LIBRARY_PATH is used by your program to search for directories containing the libraries after it has been successfully compiled and linked.

LD_LIBRARY_PATH是程序运行是使用的

### 参考

* [LD_LIBRARY_PATH vs LIBRARY_PATH](http://stackoverflow.com/questions/4250624/ld-library-path-vs-library-path)

