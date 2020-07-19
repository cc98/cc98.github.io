---
layout: post
title: How to use Map/List in playframework template
date: 2013-03-26 20:13:08.000000000 -07:00
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
  bot_views: '6'
  views: '2598'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/solutions/932.html"
---
To be even more specific, I wish to access the Map as I iterate over a List of objects, e.g.,

```java
#{list items:itemList, as:'item'} // access the map value using the ${item?.id} as the key #{/list}
```

but how to use Map like HashMap, TreeMap to play framework template?<!--more-->

This is a&nbsp; **generic solution** &nbsp;to iterate on&nbsp;_Map_&nbsp;in using Play! Framework:

in the controller :

```java
render(map);
```

in the template:

```java
#{list items:map.keySet(), as:'key'} ${map.get(key)} #{/list}
```

&nbsp;

The fact that you want to rely on a side&nbsp;_List_&nbsp;to iterate on your&nbsp;_Map_&nbsp;suggest me that you are searching a predictible way for your iteration process.

In that case, just remember that iteration will be unpredictable if you don't use an ordered/sorted&nbsp;_Map_implementation.

&nbsp;

- **HashMap** &nbsp;gives you an&nbsp; **unsorted** ,&nbsp; **unordered** &nbsp;_Map_
- **LinkedHashMap** &nbsp;maintains&nbsp; **insertion order**
- **TreeMap** &nbsp;is the only JDK implementation of a&nbsp; **sorted** &nbsp;_Map_. By default it allows you to iterate following the&nbsp; **natural order** &nbsp;of the elements. You can also specify a custom sort order and implements the&nbsp;**[Comparable](http://download.oracle.com/javase/6/docs/api/java/lang/Comparable.html)**&nbsp;interface. This will lead you to override the&nbsp;_compareTo()_&nbsp;method.

&nbsp;

&nbsp;

