---
layout: post
title: Mac OS X中MacPorts安装和使用
date: 2012-07-24 17:21:16.000000000 -07:00
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
  bot_views: '6'
  views: '2335'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/599.html"
---
### 安装MacPorts：

目前最新的是2.1.1版，有新的大家自己改改

```bash
wget http://distfiles.macports.org/MacPorts/MacPorts-2.1.1.tar.gz tar zxvf MacPorts-2.1.1.tar.gz cd MacPorts-2.1.1 ./configure make sudo make install cd .. rm -rf MacPorts-2.1.1\*
```

然后将/opt/local/bin和/opt/local/sbin添加到$PATH搜索路径中

方法有几种，最常用的是直接用vim打开/etc/paths，直接将这两行添加进去。

<!--more-->

### 使用说明：

更新ports tree和MacPorts版本，强烈推荐第一次运行的时候使用-v参数，显示详细的更新过程。  
 sudo port -v selfupdate

搜索索引中的软件  
 port search name

安装新软件  
 sudo port install name

卸载软件  
 sudo port uninstall name

查看有更新的软件以及版本  
 port outdated

升级可以更新的软件  
 sudo port upgrade outdated

