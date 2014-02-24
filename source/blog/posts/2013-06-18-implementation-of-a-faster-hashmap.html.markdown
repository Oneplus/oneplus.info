---
layout: post
status: publish
published: true
title: 实现一个更快一点的hashmap
author: Oneplus
author_login: oneplus
author_email: oneplus.lau@gmail.com
author_url: http://blog.oneplus.info
excerpt: ! "这段时间在写parser，难免又碰到了特征映射的问题。去年毕设做分词、词性标注时，这部分是用__gnu_cxx::hash_map<string,int>来实现的。下表显示了几种数据集条件下的特征字典规模。\r\n<table
  width=\"100%\" border=\"1\">\r\n<tr><td>数据集</td><td>Ctb5</td><td>Ctb7</td><td>People’s
  Daily</td></tr>\r\n<tr><td>数据规模</td><td>1.8W sent.</td><td>4.7W sent.</td><td>18.4W
  sent.</td></tr>\r\n<tr><td>分词特征规模</td><td>203.1W</td><td>334.8W</td><td>774.9W</td></tr>\r\n<tr><td>词性标注特征规模</td><td>158.7W</td><td>274.2W</td><td>751.3W</td></tr>\r\n</table>\r\n\r\n"
wordpress_id: 786
wordpress_url: http://blog.oneplus.info/?p=786
date: 2013-06-18 21:54:02.000000000 +08:00
categories:
- 可以控制
- 算法才是正经事
- 挨踢民工
tags:
- C++
- hash_map
- algorithm
comments:
- id: 2995
  author: icycandy
  author_email: tgh728@gmail.com
  author_url: http://www.icycandy.com
  date: !binary |-
    MjAxMy0wNi0xOCAyMzoxNToyOSArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wNi0xOCAxNToxNToyOSArMDgwMA==
  content: 赞！
- id: 3002
  author: Darkgt
  author_email: darkgt@163.com
  author_url: http://www.darkgt.com
  date: !binary |-
    MjAxMy0wNi0xOSAxMToyNTowNCArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wNi0xOSAwMzoyNTowNCArMDgwMA==
  content: 赞!
- id: 3004
  author: debugcool
  author_email: debugcool@gmail.com
  author_url: http://www.debugcool.com
  date: !binary |-
    MjAxMy0wNi0xOSAxNzoyMzoxNiArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wNi0xOSAwOToyMzoxNiArMDgwMA==
  content: 虽但厉！
- id: 3067
  author: fandywang
  author_email: ofandywang@gmail.com
  author_url: http://weibo.com/lfwang
  date: !binary |-
    MjAxMy0wNy0wMiAyMzozMjowOSArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wNy0wMiAxNTozMjowOSArMDgwMA==
  content: 听起来你的需求使用双数组trie解决挺合适的（内存占用可能会多些），不知道是否有尝试？
- id: 3165
  author: icek
  author_email: zhuxi910511@163.com
  author_url: http://icek.me
  date: !binary |-
    MjAxMy0wNy0yMSAxMzozNjozNSArMDgwMA==
  date_gmt: !binary |-
    MjAxMy0wNy0yMSAwNTozNjozNSArMDgwMA==
  content: 赞！！！
---

这段时间在写parser，难免又碰到了特征映射的问题。去年毕设做分词、词性标注时，这部分是用`__gnu_cxx::hash_map<string,int>`来实现的。下表显示了几种数据集条件下的特征字典规模。

<table width="100%" border="1">
<tr><td>数据集</td><td>Ctb5</td><td>Ctb7</td><td>People’s Daily</td></tr>
<tr><td>数据规模</td><td>1.8W sent.</td><td>4.7W sent.</td><td>18.4W sent.</td></tr>
<tr><td>分词特征规模</td><td>203.1W</td><td>334.8W</td><td>774.9W</td></tr>
<tr><td>词性标注特征规模</td><td>158.7W</td><td>274.2W</td><td>751.3W</td></tr>
</table>

对于这个级别的数据量，在特征检索过程中，特征字典的性能已经对于整个分析器的性能产生了影响。不过，分词词性标注都是序列模型，对于序列中的每个元素，只要相应进行一次抽取就可以，特征字典的性能提高一点或者降低一点，对于整体速度的影响并不是非常明显。

