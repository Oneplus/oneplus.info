---
layout: note
title: "Grep的若干小技巧"
categories: "Linux"
tags: ["Shell", "grep"]
---

***匹配不符合模式的字符串***

~~~bash
grep -v "pattern" file
~~~

***模板中含有\t***

~~~bash
grep -P "^\t" file
~~~

***两文件差集（B.txt-A.txt）***

~~~bash
grep -F -v -f A.txt B.txt
~~~

### 参考

* [Drew's grep tutorial](http://www.uccs.edu/~ahitchco/grep/)
* [LINUX Shell下求两个文件交集和差集的办法](http://blog.csdn.net/autofei/article/details/6579320)



