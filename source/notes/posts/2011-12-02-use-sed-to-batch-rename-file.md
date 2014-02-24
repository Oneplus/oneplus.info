---
layout: note
title: "使用sed批量改文件名"
tags: ["Shell"]
---
### Sed批量去拓展名

~~~bash
|- dev.gb.conll06.raw
|- test.gb.conll06.raw
|- train.gb.conll06.raw
~~~

想要去掉其中的后缀`.raw`，用个小脚本就可以搞定：

~~~bash
for file in `ls`; do mv $file `echo $file | sed 's/\.raw$//'`; done
~~~

### Sed批量添加拓展名

~~~bash
|- dev.gb.conll06
|- test.gb.conll06
|- train.gb.conll06
~~~

同理，一个小脚本可以搞定：

~~~bash
for file in `ls`; do mv $file `echo $file | sed 's/$/\.raw//'`; done
~~~