不过在parser中，特征检索的情况就有所不同了。
主要表现就是作为一种结构学习，parser在学习模型参数以及预测过程中，需要对序列中的每两个元素抽取特征。
假如我们有30种特征模板，30词的句子，放到词性标注任务中，需要进行`30*30=900`次特征检索，而放到依存句法分析中，就需要进行`30*30*30=27000`次特征检索。
所以如果特征字典能再快点，当然是好事情。

另外一件让我比较不爽的事情是，c++的`hash_map`没法很好地支持持久化。
我想把`hash_map`当成整段内存dump到磁盘上，没可能。
只能一个key-value，一个key-value地处理。
所以呢，最理想的是有这样一种`hash map`

* 是一种动态的词典
* 以string或者const char * 作为key
* 性能与`__gnu_cxx::hash_map`相近，或者更胜一筹
* 能够很方便地进行持久化
* 不需要考虑删除操作


### 数据持久化

进一步分析，要对数据进行持久化，最好的办法就是把所有的数据都放到一段内存上，dump的时候，直接把这段内存写到磁盘上；load时，直接从磁盘中读一段内存。
池子一下子变成了一个超级好的选择。
stl中的string基本没法持久化，不用想了。
`const char *`倒是不错。我们可以把所有的key都固化到一段`char *`的buffer中。

对于value的固化，其实有这样一种考虑：如果value的类型是可以固化的，比如说int、double，那么也可以用池子来存这些value，但是如果是一些自建类型，比如说类啊什么的，本来就没有很直接的持久化的方法，小店也就只能伺候不周了。

池子固然是好想法，但我们考虑数据结构的动态性还要大于其性能考虑。
想让池子变得动态基本就要用到stl中的allocator的技术了。
维护一个池子长度上限以及当前长度，如果新加入的元素的规模大于池子上限，就将上限翻倍，重新给池子分配一段空间，把旧空间拷贝过去。

这样的话，数据固化的问题基本可以沿着这个思路解决。简单的代码可以写成这样

~~~cpp
if (pool_cap <= (new_size=(pool_size+element_size))) {
	pool_cap=((new_size)<<1);
	Element_type * new_pool = new Element_type[pool_cap];
	std::copy(pool, pool + pool_size, new_pool);
	delete [](pool);
	pool = new_pool;
}
~~~

### 性能优化

虽然hashmap中hash function是很大程度上影响性能的因素，但是这也是我们不能控制的事情。
我们能够提供的大概只有给一个合理的hashtable大小，以使得碰撞不是非常剧烈。
什么样的hashtable大小比较合适，开大了浪费，开小了碰撞又多，看来又要上动态的hashtable了。
不过即便是动态的hashtable，也面临resize时机的问题，爆栈上有这样一个问题“<a href="http://stackoverflow.com/questions/1603712/when-should-i-do-rehashing-of-entire-hash-table/1604428#1604428">When should I do rehashing of entire hash table?</a>”，第一条答案给了一个经验性的回答，翻译整理一下：
<blockquote>首先需要明确一个量load factor的概念，这个值表示hashtable的桶的个数M和桶中元素的个数N的比值，load factor=N/M。然后看一看你所使用的hashtable的类型有关（关于load factor和hashtable类型都可以去看侯捷老师的stl源码分析的5.7.1节）。
<ul><li>线性探测（linear probing）：load factor在60%左右时就该resize了</li>
<li>二次探测（quadratic probing）：load factor在80%-85%时就该resize了</li>
<li>开链（separate chaining）：load factor大于150%时就该resize了</li>
</ul>
</blockquote>


然后，我们还会面临一个问题，就是resize到多大呢？
二倍当然是一个选择，但不一定是好选择，比如说二次探测的hashtable需要hashtable大小为质数，二倍了就不是质数了。
比较好的选择是二倍以上的质数，这个<a href="http://planetmath.org/goodhashtableprimes">网址</a>给出了一个hashtable size的质数表。
后来我发现stl中也有一样的质数表。

具体实现resize的时机是在hashmap每次insert一个元素之后，看一看是不是符合resize的机制。
如果符合，申请一段新的hashtable，然后枚举旧的hashtable中的每个元素，把他们插入到新的hashtable中。

好的，到这里我们基本对于hashtable的实现心里也有数了。
不过做出来的可能也只是hash_map的一个翻版，如何在性能上进一步提升呢？
之前有一次讨论中，陆子龙师兄说在构造hashmap时可以将高频的key有限插入hashtable，这样从概率的角度讲，高频的key就有更多更大可能性一次就被检索到。
这或许是一个优化的好思路，而且貌似gnu.trove已经实现了这种机制。

