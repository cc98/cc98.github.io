---
layout: post
title: wait/waitpid函数说明
date: 2010-11-25 15:56:07.000000000 -08:00
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
  _wp_old_slug: ''
  views: '2544'
  bot_views: '2'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/231.html"
---
#include\<sys/types\>

pid\_t&nbsp; wait(int \*status)

pid\_t&nbsp; waitpid(pid\_t&nbsp; pid,int \*status,int options)

wait函数的功能是等待子进程执行完的时候执行父进程

发出wait调用的进程会进入睡眠知道它的一个子进程退出或受到一个不能被忽略的信号时候唤醒，如果该调用进程没有子进程或它的子进程已经结束，该调用立即返回，调用返回是参数status中包含子进程退出时的状态信息

<!--more-->

调用waitpid 与wait的区别是waitpid等待由参数pid指定的子进程退出

对于waitpid函数中pid参数的作用解释如下

pid=-1：等待任意子进程

pid\>0: 等待进程ID与pid相等的子进程

pid=0：等待其组ID等于调用进程组ID的任一子进程

pid\<-1：等待其组ID等于pid绝对值的任一子进程

options参数使我们能进一步控制waitpid的操作，此参数可以是：

WNOHANG：若由pid指定的子进程不立即可用

则waitpid不阻塞，此时返回值0

WUNTRACED：若实现某支持作业控制，而由pid指定的任一子进程已处于暂停状态，且其状态自暂停以来还未报告过，则返回其状态

0：同wait 阻塞父进程，等待子进程退出。

# 如何等待所有的子进程结束？

1、方法一

pid\_t &nbsp; wait &nbsp; (int &nbsp; \* &nbsp; status); &nbsp;&nbsp;  
&nbsp; 函数说明 &nbsp;&nbsp;  
&nbsp; wait()会暂时停止目前进程的执行，直到有信号来到或子进程结束。如果在调用wait()时子进程已经结束，则wait()会立即返回子进程结束状态值。子进程的结束状态值会由参数status &nbsp; 返回，而子进程的进程识别码也会一快返回。如果不在意结束状态值，则 &nbsp;&nbsp;  
&nbsp; 参数 &nbsp;&nbsp;  
&nbsp; status可以设成NULL。子进程的结束状态值请参考waitpid()。 &nbsp;&nbsp;  
&nbsp; 返回值 &nbsp;&nbsp;  
&nbsp; 如果执行成功则返回子进程识别码(PID)，如果有错误发生则返回-1。失败原因存于errno中。

while( -1 !=&nbsp; wait() )  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ;&nbsp;

&nbsp;&nbsp;&nbsp; return 0;

2、方法二

waitpid()函数允许父进程等待一个特定的子进程。这个函数还允许父进程非阻塞地检查子进程是否已经终止了。

#include \<sys/wait.h\>

/\*\*  
\*  
\* @param pid\_t pid&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 指向返回状态所在单元的指针和一个用来指定可选项的标志符，  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 如果pid为-1, waitpid就等待任意一个子进程  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 如果pid大于0，waitpid就等待进程ID为pid的那个特定的子进程。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 参数pid还存在另外两种可能的值。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 如果pid为0, waitpid就等待与调用者在同一个进程组中的任意子进程。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 如果pid小于-1, waitpid就等待由pid的绝对值指定的进程组中任意一个子进程。  
\*  
\* @param int\*&nbsp; stat\_loc 指向整数变量的指针。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 如果stat\_loc不为NULL,这些函数就将子进程的返回状态存储在这个单元中。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 子进程通过调用exit, \_exit, \_Exit或从main函数中return来返回它的状态。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 返回值为零说明EXIT\_SUCCESS;任何其它的值都说明EXIT\_FAILURE。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 父进程只能对子进程返回状态的8个最低有效位进行访问  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;  
\* @param int&nbsp;&nbsp; options&nbsp; 是一个或多个标志符按位"或"的结果。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 即使子进程的状态不是立刻可用的，选项WNOHANG也会使waitpid返回。  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 选项WUNTRACED会使waitpid报告那些已经被停止的未报告的子进程的状态  
\*  
\* @return 成功: 返回子进程ID&nbsp;  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 错误:返回-1并设置errno  
\*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 如果用选项WNOHANG调用waitpid, 则waitpid就返回0来报告可能有无人等待的子进程，但这些子进程的状态不可用  
\*&nbsp;  
\*/  
pid\_t waitpid(pid\_t pid, int \*stat\_loc, int options);

void &nbsp; waitchild(int &nbsp; signo) &nbsp;&nbsp;  
&nbsp; { &nbsp;&nbsp;  
&nbsp; &nbsp; &nbsp; &nbsp; pid\_t &nbsp; pid; &nbsp;&nbsp;  
&nbsp; &nbsp; &nbsp; &nbsp; while((pid &nbsp; = &nbsp; waitpid(-1,NULL,WNOHANG))\>0){ &nbsp;&nbsp;  
&nbsp; &nbsp; &nbsp; &nbsp; } &nbsp;&nbsp;  
&nbsp; }

