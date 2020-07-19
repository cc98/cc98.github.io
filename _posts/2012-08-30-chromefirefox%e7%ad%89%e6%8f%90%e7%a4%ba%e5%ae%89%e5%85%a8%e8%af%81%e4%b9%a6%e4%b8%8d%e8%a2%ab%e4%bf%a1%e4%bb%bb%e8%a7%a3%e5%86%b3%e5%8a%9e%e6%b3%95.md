---
layout: post
title: Chrome/Firefox等提示“安全证书不被信任”解决办法
date: 2012-08-30 22:24:11.000000000 -07:00
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
  bot_views: '7'
  views: '12835'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/742.html"
---
使用GoAgent等软件时，在Chrome/Firefox等浏览器浏览时，会出现 **“the site's security certificate is not trusted”** ，导致网站不能访问，这就需要手工添加信任证书。

> GoAgent 项目主页：&nbsp;[http://code.google.com/p/goagent/](http://code.google.com/p/goagent/)
> 
> Goagent 是一个使用 Python 和 Google Appengine SDK 编写的代理软件
> 
> 可以运行在Windows/Mac/Linux/Andorid/iTouch/iPhone/iPad上

GoAgent 的配置方法很简单，需要拥有一个&nbsp;[Google 帐号](http://mail.google.com/)，然后[申请一个 GAE 空间](http://code.google.com/appengine/)，第一次申请 GAE 空间时需要用手机接收短信验证码。具体的操作可以参考 GoAgent 项目主页。

![]({{ site.baseurl }}/assets/images/trans.gif "More...")<!--more-->

如果你在使用 GoAgent 时遇到证书不被信任问题，请按以下方法解决，以Chrome为例，Firefox等同理：

**Ubuntu 系统：**

- 打开 Chrome 浏览器
- 首选项 \> 高级选项 \>&nbsp; **管理证书…**
- 在&nbsp; **授权中心** &nbsp;导入 GoAgent/local 目录下的 CA.crt 证书  
（注意不要导入到&nbsp; **服务器 ，否则不起作用** ）
- 在 授权中心 找到&nbsp; **GoAgent CA** &nbsp;并点击&nbsp; **修改…**
- 修改信任设置为全部选中
- 重启浏览器

**Windows 系统：**

- 打开 Chrome 浏览器
- 选项 \> 高级选项 \> 管理证书…
- 导入证书 \> 下一步 \> 选择 GoAgent/local 目录下的 CA.crt 证书 \> 下一步 \> 选择 证书存储： **浏览…** &nbsp;\>&nbsp; **受信任的根证书颁发机构** &nbsp;\> 下一步 … \> 完成 （注意一定要选择 **受信任的根证书颁发机构** ）
- 重启浏览器

**MAC 系统：**

- 双击 GoAgent/local 目录下的 CA.crt 证书导入到系统
- 在 Launchpad \> 实用工具 \> 钥匙串访问 \> 系统 中找到 GoAgent CA 并双击
- **选择 信任 \> 使用此证书时 \> 总是信任**
- 重启浏览器
