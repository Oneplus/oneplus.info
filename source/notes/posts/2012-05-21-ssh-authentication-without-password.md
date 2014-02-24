---
layout: note
title: "用公共key实现无密码ssh"
categories: "Linux"
tags: ["ssh"]
---
在HPC上，从server登陆到各个node都需要输密码，很麻烦，能不能不输密码呢。

需要用到的技术就是ssh中public key的authorized。
具体做法分如下几步：

1. 用ssh-keygen生成一个publc key；

~~~bash
ssh-keygen -t rsa
~~~

中间会提醒输入id_rsa文件的位置和pass-phrase，可以一路回车。id_rsa在`~/.ssh/`中产生两个文件`id_rsa`和`id_rsa.pub`，一个是私有密钥，一个是公共密钥。

2. 由于HPC中共享硬盘，直接将其中的public key（一般默认为`~/.ssh/id_rsa.pub`）在复制一份并命名为authorized_keys

3. 如果运气好，做完第二步就可以实现不输入密码登陆了。不过实际实施过程中，还有很多种发生意外的可能（经亲身验证）。尤其需要注意的问题是各个文件/文件夹权限的问题。

合理的权限列表如下：

* id_rsa 600
* id_rsa.pub 644
* ~/.ssh/    755

同时要注意的就是，`$HOME`，也就是~不能是777的权限，在这个问题上卡了三四个小时啊。

