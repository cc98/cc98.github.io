---
layout: post
title: 再加InnoDB和MyISAM区别总结
date: 2012-03-24 10:24:30.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Share
tags: []
meta:
  _edit_last: '1'
  bot_views: '4'
  views: '2660'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/441.html"
excerpt: InnoDB和MyISAM是许多人在使用MySQL时最常用的两个表类型，这两个表类型各有优劣，视具体应用而定。基本的差别为：MyISAM类型不支持事务处理等高级处理，而InnoDB类型支持。MyISAM类型的表强调的是性能，其执行速度比InnoDB类型更快，但是不提供事务支持，而InnoDB提供事务支持已经外部键等高级数据库功能。
---
InnoDB和MyISAM是许多人在使用MySQL时最常用的两个表类型，这两个表类型各有优劣，视具体应用而定。基本的差别为：MyISAM类型不支持事务处理等高级处理，而InnoDB类型支持。MyISAM类型的表强调的是性能，其执行速度比InnoDB类型更快，但是不提供事务支持，而InnoDB提供事务支持已经外部键等高级数据库功能。  
MyIASM是IASM表的新版本，有如下扩展：

·二进制层次的可移植性。  
·NULL列索引。  
·对变长行比ISAM表有更少的碎片。  
·支持大文件。  
·更好的索引压缩。  
·更好的键吗统计分布。  
·更好和更快的auto\_increment处理。  
以下是一些细节和具体实现的差别：  
◆1.InnoDB不支持FULLTEXT类型的索引。  
◆2.InnoDB 中不保存表的具体行数，也就是说，执行select count(\*) from table时，InnoDB要扫描一遍整个表来计算有多少行，但是MyISAM只要简单的读出保存好的行数即可。注意的是，当count(\*)语句包含 where条件时，两种表的操作是一样的。  
◆3.对于AUTO\_INCREMENT类型的字段，InnoDB中必须包含只有该字段的索引，但是在MyISAM表中，可以和其他字段一起建立联合索引。  
◆4.DELETE FROM table时，InnoDB不会重新建立表，而是一行一行的删除。  
◆5.LOAD TABLE FROM MASTER操作对InnoDB是不起作用的，解决方法是首先把InnoDB表改成MyISAM表，导入数据后再改成InnoDB表，但是对于使用的额外的InnoDB特性（例如外键）的表不适用。

另外，InnoDB表的行锁也不是绝对的，假如在执行一个SQL语句时MySQL不能确定要扫描的范围，InnoDB表同样会锁全表，例如update table set num=1 where name like “%aaa%”

综上所述，任何一种表都不是万能的，只有恰当的针对业务类型来选择合适的表类型，才能最大的发挥MySQL的性能优势。

