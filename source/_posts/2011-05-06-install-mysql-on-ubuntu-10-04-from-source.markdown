---
comments: true
published: false
date: 2011-05-06 21:45:02
layout: post
slug: install-mysql-on-ubuntu-10-04-from-source
title: Ubuntu 10.04.2上编译安装MySQL 5.5.11
wordpress_id: 259
categories:
- Linux
tags:
- mysql
- ubuntu
- 编译安装
---

由于我之前安装其他的软件时，已经安装了mysql的开发相关的lib，因此编译安装MySQL不是很顺利。具体的错误神马的，就不提了（也没记住多少……）应该都是个例。总结起来一句话就是——尽量在你安装Mysql前电脑尽量保持clean(一些mysql的开发包一类的最好先卸载)。
<!-- more -->
有一些童鞋可能会问在ubuntu里apt不是可以完全搞定吗，为什么要这么费事的编译安装？我的原因：对我来说用ubuntu，用linux就是了解细枝末节，更深入的理解OS，也就是“折腾”，apt-get install是很好很强大，但这种方法提供便利的同时也阻碍了你去了解linux上软件构建的过程，这种方法同WIndows上下载安装包装软件还简单（起码在WIN上你还知道什么东西放在哪儿了）。通过从源代码编译安装，你就有了一个了解Linux上软件构建部署的机会，可以收获更多。同时在这过程中你也可以将mysql部署到任何位置，同时又可以用到比repo里更新的版本。


正题：




步骤：





	
  1. 编译前的准备工作

	
  2. 初识CMAKE——配置MySQL编译选项

	
  3. 编译安装

	
  4. 安装后的MySQL配置

	
  5. 设置开机自动启动MySQL服务

<!-- more -->


