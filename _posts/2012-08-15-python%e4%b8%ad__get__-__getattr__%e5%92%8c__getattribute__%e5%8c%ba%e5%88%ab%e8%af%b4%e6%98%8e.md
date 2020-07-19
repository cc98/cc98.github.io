---
layout: post
title: python中__get__, __getattr__和__getattribute__区别说明
date: 2012-08-15 11:11:41.000000000 -07:00
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
  bot_views: '2'
  views: '2299'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/636.html"
---
\_\_get\_\_,\_\_getattr\_\_和\_\_getattribute都是访问属性的方法，但不太相同。  
object.\_\_getattr\_\_(self, name)  
当一般位置找不到attribute的时候，会调用getattr，返回一个值或AttributeError异常。

object.\_\_getattribute\_\_(self, name)  
无条件被调用，通过实例访问属性。如果class中定义了\_\_getattr\_\_()，则\_\_getattr\_\_()不会被调用（除非显示调用或引发AttributeError异常）

object.\_\_get\_\_(self, instance, owner)  
如果class定义了它，则这个class就可以称为descriptor。owner是所有者的类，instance是访问descriptor的实例，如果不是通过实例访问，而是通过类访问的话，instance则为None。（descriptor的实例自己访问自己是不会触发\_\_get\_\_，而会触发\_\_call\_\_，只有descriptor作为其它类的属性才有意义。）（所以下文的d是作为C2的一个属性被调用）

```python
class C(object): a = 'abc' def \_\_getattribute\_\_(self, \*args, \*\*kwargs): print("\_\_getattribute\_\_() is called") return object.\_\_getattribute\_\_(self, \*args, \*\*kwargs) # return "haha" def \_\_getattr\_\_(self, name): print("\_\_getattr\_\_() is called ") return name + " from getattr" def \_\_get\_\_(self, instance, owner): print("\_\_get\_\_() is called", instance, owner) return self def foo(self, x): print(x) class C2(object): d = C() if \_\_name\_\_ == '\_\_main\_\_': c = C() c2 = C2() print(c.a) print(c.zzzzzzzz) c2.d print(c2.d.a)
```

<!--more-->

**输出结果：**

```python
\_\_getattribute\_\_() is called abc \_\_getattribute\_\_() is called \_\_getattr\_\_() is called zzzzzzzz from getattr \_\_get\_\_() is called \<\_\_main\_\_.C2 object at 0x16d2310\> \<class '\_\_main\_\_.C2'\> \_\_get\_\_() is called \<\_\_main\_\_.C2 object at 0x16d2310\> \<class '\_\_main\_\_.C2'\> \_\_getattribute\_\_() is called abc
```

很多时候，您仅希望以某种特殊的方式使用少数属性，而其他属性则按照普通属性操作。这些普通属性不会触发任何特殊代码，也不会因为遍历方法代码而浪费时间。在这些情况下，您可以对属性使用_描述符_。或者，定义与描述符密切关联的_特性（property）_。实际上，特性和描述符基本是同一类东西，但是定义语法却截然不同。并且由于定义类型存在差别，正如您所料，特性和描述符各有优缺点。

&nbsp;

可以看出，每次通过 **实例** 访问属性，都会经过\_\_getattribute\_\_函数。而当属性不存在时，仍然需要访问\_\_getattribute\_\_，不过接着要访问\_\_getattr\_\_。这就好像是一个异常处理函数。  
每次访问descriptor（即实现了\_\_get\_\_的类），都会先经过\_\_get\_\_函数。

需要注意的是，当使用类访问不存在的变量是，不会经过\_\_getattr\_\_函数。而descriptor不存在此问题，只是把instance标识为none而已。

