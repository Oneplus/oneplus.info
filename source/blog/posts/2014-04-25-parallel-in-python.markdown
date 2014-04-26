---
layout: post
title: Parallel and HPC with Python (or numpy)
author: Oneplus
published: true
---

For guys working with natural language processing problems, it's daily task to process
tons of data. To handle the millions of lines of sentences, I would prefer C/C++ or
Java in the past, especially at certain scenario like performing machine learning algorithm
onto the data. However, in this days, I wrote a very slow python program (and working around
`numpy`, it's an important clue for future story). After wasting too much time on this single
thread program, I decided to parallel it.

### Buzz in the task

Let me briefly introduce my task (It's usually important for choosing the appropriate
parallel model). I have a collection of data which contains about 200 thousand entries.
My algorithm is some kind of `loop-loop` and can be illustrated as the following pseudocode.

~~~ python
while not terminal-condition:
    init(global_vector)
    for instance in instances:
        global_vector += time-consuming-process(instance)
    do-something(global_vector)
~~~

Since the `time-consuming-process` is very time consuming, we can easily use a `producer`
to distribute these tasks onto several `consumers`. What a textbook parallel model! To
make it more clear, also for convenience of future discussion, let me put it into some
meaningless but runnable code.

~~~ python
#!/usr/bin/env python
import numpy as np
import time

nr_instances = 2000
nr_dim = 257241

def do_something(vector):
    pass

def consumer():
    for _ in xrange(3):                 # use to simulate the time consuming
        x = np.random.rand(nr_dim)      # numpy array operation.
    ret = np.zeros(nr_dim)
    ret[np.random.randint(0, nr_dim, 20)] += np.random.rand(20)
    return ret

def producer():
    global_vector = np.zeros(nr_dim)
    instances = range(nr_instances)
    for index, instance in enumerate(instances):
        global_vector += consumer()
    do_something(global_vector)

if __name__=="__main__":
    for i in xrange(5):
        producer()
        print "iter %d is done." % i
~~~

A simple `time` command shows the above code runs `1m29.155s` on my server.

### Threading

As I mentioned before, I decide to paralled the above code. First thing that came into
my mind is the __threading__. According to my past experience, multi-threaded programming
is always the best choice when you have a server with several cores.

Distributing the producer's to several thread can be painless done with python `threading`
module. The producer's job is dividing the instances into several groups, feed them to each
of the thread and wait all these threads finish their work. A wrapper for the consumer is
implemented for recieveing data and invoke meta-consumer process.

After a slight modification on the above program, it became the multi-threaded version.

~~~
#!/usr/bin/env python
import numpy as np
import time
import threading
from basic import consumer, do_something, nr_instances, nr_dim

nr_threads = 4

def consumer_wrapper(instances, results, index):
    global_vector= np.zeros(nr_dim)
    for instance in instances:
        global_vector += consumer()
    results[index] = global_vector

def producer():
    global_vector = np.zeros(nr_dim)
    instances = range(nr_instances)
    threads = [None] * nr_threads
    results = [None] * nr_threads
    fence = nr_instances / nr_threads
    for i in xrange(nr_threads):
        chunk = instances[i*fence: (L if i+1==nr_instances else i*fence+fence)]
        threads[i] = threading.Thread(target=consumer_wrapper, args=(chunk, results, i))
        threads[i].start()
    for i in xrange(nr_threads):
        threads[i].join()
    global_vector = sum(results)
    do_something(global_vector)

if __name__=="__main__":
    for i in xrange(5):
        producer()
        print "iter %d is done." % i
~~~

I was expecting that the multi-threaded version will bring 2 to 3 times speed up if I
config the program with 4 threads. However, this code run `1m33.678s` on the same server.
I can't even believe that a multi-threaded program runs slower than the single-threaded
program.

After a survey on this issue, I found the answer. It suffer from the Python GIL which
prevent the script running on two cores. There are lots of article talking about the
GIL problems, so I won't write more on this. The conclusion is that _multi-threaded in
Python doesn't work for my task_.

### Multiprocessing

The failure of multi-threaded program drive me to seek for some alternative and I found
the `multiprocessing` module. At the begining of its document page, it says,

> _effectively side-stepping the Global Interpreter Lock by using subprocesses instead of threads_

To my understanding, its mechanism is treating the each thread as a process. When creating
a thread, it actually copy(fork) the entire processing into a new process. 

~~~
#!/usr/bin/env python
import numpy as np
import time
from multiprocessing import Pool
from basic import consumer, do_something, nr_dim, nr_instances

nr_threads = 4

def consumer_wrapper(instances):
    global_vector= np.zeros(nr_dim)
    for instance in instances:
        global_vector += consumer()
    return global_vector

def producer():
    instances = range(nr_instances)
    pool = Pool(processes = nr_threads)
    L = len(instances)
    fence = nr_instances / nr_threads
    arguments = [(instances[i*fence:(L if i+1==nr_threads else (i+1)*fence)]) \
            for i in xrange(nr_threads)]

    global_vector = sum(pool.map(consumer_wrapper, arguments))
    pool.close()
    pool.join()
    do_something(global_vector)

if __name__=="__main__":
    for i in xrange(5):
        producer()
        print "iter %d fin" % i
~~~
It takes `0m33.970s` for the multiprocessing version to run.

### MPI

### Summary


