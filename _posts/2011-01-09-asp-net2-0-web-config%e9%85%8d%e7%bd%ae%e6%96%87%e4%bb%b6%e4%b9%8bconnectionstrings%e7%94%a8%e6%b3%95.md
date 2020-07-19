---
layout: post
title: Asp.Net2.0 web.config配置文件之connectionStrings用法
date: 2011-01-09 14:01:58.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Skills
tags: []
meta:
  _wp_old_slug: ''
  _edit_last: '1'
  views: '2371'
  bot_views: '6'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/269.html"
---
以前写Asp.net代码，用的Web.Config配置文件中连接字符串多是&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<appSettings\>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<add key="ConnectionString" value="Server=.;Integrated Security=SSPI;Database=Message;" /\>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \</appSettings\>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 在Asp.Net 2.0 中新加了\<connectionStrings\>这一节

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<connectionStrings \>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<add /\>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<clear /\>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<remove /\>  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \</connectionStrings\>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 现在用起来就方便些了

<!--more-->

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<connectionStrings\>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<add name="Sales"  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; providerName="System.Data.SqlClient"  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; connectionString= "server=myserver;database=Products;uid=salesUser;pwd=sellMoreProducts" /\>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \</connectionStrings\>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 使用时，只需要如下即可：

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; System.Configuration.ConfigurationManager.ConnectionStrings["Sales"]

