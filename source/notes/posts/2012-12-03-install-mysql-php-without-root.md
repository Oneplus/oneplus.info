---
layout: note
title : "在没有Root权限的情况下安装Mysql和PHP"
categories: "Operation"
tags: ["Server", "MySQL", "PHP"]
---
前一阵子，larry学长在他的linode上给我开了一个账号，把oneplus.info搬运到了这里。
现在的服务器环境配置如下：

* ubuntu 12.04
* nginx 1.14

无Mysql、无PHP。
由于之前使用wordpress建站，不得不在没有root的情况下安装Mysql和PHP

首先，高版本MySQL使用CMake编译工具构建，构建之前需要安装CMake。
CMake的安装方法如下：

~~~bash
cd ~
mkdir -p local/cmake/.src
cd local/cmake/.src
wget http://www.cmake.org/files/v2.8/cmake-2.8.4.tar.gz
tar zxvf cmake-2.8.4.tar.gz
cd cmake-2.8.4
./configure --prefix=$HOME/local/cmake
make & make install
~~~

安装了CMake之后，开始编译安装MySQL。

~~~bash
PORT=12345 # 找一个没有人用的端口
cd ~
mkdir -p local/mysql/.src
cd local/mysql/.src
wget 'http://downloads.mysql.com/archives/mysql-5.5/mysql-5.5.27.tar.gz'
tar zxvf mysql-5.5.27.tar.gz
cd mysql-5.5.27
cmake -DCMAKE_INSTALL_PREFIX=$HOME/local/mysql \
-DMYSQL_TCP_PORT=$PORT \
-DWITH_INNOBASE_STORAGE_ENGINE=1 .
make & make install
~~~

经过一通编译，MySQL已经安装在$HOME/local/mysql下面了。

现在，需要启动mysql服务了。
MySQL服务是一种daemon服务，简单讲就是运行在后台监听某些端口的服务。
运行MySQL服务的命令是mysqld。
在运行服务之前，首先需要将mysql的一系列命令添加到$PATH中，方法是
~~~bash
echo export PATH=$HOME/local/mysql/bin:$HOME/local/mysql/scripts:$PATH >> ~/.bash_profile
source ~/.bash_profile
~~~

这里，添加了$HOME/local/mysql/bin和$HOME/local/mysql/scripts两个path到系统。

然后用mysql中提供的mysql_install_db脚本创建mysql数据库

~~~bash
mysql_install_db --basedir=$HOME/local/mysql \
--datadir=$HOME/local/mysql/data \
--tmpdir=$HOME/local/mysql/tmp \
--user=$USER
~~~

然后创建mysqld，首先将mysql的配置文件拷贝到$HOME/.my.cnf，命令是：

~~~bash
cp $HOME/mysql/support-files/my-small.cnf $HOME/.my.cnf
~~~

其中，
~~~bash
[client]
port=3306 # 指定端口
socket=$HOME/local/mysql/my.sock

[mysql]
port=3306
socket=$HOME/local/mysql/my.sock

[mysqld]
port=3306 # 指定端口
socket=$HOME/local/mysql/my.sock
datadir=$HOME/local/mysql/data

[mysql.server]
user=yjliu
basedir=$HOME/local/mysql
~~~

然后就是启动mysql服务

~~~bash
mysqld_safe --defaults-file=$HOME/.my.cnf --socket=$HOME/local/mysql/my.sock &
~~~

接下来就可以mysql测试一下是否成功了。

关于mysql，还有一些需要注意的是：当在本地上链接MySQL时，如果指定mysql通过localhost访问，那么mysql并不是通过web端口127.0.0.1:port进行访问的，而是通过一种名为mysql.sock的socket文件进行访问。
如果在web服务中将mysql链接配成localhost，可能会出现一些麻烦事就是不能读写/tmp/mysql.sock而链接数据库不成功（发生在PHP中）。
一个解决方法是使用127.0.0.1:port代替localhost，另一种解决方法是通过配置php.ini，将php.ini的如下字段进行设置然后在启动php监听时加载这个php.ini就OK了。

~~~bash
[MySQL]
mysql.default_socket = /home/yjliu/local/mysql/my.sock
mysql.default_port = 47389
~~~

参考：

* http://community.webfaction.com/questions/3838/compiling-a-private-mysql-installation-in-your-home-directory
* http://www.tech-recipes.com/rx/762/solve-cant-connect-to-local-mysql-server-through-socket-tmpmysqlsock/

安装了mysql，下一步是安装PHP。

同样，我们没有root权限，我们尝试把他安装在$HOME下面，这个难度要比mysql小很多。但是，这里也有一个限制，就是我们能够使用的服务器脚本组合是nginx+php。

下载PHP，编译安装就完成了：

~~~bash
cd ~
mkdir -p local/php5/.src
cd local/php5/.src
wget http://cn2.php.net/get/php-5.3.19.tar.bz2
bzip2 –d php-5.3.19.tar.bz2
tar xvf php-5.3.19.tar.bz2
cd php-5.3.19
./configure --prefix=$HOME/local/php5 \
--with-mysql=$HOME/local/mysql \#设置mysql的安装路径
--with-curl=$HOME/local/cUrl \#设置cUrl
--enable-fpm \ #开启fpm支持
--enable-debug #支持调试
make & make install
~~~

这里重要的一步是在configure中指定mysql位置和开启fpm支持。
这些都完成后，就可以启动php服务了。

~~~bash
./sbin/php-fpm
~~~

如果我们想指定一些配置文件的位置，就可以用
~~~bash
./sbin/php-fpm -c ./lib/php-easy.ini
~~~

参考：
* http://www.cnblogs.com/jsckdao/archive/2011/05/05/2038265.html

这些都搞定后，我们试试用netstat –antl查看一下哪些端口在使用，发现有47388和47389说明服务已经运行起来了。

下一步就是配置nginx，这个在nginx的example配置文件中已经非常清晰地体现了。
只要在某个server中添加如下location就OK了。

~~~bash
location ~ \php {
    root  /home/yjliu/www/main;
    fastcgi_pass 127.0.0.1:47388;
    fastcgi_index index.php;
    fastcgi_param SCRIPT_FILENAME /home/yjliu/www/main$fastcgi_script_name;
    include fastcgi_params;
}
~~~

就想干啥干啥了 =)
