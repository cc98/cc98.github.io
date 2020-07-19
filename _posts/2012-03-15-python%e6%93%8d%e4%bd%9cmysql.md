---
layout: post
title: Python操作Mysql
date: 2012-03-15 23:31:21.000000000 -07:00
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
  bot_views: '5'
  views: '2137'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/438.html"
---
&nbsp;平时的主要编程语言是Java，开发时也主要用Mysql，经常为了测试，调试的目的需要操作数据库，比如备份，插入测试数据，修改测试数据，有些时候不能简单的用SQL就能完成任务，或都很好的完成任务，用Java写又有点太麻烦了，就想到了Python。Python语法简洁，不用编译，可以经较好的完成任务。今天看了下Python对Mysql的操作，做一下记录。

首先，安装需要的环境，Mysql和Python就不说了，必备的东西。

主要是安装的MySQLdb，可以去sf.net下载，具体地址是http://sourceforge.net/projects/mysql-python/

如果用Ubuntu，直接

sudo apt-get install python-mysqldb

安装完成之后可以在Python解释器中测试一下

&nbsp;<!--more-->

输入

Python代码

import MySQLdb #注意大小写！！

&nbsp;如果不报错，就证明安装成功了，可能继续了

MySQLdb在Python中也就相当于JAVA中的MySQL的JDBC Driver，Python也有类似的数据接口规范Python DB API，MySQLdb就是Mysql的实现。操作也比较简单和其它平台或语言操作数据库一样，就是建立和数据库系统的连接，然后给数据库输入SQL，再从数据库获取结果。

先写一个最简单的，创建一个数据库：

Python代码

```python
#!/usr/bin/env python #coding=utf-8 ################################### # @author migle # @date 2010-01-17 ################################## #MySQLdb 示例 # ################################## import MySQLdb #建立和数据库系统的连接 conn = MySQLdb.connect(host='localhost', user='root',passwd='longforfreedom') #获取操作游标 cursor = conn.cursor() #执行SQL,创建一个数据库. cursor.execute("""create database python """) #关闭连接，释放资源 cursor.close();
```

创建数据库，创建表，插入数据，插入多条数据

Python代码

```python
#!/usr/bin/env python #coding=utf-8 ################################### # @author migle # @date 2010-01-17 ################################## #MySQLdb 示例 # ################################## import MySQLdb #建立和数据库系统的连接 conn = MySQLdb.connect(host='localhost', user='root',passwd='longforfreedom') #获取操作游标 cursor = conn.cursor() #执行SQL,创建一个数据库. cursor.execute("""create database if not exists python""") #选择数据库 conn.select\_db('python'); #执行SQL,创建一个数据表. cursor.execute("""create table test(id int, info varchar(100)) """) value = [1,"inserted ?"]; #插入一条记录 cursor.execute("insert into test values(%s,%s)",value); values=[] #生成插入参数值 for i in range(20): values.append((i,'Hello mysqldb, I am recoder ' + str(i))) #插入多条记录 cursor.executemany("""insert into test values(%s,%s) """,values); #关闭连接，释放资源 cursor.close();
```

查询和插入的流程差不多，只是多了一个得到查询结果的步骤

Python代码

```python
#!/usr/bin/env python #coding=utf-8 ###################################### # # @author migle # @date 2010-01-17 # ###################################### # # MySQLdb 查询 # ####################################### import MySQLdb conn = MySQLdb.connect(host='localhost', user='root', passwd='longforfreedom',db='python') cursor = conn.cursor() count = cursor.execute('select \* from test') print '总共有 %s 条记录',count #获取一条记录,每条记录做为一个元组返回 print "只获取一条记录:" result = cursor.fetchone(); print result #print 'ID: %s info: %s' % (result[0],result[1]) print 'ID: %s info: %s' % result #获取5条记录，注意由于之前执行有了fetchone()，所以游标已经指到第二条记录了，也就是从第二条开始的所有记录 print "只获取5条记录:" results = cursor.fetchmany(5) for r in results: print r print "获取所有结果:" #重置游标位置，0,为偏移量，mode＝absolute | relative,默认为relative, cursor.scroll(0,mode='absolute') #获取所有结果 results = cursor.fetchall() for r in results: print r conn.close()
```

