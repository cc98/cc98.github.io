---
layout: post
title: Mac OS X添加PATH环境变量
date: 2012-07-22 13:21:28.000000000 -07:00
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
  bot_views: '2'
  views: '3677'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/575.html"
---
解决办法:  
sudo vim /etc/paths

将路径添加到里面去， 一行一个路径

注意：即便添加成功，未必运行成功；在制定路径下得脚本必须具是executable, 否则就会被在搜索时被忽略。  
sudo chmod +x XXX

而在Ubuntu下，则只需要修改/etc/.profile或者 ~/.profile或~/.bashrc等修改

