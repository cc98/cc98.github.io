---
layout: post
title: Java HashMap按value排序方法
date: 2012-10-31 16:01:52.000000000 -07:00
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
  bot_views: '3'
  views: '2526'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/828.html"
---
Java HashMap按value排序方法，代码如下：

```java
public static void main(String[] args) { List\<Map.Entry\<String, Integer\>\> list = new ArrayList\<Map.Entry\<String, Integer\>\>(area2no.entrySet()); Collections.sort(list, new Comparator\<Map.Entry\<String, Integer\>\>() { public int compare(Entry\<String, Integer\> arg0, Entry\<String, Integer\> arg1) { return arg0.getValue() - arg1.getValue(); } }); for(int i=0; i\< list.size(); i++){ Entry\<String, Integer\> entry = list.get(i); System.out.println(entry.getKey() + "("" + entry.getKey() + "", " + entry.getValue() + ", "" + map.get(entry.getKey()) + ""),"); } }
```
