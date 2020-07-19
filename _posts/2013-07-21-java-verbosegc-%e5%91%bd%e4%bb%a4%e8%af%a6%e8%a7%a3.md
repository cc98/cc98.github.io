---
layout: post
title: Java -verbose:gc 命令详解 JVM参数以及其含义
date: 2013-07-21 15:56:17.000000000 -07:00
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
  bot_views: '6'
  views: '1134'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/1055.html"
---
Java -verbose:gc 中参数-verbose:gc 表示输出虚拟机中GC的详细情况.

使用后输出如下:

[Full GC 168K-\>97K(1984K)， 0.0253873 secs]

解读如下:

　　箭头前后的数据168K和97K分别表示垃圾收集GC前后所有存活对象使用的内存容量，说明有168K-97K=71K的对象容量被回收，括号内的数据1984K为堆内存的总容量，收集所需要的时间是0.0253873秒（这个时间在每次执行的时候会有所不同）

Note:GC会暂用CPU时间片,有可能造成应用程序在某个时刻极短的停顿.

<!--more-->

Java&nbsp; **-Xms2g -Xmx2g -Xmn512M -Xss128K -XX:PermSize=128M -XX:MaxPermSize=128M -XX:NewRatio=4 -XX:SurivorRatio=4 -XX:MaxTenuringThreshold=1**

-Xms2g：JVM启动初始化堆大小为2g，Xms的默认是物理内存的1/64但小于1G。

-Xmx2g：JVM最大的堆大小为2g，Xmx默认是物理内存的1/4但小于1G；将-Xms和-Xmx的值配置为一样，可以避免每次垃圾回收完成后对JVM堆大小进行重新的调整。

-Xmn512M：堆中的新生代大小为512M

-Xss128K：每个线程的堆栈大小为128K

-XX:PermSize=128M：JVM持久代的初始化大小为128M

-XX:MaxPermSize=128M：JVM持久代的最大大小为128M

-XX:NewRatio=4：JVM堆的新生代和老年代的大小比例为1：4

-XX:SurvivorRatio=4：新生代Surivor区（新生代有2个Surivor区）和Eden区的比例为2：4

-XX:MaxTenuringThreshold=1：新生代的对象经过几次垃圾回收后（如果还存活），进入老年代。如果该参数设置为0，这表示新生代的对象在垃圾回收后，不进入survivor区，直接进入老年代

&nbsp;

Java **&nbsp;-XX:+UseParallelGC -XX:ParallelGCThread=4&nbsp;-XX:+UseParallelOldGC -XX:MaxGCPauseMillis=100 -XX:+UseAdaptiveSizePolicy**

-XX:+UseParallelGC：使用并行的垃圾收集器，但仅针对新生代有效，老年代仍然使用串行收集器

-XX:ParallelGCThread=4：设置并行垃圾回收器的线程为4个，该设置最好与处理器的数目相同

-XX:+UseParalleOldGC：配置老年代使用并行垃圾收集器，JDK1.6支持老年代使用并行收集器

-XX:MaxGCPauseMillis=100：设置每次新生代每次收集器垃圾回收的最长时间，如果无法满足该时间，JVM会自动调整新生代区的大小，以满足该值

-XX:+UseAdaptiveSizePolicy：设置此值后，JVM会自动调整新生代大小以及相应的surivor区的比例，以达到设置的最低响应时间或者收集频率等

&nbsp;

Java **&nbsp;-XX:UseConcMarkSweepGC -XX:+UseParNewGC -XX:CMSFullGCsBeforeCompaction=5 -XX:+UseCMSCompactAtFullCollection**

-XX:UseConcMarkSweepGC：设置JVM堆的老年代使用CMS并发收集器，设置该参数后，-XX:NewRatio参数失效，但-Xmn参数依然有效

-XX:UseParNewGC：设置新生代使用并发收集器，在JDK1.5以上，JVM会根据系统自动设置

-XX:CMSFullGCsBeforeCompaction=5：设置5才CMSGC后对堆空间进行压缩、整理

-XX:+UseCMSCompactAtFullCollection：打开对老年代的压缩，可能会影响性能，但可以消除堆碎片

