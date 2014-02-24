---
layout: note
title : "Python 多线程同步队列模型"
categories: "Programming"
tags: ["Python", "Multi-threaded"]
author: Oneplus
---
我面临的问题是有个非常慢的处理逻辑（比如分词、句法），有大量的语料，想用多线程来处理。

这一个过程可以抽象成一个叫“同步队列”的模型。
具体来讲，有一个生产者（Dispatcher）一方面从语料中读入句子，并且存入队列中，一方面看有没有空闲的消费者（Segmentor），如果有，就把句子从队列中弹出并交给这个空闲的消费者处理。
然后消费者把处理完成的结果交给生产者输出，生产者要保证输出与输入顺序一致。

消费者是典型的threading，它需要看见生成者的队列，从而从队列中拿一些数据。

对于生产者，python中有一个叫Queue的module，实现了FIFO的同步队列。
但它只能保证输入与交付消费者的顺序的有序，但不能保障生产者在输出时有序，所以需要一个buffer来保存输出顺序。
程序的模型大概是这样的。有一个master()，用来分发任务。有N个多线程的slave用来处理任务。

具体程序如下：

~~~python
#!/usr/bin/env python
# real    3m0.263s
# user    0m0.016s
# sys     0m0.012s

from time import sleep
from random import random
from Queue import Queue
from threading import Thread, Lock

class Segmentor(Thread):
    def __init__(self, dispatcher):
        Thread.__init__(self)
        self.d = dispatcher

    def run(self):
        while True:
            idx, item = self.d.get()
            # segment section
            sleep(random() * 5)
            # output section
            d.output( idx, item )
            self.d.task_done()

class Dispatcher(Queue):
    def __init__(self):
        Queue.__init__(self)
        self.idx = 0
        self.box = {}
        self.lock = Lock()

    def output(self, idx, item):
        self.lock.acquire()
        if idx > self.idx:
            self.box[idx] = item
        elif idx == self.idx:
            self._output(item)
            self.idx += 1
            while self.idx in self.box:
                item = self.box[self.idx]
                self._output(item)
                self.idx += 1

        self.lock.release()

    def _output(self, item):
        print item

if __name__=="__main__":
    d = Dispatcher()
    for i in xrange(4):
        t = Segmentor(d)
        t.daemon = True
        t.start()

    num = 0
    for line in open("data", "r"):
        d.put( (num, line.strip()) )
        num += 1

    d.join()
~~~

在300句的条件下，单线程的处理速度约为750s=12m，开4个线程后3m可以处理完成，并且输出是有序的。

其他语言应该可以仿照这个方式编写程序，对于没有同步队列的语言，实现时可以参考这个http://hg.python.org/cpython/file/2.7/Lib/Queue.py


