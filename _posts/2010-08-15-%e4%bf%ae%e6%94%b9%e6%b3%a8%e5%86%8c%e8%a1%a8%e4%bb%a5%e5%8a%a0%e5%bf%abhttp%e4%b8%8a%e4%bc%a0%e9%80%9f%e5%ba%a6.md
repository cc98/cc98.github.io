---
layout: post
title: 修改注册表以加快HTTP上传速度
date: 2010-08-15 19:24:34.000000000 -07:00
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
  _wp_old_slug: ''
  views: '6057'
  bot_views: '13'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/solutions/132.html"
---
使用HTTP协议上传比较大的文件档案，比如通过Web方式在邮箱里发送包含交大附件的邮件，附件上传的时间往往会拖很久。微软表示这与带宽无关，而是因为系统Winsock默认的传送缓冲区太小了（只有8KB）。只要修改一下缓冲区大小，HTTP龟速上传的情况就可以大大改观。  
修改的方法很简单，打开注册表后，定位分支〔HKEY\_CURRENT\_USERSoftwareMicrosoftWindowsCurrentVersionInternet Settings〕  
然后在右侧窗口里的空白处，右键单击，新建一名为 "SocketSendBufferLength"的DWORD值，然后“数值数据”输入“4000”（十六进制，即16KB），点击确认保存修改。最后重启电脑即可将winsock默认的传送缓冲区设置为16KB。

