---
layout: post
title: '解决select into outfile : Access Denied问题'
date: 2012-11-29 15:00:29.000000000 -08:00
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
  bot_views: '5'
  views: '6843'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/solutions/854.html"
---
abc@localhost : \> select \* into outfile ‘/tmp/1.txt’ from tb1 limit 5;  
ERROR 1045 (28000): Access denied for user ‘abc’@'%’ (using password: NO)

### 方法一：添加file授权。

grant file on \*.\* to abc;

如果上面提示的错误是：如果是Access denied for user ‘abc’@'127.0.0.1’ (using password: NO)

则需要执行：grant file on \*.\* to abc@'127.0.0.1';

之后：&nbsp;flush privileges;

用abc用户重新连接，select into outfile 搞定。

<!--more-->

### 方法二：直接在外面导

mysql -uabc -p -e ’select \* from tb1 limit 5;’ \>1.txt

&nbsp;

