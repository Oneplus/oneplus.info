---
layout: note
title : "记一次修复MySQL数据库的经历"
categories: "Operation"
tags: ["Server", "MySQL"]
author: Oneplus
---

实验室服务器的硬盘满了，结果导致一个线上服务的MySQL数据库的两个表坏了。具体症状是`desc cdb_searchindex`显示

~~~bash
ERROR 1017 (HY000): Can't find file: 'cdb_searchindex' (errno: 2)
~~~

这是要通过/etc/my.cnf(或者同类的mysql配置文件)找到数据文件的位置。定位后进入文件夹，`ls cdb_searchindex*`一看，只剩一个cdb_searchindex.frm文件了。

接下来要进行恢复了。

第一步是确定这个表的引擎类型，命令是:

~~~ bash
show table status from `discuz`;
~~~

一看都是MyISAM，恢复起来就相对比较容易了。

第二步是在数据库文件所在的文件夹中新建`cdb_searchindex.MYD`和`cdb_searchindex.MYI`两个文件，注意权限应该是mysql的。

第三步是在mysql中用

~~~ bash
repair table cdb_searchindex USE_FRM;
~~~

就可以恢复了。

第四步用

~~~ bash
mysqlcheck discuz;
~~~

没啥问题就OK了。

### 参考

* [MYSQL数据文件--.frm文件(只有.frm文件时的表结构恢复)](http://myceo.blog.51cto.com/2340655/737216)
