---
layout: post
title: "[Java]统计文件字母，统计单词"
date: 2011-04-15 22:41:19.000000000 -07:00
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
  views: '8147'
  bot_views: '1'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/300.html"
---
1、编写一个程序，统计给定文件中每个字母出现的频率。  
  
2、编写一个程序，统计给定文件中包含的单词数目，并按单词表的顺序显示统计结果。  
<!--more-->

<sourcecode language="java"><br>
package com.space;</sourcecode>

import java.io.FileInputStream;  
import java.io.FileNotFoundException;  
import java.io.IOException;

public class Calculate {  
 public static void main(String[] args) {  
 FileInputStream fis = null;  
 int[] cnt = new int[27]; //a-z, upper&lower case ignore, cnt[26] other chars  
 int i=0;  
 try {  
 fis = new FileInputStream("src/test.txt");  
 while((i=fis.read())!=-1){  
 if('A'\<=i && i\<='Z')  
 i = i -'A' + 'a';  
 if((int)'a'\<=i && i\<=(int)'z'){  
 cnt[(i-'a')]++;  
 }  
 else  
 cnt[26]++; //count other characters  
 }  
 for(i=0;i\<26;i++){  
 System.out.println((char)('a'+i)+":"+cnt[i]);  
 }  
 } catch (FileNotFoundException e) {  
 // TODO Auto-generated catch block  
 e.printStackTrace();  
 } catch (IOException e) {  
 // TODO Auto-generated catch block  
 e.printStackTrace();  
 }

}

}

[sourcecode class="java"]  
package com.space;

import java.io.BufferedReader;  
import java.io.FileNotFoundException;  
import java.io.FileReader;  
import java.io.IOException;  
import java.util.Arrays;  
import java.util.Comparator;  
import java.util.HashMap;  
import java.util.Hashtable;  
import java.util.Iterator;  
import java.util.Map;  
import java.util.Set;

public class CalculateWords {  
 public static void main(String[] args) {  
 FileReader fr = null;  
 BufferedReader br = null;  
 String line = null;  
 String[] words = null;

HashMap hm = new HashMap();  
 Hashtable ht = new Hashtable();

try {  
 fr = new FileReader("src/test.txt");  
 br = new BufferedReader(fr);  
 while((line = br.readLine())!=null){  
 words = line.split(" +");  
 for(String word : words){  
 Integer value = (Integer) ht.get(word);  
 if(value == null){  
 value = 1;  
 ht.put(word, value);  
 }  
 else{  
 value++;  
 ht.put(word, value);  
 }  
 }  
 }

Set set = ht.entrySet();

Map.Entry[] entries = (Map.Entry[]) set.toArray(new Map.Entry[set.size()]);

Arrays.sort(entries, new Comparator() {  
 public int compare(Object arg0, Object arg1) {  
 String key1 = (String) ((Map.Entry) arg0).getKey();  
 String key2 = (String) ((Map.Entry) arg1).getKey();  
 return key1.compareTo(key2);  
 }  
 });

for(Map.Entry entry : entries){  
 System.out.println(entry.getKey()+": "+entry.getValue());  
 }

System.out.println("\*\*\*\*\*\*\*\*\*\*\*\*\*");

Iterator it = ht.entrySet().iterator();  
 while(it.hasNext()){  
 Map.Entry entry = (Map.Entry)it.next();  
 System.out.println(entry.getKey()+": "+entry.getValue());  
 }

Iterator iter = ht.keySet().iterator();  
 while(iter.hasNext()){  
 String s = (String)iter.next();  
 System.out.println(s+": "+ht.get(s));  
 }

} catch (FileNotFoundException e) {  
 // TODO Auto-generated catch block  
 e.printStackTrace();  
 } catch (IOException e) {  
 // TODO Auto-generated catch block  
 e.printStackTrace();  
 }

}

}  
[/sourcecode]

