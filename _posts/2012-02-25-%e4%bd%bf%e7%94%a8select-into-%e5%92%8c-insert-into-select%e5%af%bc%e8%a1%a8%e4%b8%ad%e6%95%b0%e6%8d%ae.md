---
layout: post
title: 使用SELECT INTO 和 INSERT INTO SELECT导表中数据
date: 2012-02-25 18:12:09.000000000 -08:00
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
  bot_views: '7'
  views: '3470'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/428.html"
---
Insert是T-sql中常用语句，Insert INTO table(field1,field2,...) values(value1,value2,...)这种形式的在应用程序开发中必不可少。但我们在开发、测试过程中，经常会遇到需要表复制的情况，如将一个table1的数据的部分字段复制到table2中，或者将整个table1复制到table2中，这时候我们就要使用SELECT INTO 和 INSERT INTO SELECT 表复制语句了。

1.INSERT INTO SELECT语句

语句形式为：Insert into Table2(field1,field2,...) select value1,value2,... from Table1

要求目标表Table2必须存在，由于目标表Table2已经存在，所以我们除了插入源表Table1的字段外，还可以插入常量。

&nbsp;

2.SELECT INTO FROM语句

语句形式为：SELECT vale1, value2 into Table2 from Table1

要求目标表Table2不存在，因为在插入时会自动创建表Table2，并将Table1中指定字段数据复制到Table2中。

