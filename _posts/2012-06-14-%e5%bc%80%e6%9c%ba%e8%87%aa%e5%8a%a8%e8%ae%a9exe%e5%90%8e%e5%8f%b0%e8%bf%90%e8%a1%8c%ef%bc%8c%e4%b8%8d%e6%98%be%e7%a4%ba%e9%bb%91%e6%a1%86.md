---
layout: post
title: 开机自动让exe后台运行，不显示黑框
date: 2012-06-14 02:06:02.000000000 -07:00
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
  bot_views: '4'
  views: '3749'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/530.html"
---
通过两步实现，比如你需要执行proxy.exe。

1、添加.bat文件，使用start命令启动proxy.exe，/b表示后台运行，代码如下，保存为start.bat

```bash
start /b D:Downloadsgoagentlocalproxy.exe \> D:Downloadsgoagentlocalproxy.log
```

2、使用vbs来执行.bat文件，使用代码如下，保存为start.vbs

```vb
DIM objShell set objShell=wscript.createObject("wscript.shell") iReturn=objShell.Run("start.bat", 0, TRUE)
```

3、添加开机自动启动项，有两种方法

第一种，将start.vbs拖到 **开始菜单\>附件\>启动** 中，开机就会自动运行这个vbs

第二种，在 **开始\>运行** 运行 **regedit** 打开注册表，找到 **HKEY\_CURRENT\_USERSoftwareMicrosoftWindowsCurrentVersionRun** ，在这里添加启动项start.vbs

&nbsp;

