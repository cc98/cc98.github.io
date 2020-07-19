---
layout: post
title: Java编程 Swing模板
date: 2011-04-07 13:32:07.000000000 -07:00
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
  views: '2520'
  bot_views: '2'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/297.html"
---
1、创建框架：  
[cc lang="java"]  
import java.awt.\*;

import javax.swing.\*;

public class SimpleFrameTest {

public static void main(String[] args) {  
 // 事件调度线程  
 EventQueue.invokeLater(new Runnable() {  
 public void run() {  
 // 创建一个SimpleFrame窗体  
 SimpleFrame frame = new SimpleFrame();

// 默认关闭窗口时退出  
frame.setDefaultCloseOperation(JFrame.EXIT\_ON\_CLOSE);  
 // 设置窗体可见  
 frame.setVisible(true);  
 }  
 });  
 }  
}  
[/cc]  
<!--more-->

[cc lang="java"]  
class SimpleFrame extends JFrame {

// 构造函数

public SimpleFrame() {

setSize(DEFAULT\_WIDTH, DEFAULT\_HEIGHT);

}

// 声明默认窗体宽度

public static final int DEFAULT\_WIDTH = 300;

// 声明默认窗体高度

public static final int DEFAULT\_HEIGHT = 200;

}  
[/cc]  
2、框架定位：  
[cc lang="java"]

```
import java.awt.\*; import javax.swing.\*; public class SimpleFrameTest { public static void main(String[] args) { // 事件调度线程 EventQueue.invokeLater(new Runnable() { public void run() { // 创建一个SimpleFrame窗体 SimpleFrame frame = new SimpleFrame(); // 默认关闭窗口时退出 frame.setDefaultCloseOperation(JFrame.EXIT\_ON\_CLOSE); // 设置窗体可见 frame.setVisible(true); //定位窗体的位置 frame.setLocation(200,300); // 创建一个SimpleFrame窗体 SimpleFrame frame1 = new SimpleFrame(); //将窗体定位于（100,100）处，宽度设置为200，高度设置为400 frame1.setBounds(100,100,200,400); //设置窗体为可见 frame1.setVisible(true); // 创建一个SimpleFrame窗体 SimpleFrame frame2 = new SimpleFrame(); //设置窗体为可见 frame2.setVisible(true); //根据平台设置窗体的位置 try{ frame2.setLocationByPlatform(true); }catch(IllegalComponentStateException e){ } } }); } } [/cc] [cc lang="java"] class SimpleFrame extends JFrame { // 构造函数 public SimpleFrame() { setSize(DEFAULT\_WIDTH, DEFAULT\_HEIGHT); } // 声明默认窗体宽度 public static final int DEFAULT\_WIDTH = 300; // 声明默认窗体高度 public static final int DEFAULT\_HEIGHT = 200; } [/cc] 3、框架属性： 4、决定框架大小： [cc lang="java"] import java.awt.Dimension; import java.awt.EventQueue; import java.awt.IllegalComponentStateException; import java.awt.Image; import java.awt.Toolkit; import javax.swing.JFrame; public class SimpleFrameTest { public static void main(String[] args) { // 事件调度线程 EventQueue.invokeLater(new Runnable() { public void run() { // 创建一个SimpleFrame窗体 SimpleFrame frame = new SimpleFrame(); // 默认关闭窗口时退出 frame.setDefaultCloseOperation(JFrame.EXIT\_ON\_CLOSE); // 设置窗体可见 frame.setVisible(true); //定位窗体的位置 frame.setLocation(200,300); //设置窗体的标题 frame.setTitle("This is a Jframe!"); //调用Toolkit类的静态方法得到一个Toolkit对象 Toolkit kit = Toolkit.getDefaultToolkit(); //通过kit对象的getImage方法获得image对象 Image img = kit.getImage("qq.jpg"); //设置窗体图标 frame.setIconImage(img); //调用Toolkit的对象的getScreenSize（）方法 Dimension screenSize = kit.getScreenSize(); int screenWidth = screenSize.width; int screenHeight = screenSize.height; //设置窗体的大小： frame.setSize(screenWidth/2,screenHeight/2); // 创建一个SimpleFrame窗体 SimpleFrame frame1 = new SimpleFrame(); //将窗体定位于（100,100）处，宽度设置为200，高度设置为400 frame1.setBounds(100,100,200,400); //设置窗体为可见 frame1.setVisible(true); // 创建一个SimpleFrame窗体 SimpleFrame frame2 = new SimpleFrame(); //设置窗体为可见 frame2.setVisible(true); //根据平台设置窗体的位置 try{ frame2.setLocationByPlatform(true); }catch(IllegalComponentStateException e){ System.out.println("IllegalComponentStateException"); System.out.println(frame2.isLocationByPlatform()); } } }); } } class SimpleFrame extends JFrame { // 构造函数 public SimpleFrame() { setSize(DEFAULT\_WIDTH, DEFAULT\_HEIGHT); } // 声明默认窗体宽度 public static final int DEFAULT\_WIDTH = 300; // 声明默认窗体高度 public static final int DEFAULT\_HEIGHT = 200; } [/cc]
```
