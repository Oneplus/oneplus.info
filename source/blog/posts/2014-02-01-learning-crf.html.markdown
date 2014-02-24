---
title: Linear-chained CRF 学习笔记
layout: post
published: false
author: Oneplus
---

这篇会简要整理linear-chained CRF的模型，求边缘概率的前向后向过程，使用SGD进行参数估计。

### CRF的基本知识

对于CRF的基础知识，有很多资料介绍。不同的资料往往出发点又有不同。
个人感觉，Andrew McCallum的Tutorial大概是介绍得最清楚的一篇。
我想，比起把前人的东西重写或者编译一遍即浪费体力，又可能由于写得不清楚导致新的误解。
所以，需要了解基础知识

但是，
到这篇的最后，

### 对序列数据建模

词性标注、分词等等问题都可以认为是对序列问题进行建模。
下面这个词性标注的例子将作为例子贯穿全篇。

* 训练实例：(\[N V N\], \[cat chase dog\])
* 特征模板：$ 0=word_i $
* 特征空间：$ \mathcal{F} $
~~~
F = {
    0 => 'cat-N',   1 => 'cat-V',
    2 => 'chase-N', 3 => 'chase-V',
    4 => 'dog-N',   5 => 'dog-V',
    6 => 'N-N',     7 => 'N-V',
    8 => 'V-N',     9 => 'V-V',
}
~~~

### The Model

$ p(y|x) = \frac{1}{Z} \exp{ \sum_{k=1}^K{ \lambda_k f_k ( y_t, y\_{t-1}, x_t ) } }$

带入上面的例子，就是

$$
\begin{array}{ll}
    p([N V N]|['cat', 'chase', 'dog']) & = \frac{1}{Z} \exp{ \sum_{k=1;y=[N V N]}^K{ \lambda_k f_k (y_t, y\_{t-1}, x_t}) } \cr
    & = \frac{1}{Z} \exp \{ \sum\_{k=1}^K{ \lambda\_k f\_k(N, nil, 'cat') } + \sum\_{k=1}^K { \lambda\_k f\_k(V, N, 'chase')} + \sum\_{k=1}^K { \lambda\_k f\_k(N, V, 'dog') } \}
\end{array}
$$

对于第一个分量，只有特征空间中的第0维有值，同理第二个分量有值的是3、7两维，第三个分量是4、8两维。
那么，上式可以写成

$$
\begin{array}{ll}
    p([N V N]|['cat', 'chase', 'dog']) = & \frac{1}{Z} \exp ( \lambda\_0 f\_0(N, nil, 'cat') \cr
    & + \lambda\_3 f\_3(V, N, 'chase') + \lambda\_7 f\_7(V, N, 'chase') \cr
    & + \lambda\_4 f\_4(N, V, 'dog') + \lambda\_8 f\_8(N, V, 'dog') )
\end{array}
$$

这里有一个需要注意的地方就是上面的连加式可以写成乘积的形式。

### 似然函数

假设我们有N个训练实例，似然就是把模型给出的每个实例的概率乘起来。
如果再取个对数，就变成连加的形式了。

$$
\begin{array}{ll}
    \mathcal{L}(\theta) & = \log{ \prod\_{i=1}^N p( y^{(i)} | x^{(i)} ) } \cr
    & = \sum\_{i=1}^N {\log{ p(y^{(i)} | x^{(i)} }) } \cr
    & = \sum\_{i=1}^N \sum\_{t=1}^T \sum\_{k=1}^K{ \lambda_k f_k (y_t^{(i)}, y\_{t-1}^{(i)}, x_t^{(i)}) } - \sum\_{i=1}^N \log{ Z(x^{(i)}) }
\end{array}
$$

为了人为地加入一些对于参数的限制，我们可以在似然函数中加入正则项。
如果采用L2正则，上面的似然函数就变成了

$$
\mathcal{L}(\theta) = \sum\_{i=1}^N \sum\_{t=1}^T \sum\_{k=1}^K{ \lambda\_k f\_k (y\_t^{(i)}, y\_{t-1}^{(i)}, x\_t^{(i)}) } - \sum\_{i=1}^N \log{ Z(x^{(i)}) } - \sum\_{k=1}^K \frac{ \lambda_k^{2} }{ 2 \sigma^{2} }
$$

其中，$\sigma$ 是一个人为可调的参数。

上式的导数是

