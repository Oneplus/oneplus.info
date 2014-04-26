---
layout: post
title: ibm model与词对齐
published: false
latex: true
author: Oneplus
---

### 定义

- 源语言，法语，$f$代表一句话
- 目标语言，英语，$e$也代表一句话
- $f_i$，$e_j$，代表这句中的一个词
- 在统计机器翻译系统中，我们有一系列平行文本$(f^k,e^k),k=1,...,n$。

### 机器翻译

> 给定源语言$f$，要找到最好的目标语言$e$作为翻译

上面这句话的一个建模是

<div>
$$ e^*= \arg\max_{e\in E} {p(e|f)} = \arg\max_{e\in E} {p(e) \times p(f|e)} $$
</div>

这个是典型的噪声信道模型。

在机器翻译问题中，我们要对下面这个概率进行建模

<div>
$$
p(f_1,..,f_m|e_1,...,e_l,m)
$$
</div>

这个概率的含义是：给定一个长度为l的英文句子，他被翻译成长度为m的法文句子的概率。
