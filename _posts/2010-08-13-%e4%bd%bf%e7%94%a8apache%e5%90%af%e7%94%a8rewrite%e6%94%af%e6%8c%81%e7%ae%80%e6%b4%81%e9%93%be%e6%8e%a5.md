---
layout: post
title: 使用Apache启用Rewrite支持简洁链接
date: 2010-08-13 13:27:07.000000000 -07:00
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
  _wp_old_slug: ''
  views: '1906'
  bot_views: '5'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/125.html"
---
主要将AllowOverride None改成AllowOverride All

\<Directory 远程目标目录\>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Options Indexes FollowSymLinks MultiViews  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AllowOverride All  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Order allow,deny  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; allow from all  
\</Directory\>

mod\_rewrite 参考：[http://lamp.linux.gov.cn/Apache/ApacheMenu/mod/mod\_rewrite.html](http://lamp.linux.gov.cn/Apache/ApacheMenu/mod/mod_rewrite.html)

