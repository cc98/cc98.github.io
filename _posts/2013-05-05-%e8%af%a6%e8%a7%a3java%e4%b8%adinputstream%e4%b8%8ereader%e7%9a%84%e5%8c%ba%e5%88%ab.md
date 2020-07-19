---
layout: post
title: 详解Java中Inputstream与Reader的区别
date: 2013-05-05 11:59:14.000000000 -07:00
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
  views: '1169'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/947.html"
---
Reader支持16位的Unicode字符输出，InputStream支持8位的字符输出。  
Reader和InputStream分别是I/O库提供的两套平行独立的等级机构，

**InputStream、OutputStream是用来处理8位元的流，**  
 **Reader、Writer是用来处理16位元的流。**  
而在JAVA语言中，byte类型是8位的，char类型是16位的，所以在处理中文的时候需要用Reader和Writer。  
值得说明的是，在这两种等级机构下，还有一道桥梁InputStreamReader、OutputStreamWriter负责进行InputStream到Reader的适配和由OutputStream到Writer的适配。

<!--more-->

java.io.Reader&nbsp;和&nbsp;java.io.InputStream&nbsp;组成了&nbsp;Java输入类。Reader&nbsp;用于读入16位字符，也就是&nbsp;Unicode编码的字符；而&nbsp;InputStream&nbsp;用于读入&nbsp;ASCII字符和二进制数据。

在&nbsp;Java中，有不同类型的&nbsp;Reader&nbsp;输入流对应于不同的数据源：  
FileReader&nbsp;用于从文件输入；  
CharArrayReader&nbsp;用于从程序中的字符数组输入；  
StringReader&nbsp;用于从程序中的字符串输入；  
PipedReader&nbsp;用于读取从另一个线程中的&nbsp;PipedWriter&nbsp;写入管道的数据。  
相应的也有不同类型的&nbsp;InputStream&nbsp;输入流对应于不同的数据源：FileInputStream，ByteArrayInputStream，StringBufferInputStream，PipedInputStream。另外，还有两种没有对应&nbsp;Reader&nbsp;类型的&nbsp;InputStream&nbsp;输入流：  
Socket&nbsp;用于套接字；  
URLConnection&nbsp;用于&nbsp;URL&nbsp;连接。  
这两个类使用&nbsp;getInputStream()&nbsp;来读取数据。  
相应的，java.io.Writer&nbsp;和&nbsp;java.io.OutputStream&nbsp;也有类似的区别。

