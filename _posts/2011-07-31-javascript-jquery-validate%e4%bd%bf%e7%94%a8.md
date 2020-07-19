---
layout: post
title: Javascript, JQuery, Validate使用
date: 2011-07-31 13:44:04.000000000 -07:00
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
  bot_views: '5'
  views: '2786'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/330.html"
---
js实现页面跳转的几种方式  
第一种：  
[cc lang="javascript"]  
<script type="text/javascript" language="javascript">// <![CDATA[<br />
   window.location.href="login.jsp?backurl="+window.location.href;<br />
// ]]></script>  
[/cc]

第二种：  
[cc lang="javascript"]  
<script type="text/javascript" language="javascript">// <![CDATA[<br />
 alert("返回"); window.history.back(-1);<br />
// ]]></script>  
[/cc]

第三种：  
[cc lang="javascript"]  
<script type="text/javascript" language="javascript">// <![CDATA[<br />
 window.navigate("top.jsp");<br />
// ]]></script>  
[/cc]

<!--more-->

第四种  
[cc lang="javascript"]  
<script type="text/javascript" language="JavaScript">// <![CDATA[<br />
 self.location='top.htm';<br />
// ]]></script>  
[/cc]

第五种：  
[cc lang="javascript"]  
<script type="text/javascript" language="javascript">// <![CDATA[<br />
 alert("非法访问！"); top.location='xx.jsp';<br />
// ]]></script>  
[/cc]

新版的jQuery使用方便很多，只需要在需要验证的字段上添加class属性，属性值可以为required,number,email等，同时可以设置minlength等属性。  
**JQuery验证实例：**

[cc lang="javascript"]

<form id="commentForm" action="" method="get">
<fieldset>
<legend>A simple comment form with submit validation and default messages</legend>
<p><label for="cname">Name</label><br>
<em>*</em></p>
<p><input id="cname" type="text" name="name" size="25"><label for="cemail">E-Mail</label><br>
<em>*</em></p>
<p><input id="cemail" type="text" name="email" size="25"><label for="curl">URL</label><br>
<em></em></p>
<p><input id="curl" type="text" name="url" size="25"><label for="ccomment">Your comment</label><br>
<em>*</em><textarea id="ccomment" name="comment" cols="22"></textarea></p>
<p><input type="submit" value="Submit"></p>
</fieldset>
</form>

&nbsp;

[/cc]

**自己使用到的一些js代码：** 右键另存为，下载

[setday.js](http://www.404story.com/wp-content/uploads/2011/07/setday.js)&nbsp;日历js代码

[function.js](http://www.404story.com/wp-content/uploads/2011/07/function.js)&nbsp;省市对应选择框js代码，弹出验证提示函数

JQuery官方代码：

[jquery-1.6.2.js](http://www.404story.com/wp-content/uploads/2011/07/jquery-1.6.2.js)&nbsp;官方目前最新的版本

[jquery.validate.js](http://www.404story.com/wp-content/uploads/2011/07/jquery.validate.js)&nbsp;验证最新版本

