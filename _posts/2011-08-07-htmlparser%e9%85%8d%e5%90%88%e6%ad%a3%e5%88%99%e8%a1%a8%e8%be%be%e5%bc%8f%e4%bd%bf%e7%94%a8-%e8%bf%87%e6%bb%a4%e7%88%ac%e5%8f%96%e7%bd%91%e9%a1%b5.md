---
layout: post
title: "[HTMLParser]配合[正则表达式]使用 过滤爬取网页"
date: 2011-08-07 23:01:37.000000000 -07:00
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
  bot_views: '5'
  views: '4221'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/solutions/358.html"
---
爬虫已经能够把所有页面爬下来了，但是保存的是包括完整html标签的html文件，所以使用HtmlParser来过滤不需要的html标签。然后想到了直接使用了正则表达式匹配来去除98上的[url]这种BB功能标签，别看就一个正则表达式，其实折腾了好久。正则表达式匹配[中括号，使用\[，同理匹配?使用\?，别被网上一些言论误导。。不然都false。。还是自己查api比较靠谱。

**&nbsp;HTMLParser** 的核心模块是 **org.htmlparser.Parser** 类，这个类实际完成了对于HTML页面的分析工作。这个类有下面几个构造函数：  
&nbsp;&nbsp;&nbsp; public Parser ();  
&nbsp;&nbsp;&nbsp; public Parser (Lexer lexer, ParserFeedback fb);  
&nbsp;&nbsp; &nbsp;public Parser (URLConnection connection, ParserFeedback fb) throws ParserException;  
&nbsp;&nbsp;&nbsp; public Parser (String resource, ParserFeedback feedback) throws ParserException;  
&nbsp;&nbsp; &nbsp;public Parser (String resource) throws ParserException;  
&nbsp;&nbsp;&nbsp; public Parser (Lexer lexer);  
&nbsp;&nbsp;&nbsp; public Parser (URLConnection connection) throws ParserException;  
和一个静态类 public static Parser createParser (String html, String charset);

<!--more-->

HtmlParser的filter功能也很强大，支持各种组合。。14个filter如下，下面注释掉的代码有使用几种

[**判断类**** Filter ****：**](http://www.baizeju.com/html/HTMLParser/200807/07-121.html#判断类Filter)  
TagNameFilter  
HasAttributeFilter  
HasChildFilter  
HasParentFilter  
HasSiblingFilter  
IsEqualFilter  
[**逻辑运算**** Filter ****：**](http://www.baizeju.com/html/HTMLParser/200807/07-121.html#逻辑运算Filter)  
AndFilter  
NotFilter  
OrFilter  
XorFilter  
[**其他**** Filter ****：**](http://www.baizeju.com/html/HTMLParser/200807/07-121.html#其他Filter)  
NodeClassFilter  
StringFilter  
LinkStringFilter  
LinkRegexFilter  
RegexFilter  
CssSelectorNodeFilter

&nbsp;

**以下就来贴下完整的处理代码:**

[cc lang="java"]

package com.htmlparser;

import java.io.BufferedReader;  
import java.io.FileNotFoundException;  
import java.io.FileOutputStream;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.io.FileInputStream;  
import java.io.File;  
import java.io.OutputStreamWriter;  
import java.net.HttpURLConnection;  
import java.net.URL;  
import java.util.ArrayList;  
import java.util.LinkedList;  
import java.util.List;

import org.htmlparser.Node;  
import org.htmlparser.NodeFilter;  
import org.htmlparser.filters.AndFilter;  
import org.htmlparser.filters.HasAttributeFilter;  
import org.htmlparser.filters.NotFilter;  
import org.htmlparser.filters.StringFilter;  
import org.htmlparser.filters.TagNameFilter;  
import org.htmlparser.util.NodeIterator;  
import org.htmlparser.util.NodeList;  
import org.htmlparser.Parser;

public class TestHtmlParser {  
&nbsp;private static String ENCODE = "UTF-8";

&nbsp;// 用于输出显示测试  
&nbsp;private void message(String szMsg) {  
&nbsp;&nbsp;try {  
&nbsp;&nbsp;&nbsp;System.out.println(new String(szMsg.getBytes(ENCODE), System  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.getProperty("file.encoding")));  
&nbsp;&nbsp;} catch (Exception e) {  
&nbsp;&nbsp;}  
&nbsp;}

&nbsp;// 打开html文件，读取文件所有内容  
&nbsp;public String openFile(String filename) {  
&nbsp;&nbsp;try {  
&nbsp;&nbsp;&nbsp;BufferedReader bis = new BufferedReader(new InputStreamReader(  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;new FileInputStream(new File(filename)), ENCODE));  
&nbsp;&nbsp;&nbsp;String content = "";  
&nbsp;&nbsp;&nbsp;String temp;

&nbsp;&nbsp;&nbsp;while ((temp = bis.readLine()) != null) {  
&nbsp;&nbsp;&nbsp;&nbsp;content += temp + "n";  
&nbsp;&nbsp;&nbsp;}  
&nbsp;&nbsp;&nbsp;bis.close();  
&nbsp;&nbsp;&nbsp;return content;  
&nbsp;&nbsp;} catch (Exception e) {  
&nbsp;&nbsp;&nbsp;return "";  
&nbsp;&nbsp;}  
&nbsp;}

&nbsp;// 将解析好的字符串，写到.txt文件  
&nbsp;public boolean writeFile(String filename, String content) {  
&nbsp;&nbsp;boolean result = false;  
&nbsp;&nbsp;try {  
&nbsp;&nbsp;&nbsp;OutputStreamWriter osw = new OutputStreamWriter(  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;new FileOutputStream(new File("E:\MyCrawl\cc98-txt\"  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;+ filename + ".txt")), ENCODE);  
&nbsp;&nbsp;&nbsp;osw.write(content);  
&nbsp;&nbsp;&nbsp;osw.close();  
&nbsp;&nbsp;&nbsp;result = true;

&nbsp;&nbsp;} catch (FileNotFoundException e) {  
&nbsp;&nbsp;&nbsp;// TODO Auto-generated catch block  
&nbsp;&nbsp;&nbsp;e.printStackTrace();  
&nbsp;&nbsp;} catch (IOException e) {  
&nbsp;&nbsp;&nbsp;// TODO Auto-generated catch block  
&nbsp;&nbsp;&nbsp;e.printStackTrace();  
&nbsp;&nbsp;}  
&nbsp;&nbsp;return result;  
&nbsp;}

&nbsp;// 解析一个文件  
&nbsp;public void parseFile(File file) {  
&nbsp;&nbsp;System.out.println("parsing:" + file.getName());  
&nbsp;&nbsp;String content = openFile(file.getPath());  
&nbsp;&nbsp;try {  
&nbsp;&nbsp;&nbsp;Parser parser = Parser.createParser(content, ENCODE);  
&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp;// TextExtractingVisitor visitor = new TextExtractingVisitor();  
&nbsp;&nbsp;&nbsp;// parser.visitAllNodesWith(visitor);  
&nbsp;&nbsp;&nbsp;// String textInPage = visitor.getExtractedText();  
&nbsp;&nbsp;&nbsp;//  
&nbsp;&nbsp;&nbsp;// message(textInPage);

&nbsp;&nbsp;&nbsp;// NodeFilter Tagfilter = new TagNameFilter("span");  
&nbsp;&nbsp;&nbsp;// NodeFilter Urlfilter = new StringFilter("http://");  
&nbsp;&nbsp;&nbsp;// NodeFilter noUrlfilter = new NotFilter(Urlfilter);  
&nbsp;&nbsp;&nbsp;// NodeFilter filter = new AndFilter(Tagfilter, noUrlfilter);

&nbsp;&nbsp;&nbsp;NodeFilter tagfilter = new TagNameFilter("span");  
&nbsp;&nbsp;&nbsp;NodeFilter filterID = new HasAttributeFilter("id");  
&nbsp;&nbsp;&nbsp;NodeFilter filter = new AndFilter(tagfilter, filterID);

&nbsp;&nbsp;&nbsp;NodeList nodes = parser.extractAllNodesThatMatch(filter);

&nbsp;&nbsp;&nbsp;String txt = "";  
&nbsp;&nbsp;&nbsp;if (nodes != null) {  
&nbsp;&nbsp;&nbsp;&nbsp;for (int i = 0; i \< nodes.size(); i++) {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Node textnode = (Node) nodes.elementAt(i);

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// message("getText:" + textnode.getText());  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;txt += textnode.toPlainTextString() + "nr";

&nbsp;&nbsp;&nbsp;&nbsp;}  
&nbsp;&nbsp;&nbsp;}  
&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp;txt = txt.replaceAll("[\[/?[a-zA-Z0-9\?\](file://[/?[a-zA-Z0-9\?\). /&~=:,&&[^\]]]+\]", "");  
&nbsp;&nbsp;&nbsp;txt = txt.replaceAll("&nbsp;", "").replaceAll("[t]+", "");// .replaceAll("[n]+", "n");  
&nbsp;&nbsp;&nbsp;writeFile(file.getName(), txt);

&nbsp;&nbsp;&nbsp;// for (NodeIterator i = parser.elements(); i.hasMoreNodes();) {  
&nbsp;&nbsp;&nbsp;// Node node = i.nextNode();  
&nbsp;&nbsp;&nbsp;// message("getText:" + node.getText());  
&nbsp;&nbsp;&nbsp;// message("getPlainText:" + node.toPlainTextString());  
&nbsp;&nbsp;&nbsp;// message("toHtml:" + node.toHtml());  
&nbsp;&nbsp;&nbsp;// message("toHtml(true):" + node.toHtml(true));  
&nbsp;&nbsp;&nbsp;// message("toHtml(false):" + node.toHtml(false));  
&nbsp;&nbsp;&nbsp;// message("toString:" + node.toString());  
&nbsp;&nbsp;&nbsp;// message("=================================================");  
&nbsp;&nbsp;&nbsp;// if(node.getText().length()\>=3){  
&nbsp;&nbsp;&nbsp;// if("html".equals(node.getText().substring(0, 4))){  
&nbsp;&nbsp;&nbsp;// message("getPlainText:" + node.toPlainTextString());  
&nbsp;&nbsp;&nbsp;// }  
&nbsp;&nbsp;&nbsp;// }  
&nbsp;&nbsp;&nbsp;// }  
&nbsp;&nbsp;} catch (Exception e) {  
&nbsp;&nbsp;&nbsp;System.out.println("Exception:" + e);  
&nbsp;&nbsp;}  
&nbsp;}

&nbsp;// 主函数，遍历cc98目录  
&nbsp;public static void main(String[] args) {  
&nbsp;&nbsp;TestHtmlParser thp = new TestHtmlParser();  
&nbsp;&nbsp;LinkedList\<String\> folderList = new LinkedList\<String\>();  
&nbsp;&nbsp;folderList.add("E:\MyCrawl\cc98\");  
&nbsp;&nbsp;while (folderList.size() \> 0) {  
&nbsp;&nbsp;&nbsp;File file = new File(folderList.poll());  
&nbsp;&nbsp;&nbsp;File[] files = file.listFiles();  
&nbsp;&nbsp;&nbsp;List\<File\> fileList = new ArrayList\<File\>();  
&nbsp;&nbsp;&nbsp;for (int i = 0; i \< files.length; i++) {  
&nbsp;&nbsp;&nbsp;&nbsp;if (files[i].isDirectory()) {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;folderList.add(files[i].getPath());  
&nbsp;&nbsp;&nbsp;&nbsp;} else {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fileList.add(files[i]);  
&nbsp;&nbsp;&nbsp;&nbsp;}  
&nbsp;&nbsp;&nbsp;}

&nbsp;&nbsp;&nbsp;for (File f : fileList) {  
&nbsp;&nbsp;&nbsp;&nbsp;thp.parseFile(f);  
&nbsp;&nbsp;&nbsp;}  
&nbsp;&nbsp;}

&nbsp;}

}

[/cc]

