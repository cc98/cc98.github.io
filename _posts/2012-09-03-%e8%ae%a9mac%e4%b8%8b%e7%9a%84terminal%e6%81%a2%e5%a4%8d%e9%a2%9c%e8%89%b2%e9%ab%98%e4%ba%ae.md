---
layout: post
title: 让Mac终端terminal颜色高亮
date: 2012-09-03 14:37:49.000000000 -07:00
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
  bot_views: '2'
  views: '3482'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/772.html"
---
 **针对terminal采用bash模式:**

1. 编辑 ~/.bash\_profile, 加入以下代码:
```
export CLICOLOR=1 export LSCOLORS=gxfxaxdxcxegedabagacad
```
2. 保存,然后重启terminal,搞定,恢复正常了.

<!--more-->

**详细讲解代码中的涵义:**

1. CLICOLOR: 前景色和背景色的字符串合并值
2. LSCOLORS: 对于不同变量所采用的颜色方案,具体看如下表格:  
a &nbsp; &nbsp; &nbsp; black  
b &nbsp; &nbsp; &nbsp; red  
c&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; green  
d&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; brown  
e &nbsp; &nbsp; &nbsp; blue  
f&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; magenta  
g&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cyan  
h&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; light grey  
A&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; bold black, usually shows up as dark grey  
B&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; bold red  
C&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; bold green  
D&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; bold brown, usually shows up as yellow  
E&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; bold blue  
F&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; bold magenta  
G&nbsp;&nbsp;&nbsp;&nbsp; bold cyan  
H&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; bold light grey; looks like bright white  
x&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; default foreground or background  
而文件类型列表如下:  
1. directory  
2. symbolic link  
3. socket  
4. pipe  
5. executable  
6. block special  
7. character special  
8. executable with setuid bit set  
9. executable with setgid bit set  
10. directory writable to others, with sticky bit  
11. directory writable to others, without sticky

所以对照这张表就可以得知:

```
gxfxaxdxcxegedabagacad
```

就是对于directory而言,它的前景色就是: g(cyan),而背景色就是:x(默认的背景色).

