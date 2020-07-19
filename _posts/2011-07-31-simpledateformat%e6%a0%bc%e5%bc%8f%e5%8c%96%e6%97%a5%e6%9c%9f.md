---
layout: post
title: SimpleDateFormat格式化日期
date: 2011-07-31 00:49:55.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Skills
tags: []
meta:
  views: '3107'
  _edit_last: '1'
  bot_views: '12'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/327.html"
---
[cc lang="java"]  
import java.text.SimpleDateFormat;  
import java.util.Date;  
public class test {  
&nbsp;public static void main(String []aa){  
&nbsp;&nbsp;SimpleDateFormat dateformat1=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss E");  
&nbsp;&nbsp;String a1=dateformat1.format(new Date());  
&nbsp;&nbsp;System.out.println("时间2:"+a1);  
&nbsp;&nbsp;System.out.println(new Date().getYear()+1900);  
&nbsp;&nbsp;  
&nbsp;&nbsp;SimpleDateFormat dateformat2=new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒 E ");&nbsp;&nbsp;&nbsp;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; String a2=dateformat2.format(new Date());  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; System.out.println("时间2:"+a2);&nbsp;  
&nbsp;}  
}  
[/cc]

执行结果:  
时间2:2006-12-21 14:40:59 星期四  
2006  
时间2:2006年12月21日 14时40分59秒 星期四  
<!--more-->

java.util.Calendar对于日期的处理非常的方便，如newDate.set(Calendar.MONTH, 12); //加12个月，newDate.set(Calendar.DATE, -1); //前一天  
[cc lang="java"]  
import java.text.SimpleDateFormat;  
import java.util.Date;  
import java.util.Calendar;  
public class calendartest {  
&nbsp;/\*\*  
&nbsp; \* @param args  
&nbsp; \*/  
&nbsp;public static void main(String[] args) {  
&nbsp;&nbsp;SimpleDateFormat dateformat=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss E");  
&nbsp;&nbsp;  
&nbsp;&nbsp;System.out.println("今天&nbsp; :"+dateformat.format(new Date()));  
&nbsp;&nbsp;  
&nbsp;&nbsp;Calendar c=Calendar.getInstance();&nbsp;&nbsp;  
&nbsp;&nbsp;  
&nbsp;&nbsp;c.set(Calendar.DAY\_OF\_WEEK, Calendar.MONDAY);  
&nbsp;&nbsp;Date d1=new Date(c.getTimeInMillis());  
&nbsp;&nbsp;System.out.println("星期一:"+dateformat.format(d1));  
&nbsp;&nbsp;  
&nbsp;&nbsp;c.set(Calendar.DAY\_OF\_WEEK, Calendar.SUNDAY);  
&nbsp;&nbsp;Date d2=new Date(c.getTimeInMillis());  
&nbsp;&nbsp;System.out.println("星期日:"+dateformat.format(d2));&nbsp;&nbsp;  
&nbsp;&nbsp;  
&nbsp;}  
}  
[/cc]  
执行结果:  
今天&nbsp; :2006-12-21 16:39:03 星期四  
星期一:2006-12-18 16:39:03 星期一  
星期日:2006-12-17 16:39:03 星期日

