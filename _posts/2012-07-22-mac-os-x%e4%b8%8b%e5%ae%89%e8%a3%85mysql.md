---
layout: post
title: Mac OS X下安装MySQL
date: 2012-07-22 13:31:13.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Skills
tags: []
meta:
  _edit_last: '1'
  bot_views: '4'
  views: '2073'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/578.html"
---
MAC下安装MYSQL有两种方式，一种为 **压缩包形式** &nbsp;另一种为 **.dmg文件安装包** &nbsp;。

&nbsp;

### **首先先介绍压缩包形式的安装方法：**

去MySql官网下MySQL classic版mysql－xxxx.tar.gz[http://dev.mysql.com/downloads/mysql/](http://dev.mysql.com/downloads/mysql/5.1.html)  
记住得是64位的。因为mac下的python是64位，32位的mysql没法在python中用。  
下载之后解压，然后在terminal里敲命令吧：  
`
$ sudo mv mysql-5.1.45-osx10.6-x86_64 /usr/local/mysql
$ cd /usr/local
`

`$ sudo chown -R mysql:mysql mysql
`

递归地添加mysql目录下的所有文件给mysql组的mysql用户

&nbsp;

`$ cd mysql`

`
$ sudo scripts/mysql_install_db --user=mysql`

`以mysql用户的身份建立数据表`

&nbsp;

` $ sudo chown -R root .`

`将mysql的主目录的属主设为root用户`

`
`

`$ sudo chown -R mysql data`

将data目录的属主设为mysql用户

&nbsp;

然后cd bin用  
`$ sudo ./mysql_secure_installation`  
来修改root密码，默认回车为空，显然不太安全，然后根据提示酌情配置，因为是开发环境不用那么严格限制。

对于某些版本，如果有提示mysql/bin不在$PATH变量中，则需要将该路径添加到环境变量。具体方法参见：[Mac OS X添加PATH环境变量](http://www.404story.com/skills/575.html "Mac OS X添加PATH环境变量")

如果对某些版本提示输入当前密码，输入错误，请参考以下地址，重置密码：http://www.debian-administration.org/articles/442

<!--more-->

`$ sudo ./mysqld_safe &`  
用于启动mysql，当然加上nohup命令更好

`$ sudo ./mysql -u root -p`  
输入刚才设置的root密码来登录mysql

`$ sudo ./mysqladmin -u root -p shutdown`  
正确的停止mysql方法

&nbsp;

&nbsp;

### **安装包文件形式的安装方法：**

首先，去http://www.mysql.com/downloads/mysql下载mysql-xxxxx.dmg，然后，双击该文件，安装映像中的两个安装包文件。

&nbsp;

a. mysql-xxxx.pkg（mysql标准版安装）

b. MySQLStartupItem.pkg（mysql启动项目），可以在你电脑启动系统时自动运行mysql服务，它安装在/Library /StartupItems/MySQL/，如果你不想系统启动时运行mysql服务，请不要安装。如果你在安装后又不想使用，请删除/Library /StartupItems/MySQL/这个目录。

&nbsp;

**启动mysql服务**

&nbsp;

1、如果你已经安装了MySQLStartupItem.pkg，重新启动电脑即可。

2、如果你有安装MySQLStartupItem.pkg或者不想启动电脑，运行：应用程序－实用工具－终端，在终端中输入命令：sudo /Library/StartupItems/MySQLCOM/MySQLCOM start，然后输入你的系统管理员密码即可。

&nbsp;

**关闭mysql服务**

&nbsp;

终端中输入命令：sudo /Library/StartupItems/MySQLCOM/MySQLCOM stop，然后输入你的系统管理员密码即可。

&nbsp;

你也可以去系统偏好设置－其他－MySQL，通过这个来启动和停止MySQL服务。

&nbsp;

**更改mysql root账户密码**

&nbsp;

终端中输入命令：/usr/local/mysql/bin/mysqladmin -u root password 新密码

你可以随时使用这条命令更改你的密码。

&nbsp;

**终端登录mysql**

&nbsp;

终端中输入命令：/usr/local/mysql/bin/mysql即可。

&nbsp;

&nbsp;

附python-mysqldb安装

确保 $PATH 里面有 mysql\_config，

解开 MySQLdb 的 tar.gz，

运行 python setup.py build;

python setup.py install

&nbsp;

over了～python进去import MySQLdb试试

