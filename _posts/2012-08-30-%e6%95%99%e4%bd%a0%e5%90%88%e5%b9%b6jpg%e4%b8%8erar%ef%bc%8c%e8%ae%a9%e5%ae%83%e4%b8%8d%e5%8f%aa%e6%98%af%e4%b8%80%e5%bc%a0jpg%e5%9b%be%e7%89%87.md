---
layout: post
title: 教你合并jpg与rar，让它不只是一张jpg图片
date: 2012-08-30 22:39:16.000000000 -07:00
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
  bot_views: '5'
  views: '2085'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/723.html"
---
先来个福利：Windows 8 激活信息备份还原工具，把图片另存为rar打开解压就行。

[![]({{ site.baseurl }}/assets/images/tool.png "tool")](http://www.404story.com/labrary/723.html/attachment/tool)

&nbsp;

### <!--more-->制作方法：

首先确保你的系统可以直接查看文件的扩展名，设置方法如下：

[![]({{ site.baseurl }}/assets/images/11.jpg "11")](http://www.404story.com/labrary/723.html/attachment/11)

### **方法一**

　　1、找一张JPG格式的图片。

　　2、把你要隐藏的文件打包成一个RAR压缩文件（右击文件，选择“添加到压缩文件”）。

　　3、把JPG图片与RAR文件放到硬盘的任意根目录下（我是D盘），文件的命名为1.JPG和2.RAR。

　　4、点击“开始”菜单，在“运行”输入栏处，输入CMD就可以打开命令提示符。

　　5、输入命令“cd /”，再输入“d:”进入D盘根目录，输入“dir”可以看到我们要用的文件1.JPG和2.RAR。

　　6、输入“COPY /B 1.JPG+2.RAR 3.JPG”，回车后可以在D盘看到生成的合并文件3.JPG。

　　（此方法也可用于其它类型的文件的合并，只要文件名相对应即可，当然，也可以合并许多的文件，只要你不断的+++++就可以）

### **方法二**

用百度搜索“JPG+RAR合并器”，使用软件自动合并文件。（这个操作比较简单，但是不大安全）

