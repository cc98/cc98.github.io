---
layout: post
title: PHP如何创建Session
date: 2010-09-30 19:33:22.000000000 -07:00
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
  _wp_old_slug: ''
  views: '3384'
  bot_views: '7'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/173.html"
---
　　开始介绍如何创建 session。非常简单，真的。

　　启动 session 会话，并创建一个 $admin 变量：

　　// 启动 session

　　session\_start();

　　// 声明一个名为 admin 的变量，并赋空值。

　　$\_session["admin"] = null;

　　?\><!--more-->

　　如果你使用了 Seesion，或者该 PHP 文件要调用 Session 变量，那么就必须在调用 Session 之前启动它，使用 session\_start() 函数。其它都不需要你设置了，PHP 自动完成 session 文件的创建。

　　执行完这个程序后，我们可以到系统临时文件夹找到这个 session 文件，一般文件名形如：sess\_4c83638b3b0dbf65583181c2f89168ec，后面是 32 位编码后的随机字符串。用编辑器打开它，看一下它的内容：

　　admin|N;

一般内容结构：

　　变量名|类型:长度:值;

　　并用分号隔开每个变量。有些是可以省略的，比如长度和类型。

　　我们来看一下验证程序，假设数据库存储的是用户名和 md5 加密后的密码：

　　// 表单提交后...

　　$posts = $\_POST;

　　// 清除一些空白符号

　　foreach ($posts as $key =\> $value)

　　{

　　$posts[$key] = trim($value);

　　}

　　$password = md5($posts["password"]);

　　$username = $posts["username"];

　　$query = "SELECT `username` FROM `user` WHERE `password` = '$password'";

　　// 取得查询结果

　　$userInfo = $DB-\>getRow($query);

　　if (!empty($userInfo))

　　{

　　if ($userInfo["username"] == $username)

　　{

　　// 当验证通过后，启动 session

　　session\_start();

　　// 注册登陆成功的 admin 变量，并赋值 true

　　$\_session["admin"] = true;

　　}

　　else

　　{

　　die("用户名密码错误");

　　}

　　}

　　else

　　{

　　die("用户名密码错误");

　　}

　　我们在需要用户验证的页面启动 session，判断是否登陆：

　　// 防止全局变量造成安全隐患

　　$admin = false;

　　// 启动会话，这步必不可少

　　session\_start();

　　// 判断是否登陆

　　if (isset($\_SESSION["admin"]) && $\_session["admin"] === true)

　　{

　　echo "您已经成功登陆";

　　}

　　else

　　{

　　// 验证失败，将 $\_session["admin"] 置为 false

　　$\_session["admin"] = false;

　　die("您无权访问");

　　}

　　?\>

　　是不是很简单呢?将 $\_session 看成是存储在服务器端的数组即可，我们注册的每一个变量都是数组的键，跟使用数组没有什么分别。

　　如果要登出系统怎么办?销毁 session 即可。

　　\<?php

　　session\_start();

　　// 这种方法是将原来注册的某个变量销毁

　　unset($\_session["admin"]);

　　// 这种方法是销毁整个 session 文件

　　session\_destroy();

　　?\>

　　Session 能否像 Cookie 那样设置生存周期呢?有了 Session 是否就完全抛弃 Cookie 呢?我想说，结合 Cookie 来使用 session 才是最方便的。

　　Session 是如何来判断客户端用户的呢?它是通过 Session ID 来判断的，什么是 Session ID，就是那个 Session 文件的文件名，Session ID 是随机生成的，因此能保证唯一性和随机性，确保 Session 的安全。一般如果没有设置 Session 的生存周期，则 Session ID 存储在内存中，关闭浏览器后该 ID 自动注销，重新请求该页面后，重新注册一个 session ID。

　　如果客户端没有禁用 Cookie，则 Cookie 在启动 Session 会话的时候扮演的是存储 Session ID 和 session 生存期的角色。

　　我们来手动设置 session 的生存期：

　　session\_start();

　　// 保存一天

　　$lifeTime = 24 \* 3600;

　　setcookie(session\_name(), session\_id(), time() + $lifeTime, "/");

