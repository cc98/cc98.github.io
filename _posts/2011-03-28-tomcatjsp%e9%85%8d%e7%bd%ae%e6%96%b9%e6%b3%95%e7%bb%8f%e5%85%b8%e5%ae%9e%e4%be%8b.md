---
layout: post
title: Tomcat+JSP配置方法经典实例
date: 2011-03-28 11:33:30.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Solutions
tags:
- Java
- JSP
- Tomcat
meta:
  _edit_last: '1'
  views: '1377'
  bot_views: '5'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/solutions/288.html"
---
经常看到jsp的初学者问tomcat下如何配置jsp、servlet和bean的问题，于是总结了一下如何tomcat下配置jsp、servlet和ben，希望对那些初学者有所帮助。  
　　  
　　 **一、开发环境配置**  
　　  
　　第一步：下载j2sdk和tomcat：到sun官方站（http://java.sun.com/j2se/1.5.0/download.jsp）下载j2sdk，注意下载版本为Windows Offline Installation的SDK，同时最好下载J2SE 1.5.0 Documentation，然后到tomcat官方站点（http://jakarta.apache.org/site/downloads/downloads\_tomcat-5.cgi）下载tomcat（下载最新5.5.9版本的tomcat）；  
　　  
　　第二步：安装和配置你的j2sdk和tomcat：执行j2sdk和tomcat的安装程序，然后按默认设置进行安装即可。  
　　  
　　1.安装j2sdk以后，需要配置一下环境变量，在我的电脑-\>属性-\>高级-\>环境变量-\>系统变量中添加以下环境变量(假定你的j2sdk安装在c:j2sdk1.5.0）：  
　　  
　　JAVA\_HOME=c:j2sdk1.5.0  
　　classpath=.;%JAVA\_HOME%libdt.jar;%JAVA\_HOME%libtools.jar;（.;一定不能少，因为它代表当前路径)  
　　path=%JAVA\_HOME%bin  
　　<!--more-->  
　　接着可以写一个简单的java程序来测试J2SDK是否已安装成功：  
　　  
　　public class Test{  
　　public static void main(String args[]){  
　　System.out.println("This is a test program.");  
　　}  
　　}  
　　  
　　将上面的这段程序保存为文件名为Test.java的文件。  
　　  
　　然后打开命令提示符窗口，cd到你的Test.java所在目录，然后键入下面的命令  
　　  
　　javac Test.java  
　　java Test  
　　  
　　此时如果看到打印出来This is a test program.的话说明安装成功了，如果没有打印出这句话，你需要仔细检查一下你的配置情况。  
　　  
　　2.安装Tomcat后，在我的电脑-\>属性-\>高级-\>环境变量-\>系统变量中添加以下环境变量(假定你的tomcat安装在c:tomcat)：  
　　  
　　CATALINA\_HOME=c:tomcat  
　　CATALINA\_BASE=c:tomcat  
　　  
　　然后修改环境变量中的classpath，把tomat安装目录下的commonlib下的(可以根据实际追加)servlet.jar追加到classpath中去，修改后的classpath如下：  
　　  
　　classpath=.;%JAVA\_HOME%libdt.jar;%JAVA\_HOME%libtools.jar;%CATALINA\_HOME%commonlibservlet.jar;  
　　  
　　接着可以启动tomcat，在IE中访问http://localhost:8080，如果看到tomcat的欢迎页面的话说明安装成功了。  
　　  
　　第三步：建立自己的jsp app目录  
　　  
　　1.到Tomcat的安装目录的webapps目录，可以看到ROOT，examples, tomcat-docs之类Tomcat自带的的目录；  
　　2.在webapps目录下新建一个目录，起名叫myapp；  
　　3.myapp下新建一个目录WEB-INF，注意，目录名称是区分大小写的；  
　　4.WEB-INF下新建一个文件web.xml，内容如下：  
　　  
　　\<?xml version="1.0" encoding="ISO-8859-1"?\>  
　　\<!DOCTYPE web-app  
　　PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"  
　　"http://java.sun.com/dtd/web-app\_2\_3.dtd"\>  
　　\<web-app\>  
　　\<display-name\>My Web Application\</display-name\>  
　　\<description\>  
　　A application for test.  
　　\</description\>  
　　\</web-app\>  
　　  
　　5.在myapp下新建一个测试的jsp页面，文件名为index.jsp，文件内容如下：  
　　\<html\>\<body\>\<center\>  
　　Now time is: \<%=new java.util.Date()%\>  
　　\</center\>\</body\>\</html\>  
　　  
　　6.重启Tomcat  
　　  
　　7.打开浏览器，输入http://localhost:8080/myapp/index.jsp 看到当前时间的话说明就成功了。  
　　  
　　第四步：建立自己的Servlet：  
　　  
　　1.用你最熟悉的编辑器（建议使用有语法检查的java ide）新建一个servlet程序，文件名为Test.java，文件内容如下：  
　　  
　　package test;  
　　import java.io.IOException;  
　　import java.io.PrintWriter;  
　　import javax.servlet.ServletException;  
　　import javax.servlet.http.HttpServlet;  
　　import javax.servlet.http.HttpServletRequest;  
　　import javax.servlet.http.HttpServletResponse;  
　　public class Test extends HttpServlet {  
　　protected void doGet(HttpServletRequest request, HttpServletResponse response)  
　　throws ServletException, IOException {  
　　PrintWriter out=response.getWriter();  
　　out.println("\<html\>\<body\>\<h1\>This is a servlet test.\</h1\>\</body\>\</html\>");  
　　out.flush();  
　　}  
　　}  
　　  
　　2 .编译  
　　将Test.java放在c:test下，使用如下命令编译：  
　　  
　　C:Test\>javac Test.java  
　　  
　　然后在c:Test下会产生一个编译后的servlet文件：Test.class  
　　  
　　3 .将结构testTest.class剪切到%CATALINA\_HOME%webappsmyappWEB-INFclasses下，也就是剪切那个test目录到classes目录下，如果classes目录不存在，就新建一个。 现在webappsmyappWEB-INFclasses下有testTest.class的文件目录结构  
　　  
　　4 .修改webappsmyappWEB-INFweb.xml，添加servlet和servlet-mapping  
　　  
　　编辑后的web.xml如下所示，红色为添加的内容:  
　　  
　　\<?xml version="1.0" encoding="ISO-8859-1"?\>  
　　\<!DOCTYPE web-app  
　　PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"  
　　"http://java.sun.com/dtd/web-app\_2\_3.dtd"\>  
　　\<web-app\>  
　　\<display-name\>My Web Application\</display-name\>  
　　\<description\>  
　　A application for test.  
　　\</description\>  
　　\<servlet\>  
　　\<servlet-name\>Test\</servlet-name\>  
　　\<display-name\>Test\</display-name\>  
　　\<description\>A test Servlet\</description\>  
　　\<servlet-class\>test.Test\</servlet-class\>  
　　\</servlet\>  
　　\<servlet-mapping\>  
　　\<servlet-name\>Test\</servlet-name\>  
　　\<url-pattern\>/Test\</url-pattern\>  
　　\</servlet-mapping\>  
　　\</web-app\>  
　　  
　　这段话中的servlet这一段声明了你要调用的Servlet，而servlet-mapping则是将声明的servlet"映射"到地址/Test上  
　　  
　　5 .好了，重启动Tomcat，启动浏览器，输入http://localhost:8080/myapp/Test 如果看到输出This is a servlet test.就说明编写的servlet成功了。  
　　  
　　注意：修改了web.xml以及新加了class，都要重启Tomcat  
　　  
　　第四步：建立自己的Bean：  
　　  
　　1.用你最熟悉的编辑器（建议使用有语法检查的java ide）新建一个java程序，文件名为TestBean.java，文件内容如下：  
　　  
　　package test;  
　　public class TestBean{  
　　private String name = null;  
　　public TestBean(String strName\_p){  
　　this.name=strName\_p;  
　　}  
　　public void setName(String strName\_p){  
　　this.name=strName\_p;  
　　}  
　　public String getName(){  
　　return this.name;  
　　}  
　　}  
　　  
　　2 .编译  
　　  
　　将TestBean.java放在c:test下，使用如下命令编译：  
　　  
　　C:Test\>javac TestBean.java  
　　  
　　然后在c:Test下会产生一个编译后的bean文件：TestBean.class  
　　  
　　3 .将TestBean.class文件剪切到 %CATALINA\_HOME%webappsmyappWEB-INFclassestest下，  
　　  
　　4 .新建一个TestBean.jsp文件，文件内容为：  
　　  
　　\<%@ page import="test.TestBean" %\>  
　　\<html\>\<body\>\<center\>  
　　\<%  
　　TestBean testBean=new TestBean("This is a test java bean.");  
　　%\>  
　　Java bean name is: \<%=testBean.getName()%\>  
　　\</center\>\</body\>\</html\>  
　　  
　　5 .好了，重启Tomcat，启动浏览器，输入http://localhost:8080/myapp/TestBean.jsp 如果看到输出Java bean name is: This is a test java bean.就说明编写的Bean成功了。  
　　  
　　这样就完成了整个Tomcat下的jsp、servlet和javabean的配置。接下来需要做的事情就是多看书、多读别人的好代码，自己多动手写代码以增强自己在这方面开发的能力了。  
　　  
　　jvm应填写到  
　　c:j2sdkbin  
　　  
　　给你一个简单的配置：：：：  
　　  
　　 **JSP环境配置心得**  
　　  
　　首先要说的是，使用jdk+tomcat完全可以配置我们的jsp服务器，不再需要其实任何东东，有很多文章介绍了Apache，其实根本用不着，一般的学习调试tomcat完全可以胜任了。  
　　  
　　安装jdk后，tomcat在安装之前会自动找到jdk的安装路径，一路点击"下一步"，经过一段时间的文件复制，最后"close"，完成comcat的安装。  
　　  
　　您最好去下载一个版本较高的tomcat，比如4.1以上的，因为它不需要设置太多的系统变量，右击"我的电脑"，选择"属性"-\>"高级"-\>"环境变量"-\>"系统变量"，新建一个TOMCAT\_HOME，值设置成你的tomcat所在的路径，比如：D:Program FilesApache GroupTomcat 5.5，配置完成。  
　　  
　　从开始菜单中找到tomcat选项，一般打开顺序是：开始-\>程序-\>Apache Tomcat 5.5，选择"Start Tomcat"，让jsp服务器开始运行，此时会打开一个类似Dos的窗口，会显示一些相关的信息。

