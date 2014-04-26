---
layout: note
title: "Grep的若干小技巧"
categories: "Linux"
tags: ["Shell", "grep"]
---

### 匹配不符合模式的字符串

~~~bash
grep -v "pattern" file
~~~

### 模板中含有\t

~~~bash
grep -P "^\t" file
~~~

### 两文件差集（B.txt-A.txt）

~~~bash
grep -F -v -f A.txt B.txt
~~~

### 用A.txt文件中的词表查B.txt

~~~
grep -f A.txt B.txt
~~~

与Pipe配合

~~~
cat B.txt | grep -f A.txt
~~~

还有

~~~
cat A.txt | grep -f - B.txt
~~~

### 参考

* [Drew's grep tutorial](http://www.uccs.edu/~ahitchco/grep/)
* [LINUX Shell下求两个文件交集和差集的办法](http://blog.csdn.net/autofei/article/details/6579320)
* [How to grep with a list of words](http://stackoverflow.com/questions/17863301/how-to-grep-with-a-list-of-words)


