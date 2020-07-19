---
layout: post
title: MySQL修改密码、忘记root密码修改方法
date: 2014-08-23 20:06:25.000000000 -07:00
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
  views: '586'
  wp_review_location: bottom
  _layout: inherit
  wp_review_color: "#1e73be"
  wp_review_fontcolor: "#555555"
  wp_review_bgcolor1: "#e7e7e7"
  wp_review_bgcolor2: "#ffffff"
  wp_review_bordercolor: "#e7e7e7"
  _thumbnail_id: '1142'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/1139.html"
---
本文整理了四种在MySQL中修改root密码的方法，希望对大家有所帮助。全部方法经过测试通过。

### 方法1： 用SET PASSWORD命令

首先登录MySQL。  
格式：mysql\> set password for 用户名@localhost = password('新密码');  
例子：mysql\> set password for root@localhost = password('404story.com');  
上面例子将用户root的密码更改为404story.com

### 方法2：用mysqladmin

格式：mysqladmin -u用户名 -p旧密码&nbsp;password 新密码  
例子：mysqladmin -uroot -p123456 password 404story.com  
上面例子将用户root原来的密码123456改为新密码404story.com

### 方法3：用UPDATE直接编辑user表

首先登录MySQL。  
mysql\> use mysql;  
mysql\>&nbsp;update user set password=password('404story.com')&nbsp;where user='root' and host='localhost';  
mysql\>&nbsp;flush privileges;

### 方法4：在忘记root密码的时候，可以这样。

以windows为例：  
1. 关闭正在运行的MySQL服务。  
2. 打开DOS窗口，转到mysql\bin目录。  
3. 输入mysqld --skip-grant-tables 回车。--skip-grant-tables&nbsp;的意思是启动MySQL服务的时候跳过权限表认证。  
4. 再开一个DOS窗口（因为刚才那个DOS窗口已经不能动了），转到mysql\bin目录。  
5. 输入mysql回车，如果成功，将出现MySQL提示符 \>。  
6. 连接权限数据库： use mysql; 。  
6. 改密码：update user set password=password("404story.com") where user="root";（别忘了最后加分号） 。  
7. 刷新权限（必须步骤）：flush privileges;　。  
8. 退出&nbsp; quit。  
9. 注销系统，再进入，使用用户名root和刚才设置的新密码404story.com登录。