　　?\>

　　其实 Session 还提供了一个函数 session\_set\_cookie\_params(); 来设置 Session 的生存期的，该函数必须在 session\_start() 函数调用之前调用：

　　// 保存一天

　　\<?php

　　$lifeTime = 24 \* 3600;

　　session\_set\_cookie\_params($lifeTime);

　　session\_start();

　　$\_session["admin"] = true;

　　?\>

　　如果客户端使用 IE 6.0 ， session\_set\_cookie\_params(); 函数设置 Cookie 会有些问题，所以我们还是手动调用 setcookie 函数来创建 cookie。

　　假设客户端禁用 Cookie 怎么办?没办法，所有生存周期都是浏览器进程了，只要关闭浏览器，再次请求页面又得重新注册 Session。那么怎么传递 Session ID 呢?通过 URL 或者通过隐藏表单来传递，PHP 会自动将 session ID 发送到 URL 上，URL 形如：http://www.openphp .cn /index.php?PHPSESSID=bba5b2a240a77e5b44cfa01d49cf9669，其中 URL 中的参数 PHPSESSID 就是 Session ID了，我们可以使用 $\_GET 来获取该值，从而实现 session ID 页面间传递。

　　// 保存一天

　　\<?php

　　$lifeTime = 24 \* 3600;

　　// 取得当前 session 名，默认为 PHPSESSID

　　$sessionName = session\_name();

　　// 取得 session ID

　　$sessionID = $\_GET[$sessionName];

　　// 使用 session\_id() 设置获得的 session ID

　　session\_id($sessionID);

　　session\_set\_cookie\_params($lifeTime);

　　session\_start();

　　$\_session["admin"] = true;

　　?\>

　　对于虚拟主机来说，如果所有用户的 Session 都保存在系统临时文件夹里，将给维护造成困难，而且降低了安全性，我们可以手动设置 Session 文件的保存路径，session\_save\_path()就提供了这样一个功能。我们可以将 session 存放目录指向一个不能通过 Web 方式访问的文件夹，当然，该文件夹必须具备可读写属性。

　　\<?php

　　// 设置一个存放目录

　　$savePath = "./session\_save\_dir/";

　　// 保存一天

　　$lifeTime = 24 \* 3600;

　　session\_save\_path($savePath);

　　session\_set\_cookie\_params($lifeTime);

　　session\_start();

　　$\_session["admin"] = true;

　　?\>

　　同 session\_set\_cookie\_params(); 函数一样，session\_save\_path() 函数也必须在 session\_start() 函数调用之前调用。

　　我们还可以将数组，对象存储在 session 中。操作数组和操作一般变量没有什么区别，而保存对象的话，PHP 会自动对对象进行序列化(也叫串行化)，然后保存于 session 中。下面例子说明了这一点：

　　\<?php

　　class person

　　{

　　var $age;

　　function output() {

　　echo $this-\>age;

　　}

　　function setAge($age) {

　　$this-\>age = $age;

　　}

　　}

　　?\>

　　setage.PHP

　　\<?php

　　session\_start();

　　require\_once "person.PHP";

　　$person = new person();

　　$person-\>setAge(21);

　　$\_session['person'] = $person;

　　echo "check here to output age";

　　?\>

　　output.PHP

　　\<?php

　　// 设置回调函数，确保重新构建对象。

　　ini\_set('unserialize\_callback\_func', 'mycallback');

　　function mycallback($classname) {

　　$classname . ".PHP";

　　}

　　session\_start();

　　$person = $\_session["person"];

　　// 输出 21

　　$person-\>output();

　　?\>

　　当我们执行 setage.php 文件的时候，调用了 setage() 方法，设置了年龄为 21，并将该状态序列化后保存在 session 中(PHP 将自动完成这一转换)，当转到 output.php 后，要输出这个值，就必须反序列化刚才保存的对象，又因为在解序列化的时候需要实例化一个未定义类，所以我们定义了以后回调函数，自动包含 person.PHP 这个类文件，因此对象被重构，并取得当前 age 的值为 21，然后调用 output() 方法输出该值。

