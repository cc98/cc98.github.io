---
layout: post
title: ENCTYPE="multipart/form-data"
date: 2010-08-17 18:37:33.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Labrary
tags: []
meta:
  _wp_old_slug: ''
  _edit_last: '1'
  views: '2196'
  bot_views: '4'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/134.html"
---
用于表单里有图片上传。

\<code\>\<form name="userInfo" method="post" action="first\_submit.jsp" ENCTYPE="multipart/form-data"\>

表单标签中设置enctype="multipart/form-data"来确保匿名上载文件的正确编码。

如下：

\<tr\>

\<td height="30" align="right"\>上传图片：\</td\>

\<td\>\<INPUT TYPE="FILE" NAME="uploadfile" SIZE="34" onChange="checkimage()"\>\</td\>

\</tr\>

\</code\>

就得加ENCTYPE="multipart/form-data"。

表单中enctype="multipart/form-data"的意思，是设置表单的MIME编码。默认情况，这个编码格式是application/x-www-form-urlencoded，不能用于文件上传；只有使用了multipart/form-data，才能完整的传递文件数据，进行下面的操作.

enctype="multipart/form-data"是上传二进制数据; form里面的input的值以2进制的方式传过去。

form里面的input的值以2进制的方式传过去，所以request就得不到值了。 也就是说加了这段代码,用request就会传递不成功,

取表单值加入数据库时，用到下面的：

SmartUpload su = new SmartUpload();//新建一个SmartUpload对象

su.getRequest().getParameterValues();取数组值

su.getRequest().getParameter( );取单个参数单个值

