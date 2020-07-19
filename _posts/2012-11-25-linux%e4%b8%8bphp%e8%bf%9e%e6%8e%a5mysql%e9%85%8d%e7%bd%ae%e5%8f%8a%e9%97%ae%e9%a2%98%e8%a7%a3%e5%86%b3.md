---
layout: post
title: Linux下php连接mysql，nginx配置及问题解决
date: 2012-11-25 20:24:21.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Solutions
tags: []
meta:
  _edit_last: '1'
  bot_views: '4'
  views: '2455'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/solutions/847.html"
---
安装PHP需要下面软件包的支持，如果没有安装，请自行安装。

```bash
yum -y install gcc gcc-c++ libxml2 libxml2-devel autoconf libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel zlib zlib-devel glibc glibc-devel glib2 glib2-devel
```

由于各个Linux系统版本的不确定性，读者也可以在安装PHP过程中，根据错误提示信息，安装对应的软件库。

### **安装php和php-fpm：**

```bash
tar zxvf php-5.3.x.tar.gz cd php-5.3.x ./configure --prefix=/usr/local/php --enable-fastcgi --enable-fpm --with-mysql=mysqlnd --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd make make install cp php.ini-development /usr/local/php/lib/php.ini
```

<!--more-->

```
一定要带上--with-mysql=mysqlnd，编译安装后才能通过php连接mysql。已经安装的带上这个参数重新安装一下也很快的。
```

PHP-FPM、PHP的全局配置文件是php.ini，在上面的步骤中，已经将此文件复制到了/usr/local/php/lib/php.ini下。可以根据每个应用需求的不同，对php.ini进行相应的配置。 下面重点介绍PHP-FPM引擎的配置文件。根据上面指定的安装路径，PHP-FPM的默认配置文件为/usr/local/php/etc/php-fpm.conf。 php-fpm.conf是一个XML格式的纯文本文件，其内容很容易看明白。

这里重点介绍几个重要的配置标签：

标签listen\_address是配置fastcgi进程监听的IP地址以及端口，默认是127.0.0.1:9000。

```
\<value name="listen\_address"\>127.0.0.1:9000\</value\>
```

标签display\_errors用来设置是否显示PHP错误信息，默认是0，不显示错误信息，设置为1可以显示PHP错误信息。

```
\<value name="display\_errors"\>0\</value\>
```

标签user和group用于设置运行FastCGI进程的用户和用户组。需要注意的是，这里指定的用户和用户组要和Nginx配置文件中指定的用户和用户组一致。

```
\<value name="user"\>nobody\</value\> \< value name="group"\>nobody\</value\>
```

标签max\_children用于设置FastCGI的进程数。根据官方建议，小于2GB内存的服务器，可以只开启64个进程，4GB以上内存的服务器可以开启200个进程。

```
\<value name="max\_children"\>5\</value\>
```

标签request\_terminate\_timeout用于设置FastCGI执行脚本的时间。默认是0s，也就是无限执行下去，可以根据情况对其进行修改。

```
\<value name="request\_terminate\_timeout"\>0s\</value\>
```

标签rlimit\_files用于设置PHP-FPM对打开文件描述符的限制，默认值为1024。这个标签的值必须和Linux内核打开文件数关联起来，例如要将此值设置为65535，就必须在Linux命令行执行'ulimit -HSn 65536'。

```
\<value name="rlimit\_files"\>1024\</value\>
```

标签max\_requests指明了每个children最多处理多少个请求后便会被关闭，默认的设置是500。

```
\<value name="max\_requests"\>500\</value\>
```

标签allowed\_clients用于设置允许访问FastCGI进程解析器的IP地址。如果不在这里指定IP地址，Nginx转发过来的PHP解析请求将无法被接受。

```
\<value name="allowed\_clients"\>127.0.0.1\</value\>
```

&nbsp;

### 管理FastCGI进程

在配置完php-fpm后，就可以启动FastCGI进程了。启动fastcgi进程使用：

```
/usr/local/php/sbin/php-fpm
```

```
php-fpm&nbsp;关闭： kill&nbsp;-SIGINT&nbsp;`cat&nbsp;/usr/local/php/var/run/php-fpm.pid` php-fpm&nbsp;重启： kill&nbsp;-SIGUSR2&nbsp;`cat&nbsp;/usr/local/php/var/run/php-fpm.pid`
```

```
从php5.3.3开始&nbsp;源码中开始包含&nbsp;php-fpm，不用专门再打补丁了，只需要解开源码直接configure， 关于php-fpm的编译参数有&nbsp;–enable-fpm&nbsp;–with-fpm-user=www&nbsp;–with-fpm-group=www&nbsp;–with-libevent-dir=libevent位置。 这个php-fpm&nbsp;不再支持&nbsp;php-fpm&nbsp;补丁具有的&nbsp;/usr/local/php/sbin/php-fpm&nbsp;(start|stop|reload)等命令，需要使用信号控制： master进程可以理解以下信号 SIGINT,&nbsp;SIGTERM&nbsp;立刻终止 SIGQUIT&nbsp;平滑终止 SIGUSR1&nbsp;重新打开日志文件 SIGUSR2&nbsp;平滑重载所有worker进程并重新载入配置和二进制模块
```

```

```

```

```

```

```

### 配置Nginx来支持PHP

Nginx的安装特别简单，前面已经对此进行了详细介绍，这里不再进行讲述。下面重点介绍Nginx如何通过php-fpm的FastCGI进程对PHP进行解析处理。 由于Nginx本身不会对PHP进行解析，因此要实现Nginx对PHP的支持，其实是将对PHP页面的请求交给fastCGI进程监听的IP地址及端口。如果把php-fpm当做动态应用服务器，那么Nginx其实就是一个反向代理服务器。Nginx通过反向代理功能实现对PHP的解析，这就是Nginx实现PHP动态解析的原理。 这里假定Nginx的安装目录为/usr/local，则Nginx配置文件的路径为/usr/local/nginx/conf/nginx.conf。下面是在Nginx下支持PHP解析的一个虚拟主机配置实例。

```actionscript3
server { include port.conf; server\_name www.404story.com; location / { index index.html index.php; root /web/www/www.404story.com; } location ~ .php$ { root html; fastcgi\_pass 127.0.0.1:9000; fastcgi\_index index.php; fastcgi\_param SCRIPT\_FILENAME $document\_root$fastcgi\_script\_name; include fastcgi\_params; } }
```

通过location指令，将所有以php为后缀的文件都交给127.0.0.1:9000来处理，而这里的IP地址和端口就是FastCGI进程监听的IP地址和端口。&nbsp;fastcgi\_param指令指定放置PHP动态程序的主目录，也就是$fastcgi\_script\_name前面指定的路径，这里是/usr/local/nginx/html目录，建议将这个目录与Nginx虚拟主机指定的根目录保持一致，当然也可以不一致。&nbsp;fastcgi\_params文件是FastCGI进程的一个参数配置文件，在安装Nginx后，会默认生成一个这样的文件，这里通过include指令将FastCGI参数配置文件包含了进来。 接下来，启动nginx服务。&nbsp;/usr/local/nginx/sbin/nginx&nbsp;到此为止，Nginx+PHP已经配置完成。

### 附：mysqlnd cannot connect to MySQL 4.1+ using the old insecure authentication 错误解决方法

解决方法：

```sql
SET old\_passwords = 0; UPDATE mysql.user SET Password = PASSWORD('testpass') WHERE User = 'testuser'; FLUSH PRIVILEGES;
```
