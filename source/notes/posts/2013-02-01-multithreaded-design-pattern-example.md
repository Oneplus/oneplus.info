---
layout: note
title : "Peer模式的多线程程序例子"
categories: "Programming"
tags: ["C/C++", "Multi-threaded"]
---
程序的模型大概是这样的。有一个master()，用来分发任务。有N个多线程的slave用来处理任务。

<script src="https://gist.github.com/Oneplus/7afce62520cb4cd5c926.js"></script>

主程序里可以这样调用；

<script src="https://gist.github.com/Oneplus/f6d65430d7fa6c54abb6.js"></script>

可以看出，上面这段程序还是依赖于Processor自身的并行能力。总之，现在看来写并行程序实在是一件很复杂的事情。