为了实现这一机制，用开链的方式显得要比其他几种容易。
比方说保证高频key靠前，就只要保证在插入元素的时候维护链的有序性。
因为每个链中都不会有很多元素，所以直接用类似于交换排序的思想就好了。
维护有序性的时机主要是在某个key被重复插入后，这个key的频率增加，只要看一看这个key在链表中的前一个key是不是已经小于这个key了，如果是，就往前交换就好了。
因为每个链都比较小，而且在频率增加前这个链是有序的，所以可以在极小时间复杂度内求出算某个key的正确位置时。

到这里基本上整个数据结构的设计就出来了。Hash node设计成

~~~cpp
struct hash_node_t {
public:
  unsigned int __key_off; // 存key在key_pool中的偏移量
  unsigned int __val_off; // 存value在value_pool中的偏移量
  unsigned int __freq; // 存频次
  unsigned int __hash_val; // 存hashvalue，用于加速
  int __next_off; // 存后继节点在node_pool中的偏移量
};
~~~


因为池子的地址会动态变化，不能直接在hash node中保存指针，存偏移量就没有问题了。

一共有三个pool，一个存key，一个存value，一个存hash node，另外一个指针数组（或者偏移量数组）存hashtable的头结点，就设计成如下图那样了。

<a href="http://blog.oneplus.info/wp-content/uploads/2013/06/structure.jpg"><img src="http://blog.oneplus.info/wp-content/uploads/2013/06/structure.jpg" alt="Hash Table的数据结构" title="structure" width="500" class="aligncenter size-full wp-image-805" /></a>
我实现的代码放在<a href="https://github.com/Oneplus/libutilities/blob/master/src/smartmap/smartmap.hpp">这里</a>

### 测试

为了证明这个hashmap的性能，我进行了一个简单的benchmark。数据完全是模拟现实情境中首先构造特征字典，然后进行特征检索。benchmark的方法参考了<a href="incise.org/hash-table-benchmarks.html">这篇博客</a>中的方法。评价的大体过程是首先用一个有重复元素的key字典构建字典，然后用一个比较大规模的key集合去检索他的value。评价中采用了三个数据集，分别是ctb5，ctb6的分词特征集，和cdt的一阶句法特征集。key集是构造特征空间时用到的key，retrieve集是全特征集。各个数据的统计如下表所示

<table width="100%" border="1">
<tr><td>data set</td><td># of keys</td><td># of unique keys</td><td># retrieve entries</td></tr>
<tr><td>CTB5</td><td>12.89M</td><td>2.2M</td><td>77.3M</td></tr>
<tr><td>CTB6</td><td>16.91M</td><td>2.7M</td><td>101.5M</td></tr>
<tr><td>CDT</td><td>55.6M</td><td>5.2M</td><td>198.9M</td></tr>
</table>

参与对比的hashmap有__gnu_cxx::hash_map，google_sparse_hash，google_dense_hash，几种hashtable都做了类似的封装。benchmark用到的代码地址在<a href="https://github.com/Oneplus/libutilities/tree/master/benchmark/smartmap">这里</a>。运行的时候用

~~~
nice -n-20 ionice -c1 -n0 python bench.py
~~~

保证了进程的优先级。


实验在xeon5650 2.67GHz的服务器上进行，gcc版本是比较老的4.1.2。

在实验数据集上，时间效率和内存效率分别如下表显示。

<a href="http://blog.oneplus.info/wp-content/uploads/2013/06/speed.png"><img src="http://blog.oneplus.info/wp-content/uploads/2013/06/speed.png" alt="" title="speed benchmark" width="500"  class="aligncenter size-full wp-image-810" /></a>

<a href="http://blog.oneplus.info/wp-content/uploads/2013/06/memory.png"><img src="http://blog.oneplus.info/wp-content/uploads/2013/06/memory.png" alt="" title="memory benchmark" width="500" class="aligncenter size-full wp-image-811" /></a>

总体上来讲是达到了我的期望。下一步打算把这个模块并入LTP中，期望还能再进一步优化！

### 参考资料
<ul>
<li><a href="http://book.douban.com/subject/1110934/">STL源码分析</a></li>
<li><a href="http://stackoverflow.com/questions/1603712/when-should-i-do-rehashing-of-entire-hash-table/1604428#1604428">When should I do rehashing of entire hash table?</a></li>
<li><a href="http://incise.org/hash-table-benchmarks.html">Hash Table Benchmarks </a></li>
</ul>

话说好久没写博客了。
