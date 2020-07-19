---
layout: post
title: 'Berkeley DB Access Method: Hash、Btree、Queue、Recno'
date: 2012-05-15 22:23:06.000000000 -07:00
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
  bot_views: '3'
  views: '1748'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/519.html"
---
在数据库应用中,数据访问方式对应数据在硬盘上的存储格式和操作方法。在编写应用时，选择合适的算法可以极大的提高运算速度。大多数数据库都选用Btree算法，DB也不例外，同时还提供Hash算法、Recno算法和Queue算法。Berkeley DB的强大之一是它为这几种算法提供了差不多相同的接口，这表明当你要使用另一种算法时修改程序是简单的。程序在需要对特殊数据结构和存取模式操作时，通过不同的算法可以轻易的解决。

大多数应用要么在Btree和Hash算法之间，要么在Queue和Recno算法之间选择。

Hash 还是 Btree？  
当记录号不是用于数据存取的主键时，应该使用 Hash和Btree算法。&nbsp;(如果记录号是用于数据存取的一个二级关键字，那么还是可以选择Btree算法，因为它支持一个主键和一个记录号同时存取。)<!--more-->

Btree中的主键是有序存储，记录间的关联是依靠次序。并且其结构能随数据的插入和删除进行动态调整。为了代码的简单，DB没有实现对关键字的前缀码压缩。Btree支持对数据查询、插入、删除的常数级速度。关键字可以为任意的数据结构。 因此，当在主键有序时，Btree算法应该被使用。例如，如果主键是时间戳， 那么8点时间戳后面跟随的就是9点时间戳， 这种情况下，Btree算法一般是正确的选择。再来个例子：如果主键是名字，应用需要取出所有同姓的记录，那么Btree 存取方法同样是个好选择。

Hash 和 Btree 两种方式在小的数据集合上几乎没有性能的差别。不过，由于Hash使用的是扩展线性HASH算法（extended linear hashing），可以根据HASH表的增长进行适当的调整。所以当一个数据集合足够大且关键字为随机分布时，采用Hash算法比较好。

Queue 还是 Recno？  
当用记录号作为数据存取的主键时，应该使用 Queue和Recno存取方法。记录号由算法本身生成。实际上，这和关系型数据库中逻辑主键通常定义为int AUTO型是同一个概念。两者基本上都是建立在Btree算法之上，提供存储有序数据的接口。Queue的优势在于：由于其记录为定长，在插入操作时把记录插入到队列的尾部，所以速度最快，而且它执行上锁和并发处理的水平也相当高。 Recno 的长处在于它支持一些Queue不能实现的特征，比如可变长记录和支持flat-text文件。

记录号可以是可变的或者不变的： 可变指的是当记录被删除或者插入记录号发生变化；不变指的是记录号无论数据库如何操作，记录号都不会发生改变。&nbsp;基于记录号存取在Btree方式下也是可行的。但是，记录号是可变，当记录删除或插入时，数据库内的其他记录的记录号都将发生改变。 Queue存取方法总是用固定的方式运行，不管数据库如何操作，记录号始终改变。 Recno 可以被设置为不变和可变两种形式。

另外，Recno为数据库提供支持flat-text文件的永久存储和数据在读或修改时提供一个快速的临时存储空间。

## Choose Database Access Method

| **Access Method** | **Description** | **Choosing Occasion** |
| B+树 | 关键字有序存储，并且其结构能随数据的插入和删除进行动态调整。为了代码的简单，Berkeley DB没有实现对关键字的前缀码压缩。B+树支持对数据查询、插入、删除的常数级速度。关键字可以为任意的数据结构。 | 1、&nbsp;当Key为复杂类型时。

2、&nbsp;当Key有序时。

 |
| Hash | DB中实际使用的是扩展线性HASH算法（extended linear hashing），可以根据HASH表的增长进行适当的调整。关键字可以为任意的数据结构。 | 1、&nbsp;当Key为复杂类型。

2、&nbsp;当数据较大且key随机分布时。

&nbsp;

 |
| Recno | 要求每一个记录都有一个逻辑纪录号，逻辑纪录号由算法本身生成。相当于关系数据库中的自动增长字段。Recho建立在B+树算法之上，提供了一个存储有序数据的接口。记录的长度可以为定长或不定长。 | 1、&nbsp;当key为逻辑记录号时。

2、&nbsp;当非高并发的情况下。

 |
| Queue | 和Recno方式接近,&nbsp;只不过记录的长度为定长。数据以定长记录方式存储在队列中，插入操作把记录插入到队列的尾部，相比之下插入速度是最快的。 | 1、当key为逻辑记录号时。

2、&nbsp;定长记录。

3、&nbsp;高并发的情况下。

&nbsp;

 |

来源：http://hi.baidu.com/xinzsky/blog/item/0652048176a794ddbd3e1ec5.html

