---
layout: post
status: publish
published: true
title: 最大熵模型的简单实现
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "谈到最大熵，真的是一个妇孺皆知老少咸宜的好模型。而且，网上确实已有大批量的论文、笔记、幻灯片介绍最大熵。所以，这篇的重点放在如何实现一个简单的最大熵分类器上。\r\n"
wordpress_id: 671
wordpress_url: http://blog.oneplus.info/?p=671
date: 2012-07-22 21:58:16.000000000 +08:00
categories:
- 可以控制
- 热爱科学好少年
tags:
- 机器学习
- 最大熵
- maxent
comments:
- id: 865
  author: icek
  author_email: zhuxi910511@163.com
  author_url: http://icek.me
  date: !binary |-
    MjAxMi0wNy0yNyAwODozODoxMiArMDgwMA==
  date_gmt: !binary |-
    MjAxMi0wNy0yNyAwMDozODoxMiArMDgwMA==
  content: 好东西阿！顺便问一下文章里的公式是怎么搞的？
- id: 866
  author: Oneplus
  author_email: oneplus.lau@gmail.com
  author_url: http://blog.oneplus.info
  date: !binary |-
    MjAxMi0wNy0yNyAwODo1MzozMSArMDgwMA==
  date_gmt: !binary |-
    MjAxMi0wNy0yNyAwMDo1MzozMiArMDgwMA==
  content: 公式是用latex for wordpress这个插件写的。
- id: 877
  author: luyi0619
  author_email: luyi0619@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMi0wOC0yNiAwMDowOToxOCArMDgwMA==
  date_gmt: !binary |-
    MjAxMi0wOC0yNSAxNjowOToxOCArMDgwMA==
  content: 和学长比感觉自己什么都不会呢。。
- id: 880
  author: Darkgt
  author_email: darkgt@163.com
  author_url: http://www.darkgt.com
  date: !binary |-
    MjAxMi0wOC0yOCAyMDo0Njo1NyArMDgwMA==
  date_gmt: !binary |-
    MjAxMi0wOC0yOCAxMjo0Njo1NyArMDgwMA==
  content: 每次看都能学到新东西，真不错
- id: 2165
  author: DX
  author_email: qdxzzz@gmail.com
  author_url: ''
  date: !binary |-
    MjAxMy0wMy0xMiAxMTo0MzozNiArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wMy0xMiAwMzo0MzozNiArMDgwMA==
  content: ! "lz写的很简洁明了，很有帮助。\r\n有个地方有点疑问，模型期望背后的直觉解释是啥？lz写模型期望如何计算的那一段\r\n“模型期望需要首先求p(y|x)。这个条件概率可以通过简单地将所有(x,y)符合的fi和对应的参数λi乘起来后相加。归一化因子是各个Outcome
    y的p(y|x)的和。在求得p(y|x)后，要求Eq(fi)，只需要枚举所有符合fi的(x,y)对应的p(y|x)，乘以Context x出现的次数再除以N就可以。\r\n”\r\n没太看明白。能写个公式吗？\\lambda_i一开始的时候如果初始化为0，那么p(y|x)开始的时候就是0了？"
- id: 3068
  author: fandywang
  author_email: ofandywang@gmail.com
  author_url: http://weibo.com/lfwang
  date: !binary |-
    MjAxMy0wNy0wMiAyMzo1MToyNyArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wNy0wMiAxNTo1MToyNyArMDgwMA==
  content: 写得挺好的，简洁清楚，不过，推倒过程还是需要看论文。
- id: 3113
  author: fandywang
  author_email: ofandywang@gmail.com
  author_url: http://weibo.com/lfwang
  date: !binary |-
    MjAxMy0wNy0wOSAyMjowNDoyNyArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wNy0wOSAxNDowNDoyNyArMDgwMA==
  content: 最近也实现了一个，欢迎oneplus 帮忙 review  https://github.com/fandywang/mltk
- id: 4109
  author: cr7
  author_email: dlut200803001@163.com
  author_url: ''
  date: !binary |-
    MjAxMy0xMi0wMSAxNjo1MjoxNiArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0xMi0wMSAwODo1MjoxNiArMDgwMA==
  content: 同问，为什么要通过期望相等来建立约束。
- id: 4213
  author: yeky
  author_email: yekangyin@hotmail.com
  author_url: ''
  date: !binary |-
    MjAxMy0xMi0xMSAxNDowNzoyNCArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0xMi0xMSAwNjowNzoyNCArMDgwMA==
  content: 期望相等这个约束相当于求极大似然估计。在Maxent中，其实有两个优化方向，一个是最大熵方向（即对未知信息尽量均匀分布），另一个就是极大似然方向（让模型尽量与样本吻合）。而一般的模型只有后一个优化方向。
