---
layout: post
title: CRF Benchmark Test
author: Oneplus
tags:
    - CRF
    - Benchmark
published: false
---

When you decided to model your sequence data with Conditional Random Fields (CRF),
a branch of CRF toolkits is presented to you. As the old saying

> Equip yourself with the most powerful weapon to battle against the-state-of-the-art!

So I conduct several benchmarks on the CRF toolkits to find out the (maybe most)
powerful weapon :-)

Actually, In [crfsuite](http://www.chokkan.org/index.html.en)'s home page, there is
a fairly good [benchmark](http://www.chokkan.org/software/crfsuite/benchmark.html),
However, there are also some minor mistakes and something needs to be updated.
In this blog, I am trying to describe my benchmark result on different implementations
of CRF, precisely speaking, the linear-chained CRF.

### Things to keep in mind

To evaluate different toolkits, basic concepts for CRF should be seriously studied.
However, this blog doesn't aim to explain these concepts. For some serious introduction,
readers can refer to the [supplement resources](#supplement-resources) section. In this
blog, several things reader needs to keep in mind are listed below.

* Three things we care in this blog is the accuracy, training speed and expansibility of
linear-chained CRF toolkits.
* If we model the sequence data in different ways, we may observe different results and
different time.
* 