$$
\frac{\partial \mathcal{L}}{\partial \lambda\_k} = \sum\_{i=1}^N \sum\_{t=1}^T { f\_k (y\_t^{(i)}, y\_{t-1}^{(i)}, x\_t^{(i)}) } - \sum\_{i=1}^N \sum\_{t=1}^T \sum\_{y,y'} { f\_k (y, y', x\_t^{(i)}) p(y,y'|x\_t^{(i)}) } - \frac{ \lambda\_k }{ \sigma^{2} }
$$

之后，需要做的是最优化题了。

### 优化

根据andrew mccallum的那篇tutorial，这个似然没有解析解，所以要用数值方法解。
不管是用bfgs还是sgd，
我们都需要求$\mathcal{L}$和$\frac{\partial \mathcal{L}}{\partial \lambda\_k}$。

接下来首先举例说明$Z=\sum\_y \exp{ \sum\_{k=1}^K \lambda_k f_k(y_t,y\_{t-1}, x)}$

沿用之前的例子，把他带入Z，展开可得到
$$
\begin{array}{llll}
    Z = & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, nil, 'cat')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, N, 'chase')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, N, 'dog')} \cr
    & + \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, nil, 'cat')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, N, 'chase')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, N, 'dog')} \cr
    & + \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, nil, 'cat')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, N, 'chase')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, V, 'dog')} \cr
    & + \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, nil, 'cat')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, N, 'chase')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, V, 'dog')} \cr
    & + \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, nil, 'cat')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, V, 'chase')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, N, 'dog')} \cr
    & + \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, nil, 'cat')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, V, 'chase')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, N, 'dog')} \cr
    & + \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, nil, 'cat')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, V, 'chase')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(N, V, 'dog')} \cr
    & + \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, nil, 'cat')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, V, 'chase')} & \exp{ \sum\_{k=1}^K \lambda\_k f\_k(V, V, 'dog')}
\end{array}
$$

如果只保留$f_k=1$的项，那么

$$
\begin{array}{llll}
    Z =& \exp{ \lambda_0} & \exp{ \lambda_2+\lambda_6} & \exp{ \lambda_4+\lambda_6}\ - (1) \cr
    &+\exp{ \lambda_0} & \exp{ \lambda_2+\lambda_6} & \exp{ \lambda_5+\lambda_7}\ - (2)\cr
    &+\exp{ \lambda_0} & \exp{ \lambda_3+\lambda_7} & \exp{ \lambda_4+\lambda_8}\ - (3)\cr
    &+\exp{ \lambda_0} & \exp{ \lambda_3+\lambda_7} & \exp{ \lambda_5+\lambda_9}\ - (4)\cr
    &+\exp{ \lambda_1} & \exp{ \lambda_2+\lambda_8} & \exp{ \lambda_4+\lambda_6}\ - (5)\cr
    &+\exp{ \lambda_1} & \exp{ \lambda_2+\lambda_8} & \exp{ \lambda_5+\lambda_7}\ - (6)\cr
    &+\exp{ \lambda_1} & \exp{ \lambda_3+\lambda_9} & \exp{ \lambda_4+\lambda_8}\ - (7)\cr
    &+\exp{ \lambda_1} & \exp{ \lambda_3+\lambda_9} & \exp{ \lambda_5+\lambda_9}\ - (8)
\end{array}
$$

上式很容易看出重复子结构，可以用动态规划来解。

令$a[i,j] = \log \exp \sum\_{y \in y[0:i]} \sum\_k \lambda\_k f\_k(y\_t, y\_{t-1}, x)$。
带入上面的例子举例就是

* $a[0,0] = \log \exp \lambda\_0$
* $a[1,1] = \log (\exp {(\lambda\_1 + \lambda\_3 + \lambda\_7)} + \exp {(\lambda\_1 + \lambda\_3 + \lambda\_9)}) $
* ...

状态转移方程可以写成

$$\exp a[i,y'] = \sum\_y \exp (a[i-1,y] + \sum\_k \lambda\_k f(y, y', x\_i))$$

再说如何求$p(y,y'|x)$。经验性地讲，求$p(y,y'|x)$的工作是在上面的对Z的展开中把某个分量固定(比如 $\exp{ \lambda\_2+\lambda\_6}$)，其他求和。
很幸运的是，在刚才求状态转移方程的过程中，被固定的分量的之前的和已经被算出来了。
而后面的和也可以用类似的方法求得。

这两个求和的过程被叫做前向-后向过程(forward-backward)。

写出后向过程的状态转移是

$$\exp b[i,y'] = \sum\_y \exp (b[i+1,y] + \sum\_k \lambda\_k f(y, y', x\_i))$$

有了$a$和$b$，$p(y,y'|x) = \frac{1}{Z} \exp(a[i-1,y]) \exp(\sum\_k \lambda\_k f(y,y',x\_i)) \exp(b[i,y'])$

### lbfgs

有了目标函数和目标函数的导数，比较直接容易想到的是用bfgs来解。
lbfgs的库有很多，所以在实现时可以直接把优化算法当黑盒来用。

`scipy.optimize`模块里面有fmin\_l\_bfgs\_b，直接把负似然和似然的负导数喂给这个函数就可以获得优化解了。

~~~python 
w, f, d = optimize.fmin_lbfgs_b(likelihood,
                                w,
                                fprime = dlikelihood)
~~~

### sgd

有了目标函数的导数，用sgd优化就变得很容易。

#### 梯度验证

梯度验证主要是检验梯度求得是否正确。
主要思想是对于某点$w$，在它的梯度方向上前进一小步，得到$w'=w+\delta$。
然后验证目标函数在$w$和$w'$之间的距离是否近似等于$\nabla\_w \delta$

这部分其实和CRF的关系不大，不过比较实用。

#### 正则项

正则项的意义这里不需要说了。
主要说如何

### 一些问题

* 因子图(Factor Graph)，势函数($\Phi$)
* CRF与MEMM的关系
* 优化似然与最大化熵

### 参考资料

* [Conditional random fields: Probabilistic models for segmenting and labeling sequence data]()
* [An Introduction to Conditional Random Fields for Relational Learning]()
* [Stochastic Gradient Descent Tricks]()
