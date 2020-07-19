---
layout: post
title: CallableStatement 使用实例
date: 2011-03-28 00:34:54.000000000 -07:00
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
  views: '1532'
  bot_views: '3'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/282.html"
---
/\*\*  
\* CallableStatement使用  
\*/  
package com.testjdbc.jdbc;

import java.sql.CallableStatement;  
import java.sql.Connection;  
import java.sql.Date;  
import java.sql.DriverManager;  
import java.sql.SQLException;  
import java.sql.Types;

/\*\*  
\* create date: 2011-3-26 下午03:30:06  
\*  
\* @author Tao  
\*  
\*/  
public class TestCallableStatement {  
&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp; private Connection conn;  
&nbsp;&nbsp;&nbsp; private CallableStatement cstmt;  
&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp; private String driver = "oracle.jdbc.OracleDriver";  
&nbsp;&nbsp;&nbsp; private String url = "jdbc:oracle:thin:@127.0.0.1:1521:orcl";  
<!--more-->  
&nbsp;&nbsp;&nbsp; /\*\*  
&nbsp;&nbsp;&nbsp;&nbsp; \*   
&nbsp;&nbsp;&nbsp;&nbsp; \*/  
&nbsp;&nbsp;&nbsp; public TestCallableStatement() {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // TODO Auto-generated constructor stub  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; try {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Class.forName(driver);  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; conn = DriverManager.getConnection(url, "ty", "ty");  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; } catch (ClassNotFoundException e) {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // TODO Auto-generated catch block  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; e.printStackTrace();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; } catch (SQLException e) {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // TODO Auto-generated catch block  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; e.printStackTrace();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }  
&nbsp;&nbsp;&nbsp; }  
&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp; public void useAdddatatest3(){  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; try {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt = conn.prepareCall("{call adddatatest3(?,?,?,?,?)}");  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.setInt(1, 3);  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.setString(2, "mark");  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.setDouble(3, 6000);  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.setDate(4, Date.valueOf("2010-10-10"));  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.setDate(5, Date.valueOf("2001-10-10"));  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; int i = cstmt.executeUpdate();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; System.out.println(i);  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; } catch (SQLException e) {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // TODO Auto-generated catch block  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; e.printStackTrace();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }  
&nbsp;&nbsp;&nbsp; }  
&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp; public void useGetArea(){  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; try {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt = conn.prepareCall("{call get\_area(?,?,?)}");  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.setInt(1, 20);  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.setInt(2, 30);  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.registerOutParameter(3, Types.DOUBLE);  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; cstmt.execute();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; System.out.println(cstmt.getDouble(3));  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; } catch (SQLException e) {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // TODO Auto-generated catch block  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; e.printStackTrace();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }  
&nbsp;&nbsp;&nbsp; }  
&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp; /\*\*  
&nbsp;&nbsp;&nbsp;&nbsp; \* 资源释放  
&nbsp;&nbsp;&nbsp;&nbsp; \*/  
&nbsp;&nbsp;&nbsp; public void close(){  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; if(conn != null){  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; try {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; conn.close();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; } catch (SQLException e) {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // TODO Auto-generated catch block  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; e.printStackTrace();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp; }

&nbsp;&nbsp;&nbsp; /\*\*  
&nbsp;&nbsp;&nbsp;&nbsp; \* @param args  
&nbsp;&nbsp;&nbsp;&nbsp; \*/  
&nbsp;&nbsp;&nbsp; public static void main(String[] args) {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; // TODO Auto-generated method stub  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; TestCallableStatement tcs = new TestCallableStatement();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //tcs.useAdddatatest3();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; tcs.useGetArea();  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; tcs.close();  
&nbsp;&nbsp;&nbsp; }

}

