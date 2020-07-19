---
layout: post
title: Java无数据源连接Access解决方案，获取mdb相对路径
date: 2011-09-09 16:06:41.000000000 -07:00
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
  bot_views: '2'
  views: '2709'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/391.html"
---
[cc lang="java"]  
package mytest;

import java.sql.\*;

import java.io.\*;

import java.net.\*;

public class AccessDBConn {

private Connection conn = null;

private File file = null;

private URL url = null; //之所以要用URL是因为可以通过file.toURI()得到含有空格的地址。

public Connection AccessDBConn() {

String driver="sun.jdbc.odbc.JdbcOdbcDriver";

//获得数据库的真实路径

String dburl = String.valueOf(Thread.currentThread().getContextClassLoader().getResource(""));

dburl = dburl + "../../family.mdb";//得到文件的URL: 'file:/C:...'

try{

url=new URL(dburl);

file=new File(url.toURI()); //用toURI()就解决空格问题。

}catch(Exception e){}

dburl = file.toString(); //绝对路径

String accessUrl="jdbc:odbc:Driver={Microsoft Access Driver (\*.mdb)};DBQ="+dburl;

try{

Class.forName(driver);

conn = DriverManager.getConnection(accessUrl);

}catch(Exception e){

e.printStackTrace();}

return conn;

}

public static void main (String[] args) {

AccessDBConn dbc= new AccessDBConn();

dbc.AccessDBConn();

}

}  
[/cc]

