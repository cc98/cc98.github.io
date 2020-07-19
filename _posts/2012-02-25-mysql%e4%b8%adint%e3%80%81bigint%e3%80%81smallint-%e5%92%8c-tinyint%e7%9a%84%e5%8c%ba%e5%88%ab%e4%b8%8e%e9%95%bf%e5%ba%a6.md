---
layout: post
title: mysql中int、bigint、smallint 和 tinyint的区别与长度
date: 2012-02-25 18:09:29.000000000 -08:00
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
  bot_views: '9'
  views: '39945'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/426.html"
---
各种整形，总结留作参考。

**bigint**

从 -2^63 (-9223372036854775808) 到 2^63-1 (9223372036854775807) 的整型数据（所有数字）。存储大小为 8 个字节。

**int**

从 -2^31 (-2,147,483,648) 到 2^31 – 1 (2,147,483,647) 的整型数据（所有数字）。存储大小为 4 个字节。 **int&nbsp;** 的 SQL-92 同义字为&nbsp; **integer** 。

**smallint**

从 -2^15 (-32,768) 到 2^15 – 1 (32,767) 的整型数据。存储大小为 2 个字节。

**tinyint**

从 0 到 255 的整型数据。存储大小为 1 字节。

&nbsp;

在支持整数值的地方支持&nbsp; **bigint** &nbsp;数据类型。但是， **bigint** &nbsp;用于某些特殊的情况，当整数值超过&nbsp; **int** &nbsp;数据类型支持的范围时，就可以采用&nbsp; **bigint** 。在 SQL Server 中， **int** &nbsp;数据类型是主要的整数数据类型。

在数据类型优先次序表中， **bigint** &nbsp;位于&nbsp; **smallmoney** &nbsp;和&nbsp; **int** &nbsp;之间。

只有当参数表达式是&nbsp; **bigint** &nbsp;数据类型时，函数才返回&nbsp; **bigint** 。SQL Server 不会自动将其它整数数据类型（ **tinyint** 、 **smallint** &nbsp;和&nbsp; **int** ）提升为&nbsp; **bigint** 。

int(M) 在 integer 数据类型中，M 表示最大显示宽度。在 int(M) 中，M 的值跟 int(M) 所占多少存储空间并无任何关系。和数字位数也无关系 int(3)、int(4)、int(8) 在磁盘上都是占用 4 btyes 的存储空间。