- id: 4519
  author: Huo
  author_email: hhrhakuna@163.com
  author_url: ''
  date: !binary |-
    MjAxNC0wMS0xNiAyMjozMzozMCArMDgwMA==
  date_gmt: !binary |-
    MjAxNC0wMS0xNiAxNDozMzozMCArMDgwMA==
  content: 你300行的Python源码能供学习一下吗？
---
谈到最大熵，真的是一个妇孺皆知老少咸宜的好模型。
而且，网上确实已有大批量的论文、笔记、幻灯片介绍最大熵。
所以，这篇的重点放在如何实现一个简单的最大熵分类器上。

### 最大熵模型推导

机器学习的任务是从数据中学习知识。
我们做分类问题，看到的数据往往是每个实例对应一个类别。
比如说词性标注中一个词对应一个标注。
为了下面讨论的方便，将类别称为Outcome，将每个实例的上下文环境叫做Context。
实例被称为Event，一个实例是Outcome与Context的二元组。

为了表示数据，我们从数据中抽取了一系列的特征。特征的全体可以看做是n个特征函数组成的一个集合。每个特征函数可以是从Context到0-1的二值函数。比方说这样的

$$
f(x,y)=\{ \begin{aligned} 1 & if\ x="is"\ and\ y=v \\ 0 & otherwise \end{aligned}
$$

一组特征函数就将Context从上下文空间映射到特征空间上了。

现在，我们观察到一组数据集，通过简单的统计可以知道任意一个Context x和Outcome y的组合的联合概率。有了联合概率，可以计算观察到的某一特征函数f的期望，也就是 $E\_{ref}(f)= \sum\_{x,y}{\tilde{p}(x,y)f(x,y)}$，称为观察期望/经验期望。

假设我们有一个模型给出p(y|x)的值，那么我们可以从这个模型的角度求出这个特征函数的期望，即$ E_q(f)=\sum\_{x,y}{\tilde{p}(x)p(y|x)f(x,y)}$，称为模型期望。

我们希望我们的模型能够很好地反应这些数据中蕴含的现象。那么从模型角度看到的f的期望就应该等于从数据观察到的f的期望。也就是$ E\_q(f)=E\_{ref}(f) $

假设我们有n个特征函数，那么我们就有n组等式$ E\_q(f\_i)=E\_{ref}(f\_i), i \in {1,2,...,n}$。

假设我们有那么那么多的模型，也可以认为是概率分布。他们组成一个空间$ \mathcal{P} $，而满足上面一系列特征函数期望构成的等式的概率分布构成了$ \mathcal{P}$的一个子集

$$
\mathcal{C}=\{p|p\in \mathcal{P} \quad and \ E_q(f_i)=E\_{ref}{f\_i},\ i \in (1,2,...,n)\}
$$

现在要找一个合适的模型描述数据，也就是在$ \mathcal{P} $中搜索一个p。
然后这时，熵突然出现了（- -b这里我也不知道怎么写，原谅我吧），从最大熵的角度来看，这个模型需要满足上面一系列特征函数期望构成的等式（换句话讲，是一些列一系列特征函数期望构成的约束），同时尽可能将可能性均匀地非配到不确定的上下文情况中。

对于一个模型p，它的熵的定义是这样$ H(p)=-\sum\_{x,y}\tilde{p}(x)p(y|x)\log{p(y|x)}$。
熵越大，可能性就越平均地被分配，因而我们的最终目标是最大化一个模型的熵。
而由于有前面的约束等式，这个问题变成了一个有约束的最优化问题

$$
find p * = arg{max\_{p\in C}{H(p)}}
$$

然后引入拉格朗日乘子$\lambda$，将等式约束的优化转换成无约束的最优化，得到

$$
\Lambda(p,\lambda)=H(p)+\lambda\sum_i(E_q(f_i)-E\_{ref}(f\_i))
$$

求导解p，得到一个与$\lambda$有关的函数

$$
p\_{\lambda}(y|x)=\frac{1}{Z\_{\lambda}(x)}\exp(\sum_i{\lambda_i f_i(x,y)})
$$

其中，$Z\_\lambda(x)=\sum_y{\exp(\sum_i \lambda_i f_i(x,y))}$ 。

将$p\_{\lambda}$带入无约束优化的式子中，得到

$$
\Psi(\lambda)=\Lambda(p,\lambda)=-\sum_x\tilde{p}\log{Z\_\lambda(x)}+\sum_i{\lambda_i E\_{ref}(f_i)}
$$

推导到这里，我们基本得到了算法要做的工作，就是从数据中估计出一个特征函数的权向量$\lambda$。最大化$ \Psi(\lambda) $。

注意：
<ul>
<li>$\Psi(\lambda)$等于经验分布的最大似然估计，也就是$\Psi(\lambda)=L_p(\Lambda)$</li>
<li>上面的求导过程被忽略了</li>
<li>为什么最大化$\Psi(\lambda)$是正确的，这里涉及到原问题和对偶问题，还有KTT条件。我觉得应该是写不明白，所以直接跳过，不影响我们实现最大熵模型。</li></ul>

### 最大熵模型的实现

要算$ \lambda $，解析解肯定是行不通的。对于最大熵模型对应的最优化问题，GIS，lbfgs，sgd等等最优化算法都能解。相比之下，GIS大概是最好实现的。算法的流程如下：


<ol>
<li>初始化$ \lambda=0$</li>
<li>循环$ \lambda_i^{(t+1)}=\lambda_i^{(t)}+\frac{1}{C}\log{\frac{E_{ref}(f_i)}{E_q(f_i)}} $</li>
<li>重复2到收敛</li>
</ol>
其中，$ C=\max\_{x,y}\sum\_{i=1}^n{f\_i(x,y)} $。


根据上面算法，在最大熵模型的实现过程中，我们需要计算的值包括经验期望$E\_{ref}(f)$和各轮迭代过后的模型期望$E\_q(f)$。

经验期望$ E\_{ref}(f_i)= \sum\_{x,y}{\tilde{p}(x,y)f_i(x,y)} $，求$ E\_{ref}(f_i)$只需要统计训练数据中符合$f_i$的(x,y)二元组的个数，然后除以训练实例的个数N。

模型期望需要首先求$p(y\|x)$。
这个条件概率可以通过简单地将所有(x,y)符合的$f_i$和对应的参数$\lambda_i$乘起来后相加。
归一化因子是各个Outcome y的$p(y\|x)$的和。在求得$p(y\|x)$后，要求$E_q(f_i)$，只需要枚举所有符合$f_i$的(x,y)对应的$p(y\|x)$，乘以Context x出现的次数再除以N就可以。

模型期望有了，经验期望有了，把他们一股脑儿放到算法里面去迭代就好了。

当然，到这里我们完全可以写出一个最大熵分类器。
不过，需要注意的一点，在上文也提到最大化$\Psi(\lambda)$实际是在做最大似然估计。
谈到最大似然估计，就不可避免想到了过拟合问题。
如果训练数据和测试数据的偏置比较大。
我们训练的模型很可能无法再测试数据上取得比较好的效果。
解决这一问题的一般套路是用给待估计的参数一个先验分布做MAP，这里也不例外。
如果假设$\lambda$服从Gauss分布，优化的目标函数就变成了$L\_{\tilde{p}}^{'}(\Lambda)=L_p(\Lambda)+\sum_i{\log{\frac{1}{\sqrt{2\pi\sigma_i^2}}}}-\frac{\lambda_i^2}{2\sigma_i^2}$

在使用高斯先验平滑模型后，GIS的更新变成解$ E\_{ref}(f_i)=E_q(f_i)e^{C\delta_i}+\frac{\lambda_i+\delta_i}{\sigma_i^2} $。
其中，$\lambda_i$是本轮迭代的参数，$\delta_i$是更新$\lambda_i$的增量。
上面的方程是没有解析解的，不过可以用牛顿法解除数值解。

### 补充

本来是想看一看lbfgs的，不过那个最优化的库实在是太复杂了，所以基本用的时候就当黑盒了。而且，从maxent的代码来看，其用法和GIS类似，都需要做求$ E_{ref}(f_i)$和$E_q(f_i)$的工作。

在了解了最大熵模型的一些实现细节后，我们就可以动手去实现一个最大熵分类器了。我用python写了一个GIS+binary feature版的maxent，去掉读写模型文件等外围模块，大概300行多一点。总体来讲是非常容易的。同时推荐阅读一下张乐的maxent toolkit，个人感觉写得非常好。

### 参考


<ul>
<li><a href="http://www.isi.edu/natural-language/people/ravichan/papers/bergeretal96.pdf">A Maximum Entropy Approach to Natural Language Processing</a> 个人感觉应该是最大熵必看的一篇论文。</li>
<li><a href="http://users.cms.caltech.edu/~weixl/research/read/summary/MaxEnt2.ppt">最大熵模型与自然语言处理</a> 感觉这个slide应该是基于上一篇做的，配合着看应该效果很好。</li>
<li><a href="http://work-tmp.googlecode.com/svn/trunk/maxent/10.1.1.123.127.pdf">The Improved Iterative Scaling Algorithm: A Gentle Introduction</a> 讲IIS为什么work</li>
<li><a href="http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.138.714&rep=rep1&type=pdf">Investigating GIS and Smoothing for Maximum Entropy Taggers</a> 如果要实现一个maxent，这篇也是非常非常推荐的，从最基本的GIS到加高斯先验，后面还有必要的证明。</li>
<li><a href="http://homepages.inf.ed.ac.uk/lzhang10/maxent_toolkit.html">Maximum Entropy Modeling Toolkit for Python and C++</a> 最大熵工具包，源码写得非常好看，无论从算法角度还是从软件工程角度。</li>
<li><a href="https://github.com/nicyun/easyME">easyME</a> nicyun等师兄实现的maxent toolkit的化简版，简单易懂。</li>
</ul>


