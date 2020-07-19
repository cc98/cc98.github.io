---
layout: post
title: git pull / git push 记住密码方法（ssh记住密码）
date: 2012-09-29 14:05:55.000000000 -07:00
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
  bot_views: '15'
  views: '9836'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/816.html"
---
备注： 适用于Linux/Mac OS等。

有没有觉得，每次git pull 或git push的时候，都需要重新输入密码，很麻烦。搜了下找到一种方法记住ssh连接的密码，同时把Git repository的密码保存下来，下面就来一步一步做吧。。

#### 1. 首先是保存密码输入问题，需要创建密钥，在你的命令行输入：

local:~ yourname$&nbsp;&nbsp; **ssh-keygen -t rsa**

然后依次回车，输入密码，这个密码和SSH的帐号密码无关。

<!--more-->

Generating public/private rsa key pair.  
Enter file in which to save the key (/u/kim/.ssh/id\_rsa):&nbsp;【回车】  
Enter passphrase (empty for no passphrase):&nbsp;【第一次密码】  
Enter same passphrase again:&nbsp;【第二次密码】  
Your identification has been saved in /u/kim/.ssh/id\_rsa.  
Your public key has been saved in /u/kim/.ssh/id\_rsa.pub.

#### 2. 接下来把密钥文件内容上传到的SSH帐号下:

local:~ yourname$&nbsp; **cat ~/.ssh/id\_rsa.pub&nbsp; | ssh username@yourhost 'cat \>\> .ssh/authorized\_keys'**

#### 3. 最后一步测试

local:~ yourname$&nbsp; **ssh username@yourhost.com**

如果此时不需要你输入密码，那么恭喜你设置成功了。现在你再执行git pull 或git push就不需要输入密码了。

参考：[Store your git https passwords in your OS X Keychain](http://samuel.kadolph.com/2011/03/store-your-git-https-passwords-in-your-os-x-keychain/)

&nbsp;

ps： 如果更换主机ip地址等，会出现ssh的一个提示，去除这个提示，请使用：

#### ssh-keygen -f &nbsp;~/.ssh/known\_hosts -R NewIP

&nbsp;

&nbsp;

## 对于另外一种每次需要输入用户和密码git账户，比如github。用以下方法

若想让 Git 使用 osxkeychain，可以在 Git 的全局设置中进行设置：

```
\<code\>$ git config --global credential.helper osxkeychain # Set git to use the osxkeychain credential helper \</code\>
```

经过这样的设置之后，下次再克隆 HTTPS 地址时会询问你的用户名和密码，并授权给 OSX keychain。完成这些之后你的用户名和密码就会存储到 keychain 中，再也不会在 Git 中询问了。

