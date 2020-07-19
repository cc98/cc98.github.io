---
layout: post
title: 安装memcached教程，telnet和php测试方法
date: 2013-06-18 15:51:23.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Labrary
tags: []
meta:
  _edit_last: '1'
  bot_views: '9'
  views: '2791'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/1015.html"
---
<p>用telnet测试memcached</p>
<div>
<div>telnet 127.0.0.1 11211</div>
<div>Trying 127.0.0.1…</div>
<div>Connected to zou.yunhao (127.0.0.1).</div>
<div>Escape character is ‘^]’.</div>
<div>set key 0 10 6   //10表示过期时间10秒，6表示将要存入数据字节为6（这里result为6）</div>
<div>result</div>
<div>STORED</div>
<div>get key</div>
<div>VALUE key 0 6</div>
<div>result</div>
<div>END</div>
<div><!--more--></div>
</div>
<div id="_mcePaste">4）memcached性能查看命令stats</div>
<div id="_mcePaste">telnet 127.0.0.1 11211</div>
<div id="_mcePaste">stats</div>
<div id="_mcePaste">STAT pid 18006</div>
<div id="_mcePaste">STAT uptime 702   //memcached运行的秒数</div>
<div id="_mcePaste">STAT time 1292904537 //memcached服务器所在主机当前系统的时间，单位是秒。</div>
<div id="_mcePaste">STAT version 1.4.5</div>
<div id="_mcePaste">STAT pointer_size 64  //服务器所在主机操作系统的指针大小，一般为32或64</div>
<div id="_mcePaste">STAT rusage_user 0.003999</div>
<div id="_mcePaste">STAT rusage_system 0.013997</div>
<div id="_mcePaste">STAT curr_connections 10   //表示当前的连接数</div>
<div id="_mcePaste">STAT total_connections 11   //表示从memcached服务启动到当前时间，系统打开过的连接的总数。</div>
<div id="_mcePaste">STAT connection_structures 11</div>
<div id="_mcePaste">STAT cmd_get 0   //查询缓存的次数，平均每秒缓存次数cmd_get/uptime</div>
<div id="_mcePaste">STAT cmd_set 0   //设置key=&gt;value的次数</div>
<div id="_mcePaste">STAT cmd_flush 0</div>
<div id="_mcePaste">STAT get_hits 0  //缓存命中的次数，缓存命中率=get_hits/cmd_get*100%</div>
<div id="_mcePaste">STAT get_misses 0  //cmd_get-get_hits</div>
<div id="_mcePaste">STAT delete_misses 0</div>
<div id="_mcePaste">STAT delete_hits 0</div>
<div id="_mcePaste">STAT incr_misses 0</div>
<div id="_mcePaste">STAT incr_hits 0</div>
<div id="_mcePaste">STAT decr_misses 0</div>
<div id="_mcePaste">STAT decr_hits 0</div>
<div id="_mcePaste">STAT cas_misses 0</div>
<div id="_mcePaste">STAT cas_hits 0</div>
<div id="_mcePaste">STAT cas_badval 0</div>
<div id="_mcePaste">STAT auth_cmds 0</div>
<div id="_mcePaste">STAT auth_errors 0</div>
<div id="_mcePaste">STAT bytes_read 7  //memcached服务器从网络读取的总的字节数</div>
<div id="_mcePaste">STAT bytes_written 0  //memcached服务器发送到网络的总的字节数。</div>
<div id="_mcePaste">STAT limit_maxbytes 67108864  //memcached服务缓存允许使用的最大字节数</div>
<div id="_mcePaste">STAT accepting_conns 1</div>
<div id="_mcePaste">STAT listen_disabled_num 0</div>
<div id="_mcePaste">STAT threads 4</div>
<div id="_mcePaste">STAT conn_yields 0</div>
<div id="_mcePaste">STAT bytes 0</div>
<div id="_mcePaste">STAT curr_items 0</div>
<div id="_mcePaste">STAT total_items 0</div>
<div id="_mcePaste">STAT evictions 0</div>
<div id="_mcePaste">STAT reclaimed 0</div>
<div id="_mcePaste">END</div>
<div></div>
<div></div>
<div>-------------------------------
[root@jushanweb1 ~]# telnet 192.168.12.201 13002  
Trying 192.168.12.201...  
Connected to 192.168.12.201 (192.168.12.201).  
Escape character is '^]'.  
stats  
STAT pid 8382  
STAT uptime 190574  
STAT time 1301579774  
STAT version 1.2.0  
STAT pointer\_size 32  
STAT rusage\_user 0.003999  
STAT rusage\_system 0.033994  
STAT curr\_items 1  
STAT total\_items 1  
STAT bytes 50  
STAT curr\_connections 2  
STAT total\_connections 4  
STAT connection\_structures 3  
STAT cmd\_get 0  
STAT cmd\_set 1  
STAT get\_hits 0  
STAT get\_misses 0  
STAT bytes\_read 216  
STAT bytes\_written 92  
STAT limit\_maxbytes 524288000  
END