## 一、编译前的准备工作





	
  * 官方网站下载Source Code（[点此进入下载页](http://dev.mysql.com/downloads/mysql/#downloads)）选择Source Code-->Generic Linux(mysql-VERSION.tar.gz)（PS：chrome访问此页，可能会遇到显示不正常的情况，建议换FF访问）

	
  * 建议有兴趣的童鞋读一读解压后的mysql目录下的相关文档，有许多重要的信息。比如此文以及大部分的类似文章都参考自INSTALL-SOURCE文档。

	
  * 创建mysql用户以及用户组，方便管理[bash]sudo groupadd mysql[/bash]

[bash]sudo useradd -r -g mysql mysql[/bash]




## 二、初识CMAKE——配置MySQL编译选项


MySQL 5.5的编译工具由Autotool转变为了cmake（有关于更多关于cmake的信息，请大家自行google了解）。MySQL团队也撰写了一篇[Autotools to CMake Transition Guide](http://forge.mysql.com/wiki/Autotools_to_CMake_Transition_Guide),本文将要列出的各个编译选项以及更多的编译选项的说明可以参考该文档。在troubleshooting时，此文档更是不得不看。编译时我习惯于一些选项（比如安装位置）不按默认的来，因为如果按默认选项出了问题，更不好解决（因为到时你不仅需要知道到底有选项有何含义还要知道默认的是什么，反而更麻烦）。进入解压的源代码目录mysql-VERSION

[bash]cmake . \
-DCMAKE_INSTALL_PREFIX=/usr/mysql \
-DMYSQL_DATADIR=/usr/mysql/data
-DDEFAULT_CHARSET=utf8 \
-DDEFAULT_COLLATION=utf8_general_ci \
-DMYSQL_UNIX_ADDR=/tmp/mysqld.sock \
-DWITH_DEBUG=0 \
-DWITH_INNOBASE_STORAGE_ENGINE=1[/bash]

丰富的








选项名称


选项含义






DCMAKE_INSTALL_PREFIX


安装路径






DMYSQL_DATADIR


数据库路径






DDEFAULT_CHARSET


默认字符






DDEFAULT_COLLATION


默认字符集






DMYSQL_UNIX_ADDR


连接数据库socket路径






DWITH_DEBUG


bool值，表示是否开启debug模式




在这里我开始的时候有一个疏忽：**只设置DDEFAULT_CHARSET而没有设置DDEFAULT_COLLATION**，因此总是出现

[text]COLLATION 'latin1_swedish_ci' is not valid for CHARACTER SET 'utf8'[/text]


## 三、编译安装


[bash]sudo make[/bash]

[bash]sudo make install[/bash]

这个阶段出现的问题概率较小。但是记得一定要以**root权限执行make和make install**，因为填写的安装路径不是home，而是/usr，必须有root权限才能进行写操作。


## 四、安装后的MySQL配置


出问题的地方主要是在这里。出现问题的根源在于**配置文件**以及默认配置。由于是源代码安装且安装的位置不是默认位置，因此有一些选项必须制定才能使MySQL正常运行



	
  1. 进入安装后的目录执行[bash]sudo chown -R mysql .[/bash]

[bash]chgrp -R mysql .[/bash]

	
  2. [bash]sudo bin/scripts/mysql_install_db \
--user=mysql \
--basedir=/usr/mysql \
--datadir=/usr/mysql/data \
--no-defaults[/bash]

切记后面有个--no-defaults选项，如果没有该选项，则程序会自动载入默认的配置文件，而目前你还没有完成配置文件的编写，因此很可能载入的是错误的信息。如果该指令能够运行成功，那么恭喜你，你的MySQLy可以成功的启动了。如果这一步出现了错误，不要着急，相关的log以及mysqld的启动信息提供了足够的信息帮助你trouble shooting（我就是这么过来的...）完成之后再执行

[bash]chown -R root .[/bash]

[bash]chown -R mysql data[/bash]

这两条指令应该是安全性考虑。

	
  3. 配置my.cnf——mysql的配置文件，这是很重要的一步，配置得当以后就不需要在启动时写上大段的参数了。
首先应该知道：MySQL寻找配置文件的路径以及顺序。最开始检索的位置是`/etc/my.cnf`之后是`/etc/mysql/my.cnf`因此我们要做的就是在这两个地方之一建立配置文件my.cnf。MySQL为我们准备了几种不同方案的默认配置文件（在/usr/mysql/support-files/中），因此我们可以复制一份到上述的位置[bash]sudo cp /usr/mysql/support-files/my-medium.cnf /etc/mysql/my.cnf[/bash]

通常我们是通过脚本传入适当的参数启动mysqld。因此在/etc/my.cnf中加入如下的内容：

[text]
[mysqld]
basedir=/usr/mysql
datadir=/usr/mysql/data
user=mysql
[/text]

更多关于my.cnf的配置限于篇幅就不再讲了，但为了日常的开发需要还应该继续配置的，这部分内容就参考google搜索以及MySQL Manual吧




## 五、设置开机自动启动MySQL服务


这一部分讲解如何添加MySQL在开机时自动启动。MySQL Manual关于此部分的内容不准确，没有涵盖debian类的linux发行版的做法。

MySQL已经提供了默认的脚本mysql.server（在[mysql安装目录]/support-files/），首先进入该目录，尝试运行该脚本

[bash]sudo ./mysql.server start[/bash]

运行正常的话则执行

[bash]sudo cp mysql.server /etc/init.d/mysql[/bash]

Debian/Ubuntu上开机启动服务的管理不是使用chkconfig，而使用的是sysv-rc-conf，尝试执行

[bash]sudo sysv-rc-conf[/bash]

若提示没有安装，则

[bash]sudo apt-get install sysv-rc-conf[/bash]

，之后运行即可，该工具采用的是图形界面，很直观在此就不介绍如何使用了，我们需要做的是找到【mysql】一栏，选定【3】【4】【5】这三列，这样就完成了开机自动启动MySQL daemon了。

**MySQL的安装就基本完成了，希望大家能和我一样在“折腾”的过程中有所收获，“痛并快乐着”！**


## 参考链接：





	
  * [mysql 5.5.9 编译过程中都问题 by flycatcn](http://forum.ubuntu.org.cn/viewtopic.php?f=44&t=319251)

	
  * [用源码编译安装MYSQL5.5到ubuntu10.10上by winksir](http://forum.ubuntu.org.cn/viewtopic.php?f=44&t=319886)

	
  * [MySQL 5.5 Reference Manual --Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.5/en/charset-server.html)

	
  * [MySQL 5.5 Reference Manual --mysqld_safe](http://dev.mysql.com/doc/refman/5.5/en/mysqld-safe.html)

	
  * [MySQL 5.5 Reference Manual --Using Option Files](http://dev.mysql.com/doc/refman/5.5/en/option-files.html)

	
  * [Starting and Stopping MySQL Automatically](http://dev.mysql.com/doc/refman/5.5/en/automatic-start.html)