监控
1）nagios监控

a. check\_memcached

先要安装check\_memcached插件

wget http://search.cpan.org/CPAN/authors/id/Z/ZI/ZIGOROU/Nagios-Plugins-Memcached-0.02.tar.gz

tar xzvf Nagios-Plugins-Memcached-0.02.tar.gz

cd Nagios-Plugins-Memcached-0.02

perl Makefile.PL &nbsp; (可能需要其他perl的modules，依照提示通过cpan安装即可）

make && make install

check\_memcached [-H host:port] [-w warnings] [-c critical] [--size-warnng size-warnng] [--size-critical size-critical] [--hit-warning hit-warning] [--hit-critical

hit-critical] [-t timeout]

b. /check\_tcp -H host -p 11211 -t 5 -E -s ‘statsrnquitrn’ -e ‘uptime’ -M crit

2）cacti监控

一台服务器起多个memcached，多端口cacti部署监控。

a. 需要一个 Python memcached Client API

wget ftp://ftp.tummy.com/pub/python-memcached/python-memcached-1.45.tar.gz

tar xzvf python-memcached-1.45.tar.gz

cd python-memcached-1.45

python setup.py install

b. 加模板memcached multiport

wget http://tag1consulting.com/blog/cacti-memcache-multi-port-templates

cp memcached.py &nbsp; \<cacti install目录\>/scripts/memcachedmultiport.py

c. 增加监控时devices-\>des && ip-\>host template选择memcachedmultiport-\>Downed Device Detection选择none-\>SNMP Version选择not in use-\>create graphs-\>Port to query for&nbsp;memcached statistics填写memcached端口。

3）也可以自定义nagios、cacti监控，通过memcached命令stats取相关数据。

### php方法:

### 运行下面的php文件，如果有输出This is a test!，就表示环境搭建成功。开始领略Memcache的魅力把！

```php
\< ?php $mem = new Memcache; $mem-\>connect(“66.90.103.147″, 12000); $mem-\>set(‘key’,'This is a test!’, 0, 60); $val = $mem-\>get(‘key’); echo $val; ?\>
```

# CentOS上安装memcache的方法

所有操作都在SSH下，以根帐号登录。

我的版本为Centos Release 5.3 (Final)  
使用这个命令可以知道你的Linux版本  
cat /etc/redhat-release  
首先要安装libevent库。  
cd /usr/local/src  
curl -O http://monkey.org/~provos/libevent-1.4.10-stable.tar.gz  
tar xzvf libevent-1.4.10-stable.tar.gz  
cd libevent-1.4.10-stable  
./configure –prefix=/usr/local  
make  
make install

接下来就是安装memcached

cd /usr/local/src  
curl -O http://www.danga.com/memcached/dist/memcached-1.2.8.tar.gz  
tar xzvf memcached-1.2.8.tar.gz  
cd memcached-1.2.8  
LDFLAGS=’-Wl,–rpath /usr/local/lib’ ./configure –prefix=/usr/local  
make  
make install

安装完毕后，用下面这个命令以用户root来运行memcache  
memcached -u root -d -m 64 -l 192.168.0.101 -p 11211  
root 为所执行的用户  
64 为缓存大小64M  
192.168.0.101 为所在的服务器IP地址  
11211 是所在端口

要关闭memcache  
pkill memcached

接下来是安装php-pecl-memcache  
一个命令就可以。  
yum install php-pecl-memcache

还是需要php扩展，就用下面这个命令  
pecl install memcache

接下来重启apache，用phpinfo()查看，应该可以看到memcache的部分，如果没有的话，检查这里的设置：  
/etc/php.ini加上了 extension=memcache.so  
当然也要确认memcache.so是否存在，是否在/usr/lib/php/modules/下，如果不是，那么找到它，并用完整路径表示。

查看memcache的运行情况，可以用memcache.php来查看。  
当让也要有web 程序支持才有用，比如我用的phpbb 3就可以使用memcache，具体方法参考[这里](http://www.yinfor.com/blog/archives/2009/06/enable_memcache_on_phpbb_3.html)  
[  
](http://seo.g2soft.net/assets-c/2009/06/memcache-256.html)

原作者:&nbsp;[David Yin](http://www.yinfor.com/blog/)

## Update

不过我今天实战中并没有使用上面的方法：

介绍一下yum的方法：

yum install libevent

这个是第一步，

第二步是安装memcache，但是标准的CentOS5软件仓库里面是没有memcache相应的包的,所以，我们的第一步就是导入第三方软件仓库，这里推荐的是 Dag Wieers 库（现在叫 RPMForge 了），安装方法如下：

wget&nbsp;http://dag.wieers.com/rpm/packages/rpmforge-release/rpmforge-release-0.3.6-1.el5.rf.i386.rpm

rpm -ivh rpmforge-release-0.3.6-1.el5.rf.i386.rpm

查找相关软件包

yum search memcache

有了，现在可以安装了

yum -y install –enablerepo=rpmforge memcached php-pecl-memcache

验证一下安装结果

memcached -h

php -m|grep memcache

启动memcached

/sbin/servive memcached start

============

Update Dec 16th

Linux下Memcache服务器端的安装  
服务器端主要是安装memcache服务器端，目前的最新版本是 memcached-1.3.0 。  
下载：http://www.danga.com/memcached/dist/memcached-1.2.2.tar.gz  
另外，Memcache用到了libevent这个库用于Socket的处理，所以还需要安装libevent，libevent的最新版本是libevent-1.3。（如果你的系统已经安装了libevent，可以不用安装）  
官网：http://www.monkey.org/~provos/libevent/  
下载：http://www.monkey.org/~provos/libevent-1.3.tar.gz

用wget指令直接下载这两个东西.下载回源文件后。  
1.先安装libevent。这个东西在配置时需要指定一个安装路径，即./configure –prefix=/usr；然后make；然后make install；  
2.再安装memcached，只是需要在配置时需要指定libevent的安装路径即./configure –with-libevent=/usr；然后make；然后make install；  
这样就完成了Linux下Memcache服务器端的安装。详细的方法如下：

1.分别把memcached和libevent下载回来，放到 /tmp 目录下：  
# cd /tmp  
# wget http://www.danga.com/memcached/dist/memcached-1.2.0.tar.gz  
# wget http://www.monkey.org/~provos/libevent-1.2.tar.gz

2.先安装libevent：  
# tar zxvf libevent-1.2.tar.gz  
# cd libevent-1.2  
# ./configure –prefix=/usr  
# make  
# make install

3.测试libevent是否安装成功：  
# ls -al /usr/lib | grep libevent  
lrwxrwxrwx 1 root root 21 11?? 12 17:38 libevent-1.2.so.1 -\> libevent-1.2.so.1.0.3  
-rwxr-xr-x 1 root root 263546 11?? 12 17:38 libevent-1.2.so.1.0.3  
-rw-r–r– 1 root root 454156 11?? 12 17:38 libevent.a  
-rwxr-xr-x 1 root root 811 11?? 12 17:38 libevent.la  
lrwxrwxrwx 1 root root 21 11?? 12 17:38 libevent.so -\> libevent-1.2.so.1.0.3  
还不错，都安装上了。

4.安装memcached，同时需要安装中指定libevent的安装位置：  
# cd /tmp  
# tar zxvf memcached-1.2.0.tar.gz  
# cd memcached-1.2.0  
# ./configure –with-libevent=/usr  
# make  
# make install  
如果中间出现报错，请仔细检查错误信息，按照错误信息来配置或者增加相应的库或者路径。  
安装完成后会把memcached放到 /usr/local/bin/memcached ，

5.测试是否成功安装memcached：  
# ls -al /usr/local/bin/mem\*  
-rwxr-xr-x 1 root root 137986 11?? 12 17:39 /usr/local/bin/memcached  
-rwxr-xr-x 1 root root 140179 11?? 12 17:39 /usr/local/bin/memcached-debug

安装Memcache的PHP扩展  
1.在http://pecl.php.net/package/memcache 选择相应想要下载的memcache版本。  
2.安装PHP的memcache扩展

tar vxzf memcache-2.2.1.tgz  
cd memcache-2.2.1  
/usr/bin/phpize  
./configure -enable-memcache -with-php-config=/usr/bin/php-config -with-zlib-dir  
make  
make install

3.上述安装完后会有类似这样的提示：

Installing shared extensions: /usr/local/php/lib/php/extensions/no-debug-non-zts-2007xxxx/

4.把php.ini中的extension\_dir = “./”修改为

extension\_dir = “/usr/local/php/lib/php/extensions/no-debug-non-zts-2007xxxx/”

5.添加一行来载入memcache扩展：extension=memcache.so

memcached的基本设置：  
1.启动Memcache的服务器端：  
# /usr/local/bin/memcached -d -m 10 -u root -l 66.90.103.147 -p 12000 -c 256 -P /tmp/memcached.pid

-d选项是启动一个守护进程，  
-m是分配给Memcache使用的内存数量，单位是MB，我这里是10MB，  
-u是运行Memcache的用户，我这里是root，  
-l是监听的服务器IP地址，如果有多个地址的话，我这里指定了服务器的IP地址192.168.0.200，  
-p是设置Memcache监听的端口，我这里设置了12000，最好是1024以上的端口，  
-c选项是最大运行的并发连接数，默认是1024，我这里设置了256，按照你服务器的负载量来设定，  
-P是设置保存Memcache的pid文件，我这里是保存在 /tmp/memcached.pid，

2.如果要结束Memcache进程，执行：

# kill `cat /tmp/memcached.pid`

也可以启动多个守护进程，不过端口不能重复。

3.重启apache，service httpd restart

