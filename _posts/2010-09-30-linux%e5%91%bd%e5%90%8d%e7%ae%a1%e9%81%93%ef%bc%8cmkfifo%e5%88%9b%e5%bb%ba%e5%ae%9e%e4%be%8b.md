---
layout: post
title: Linux命名管道，mkfifo创建实例
date: 2010-09-30 20:13:29.000000000 -07:00
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
  views: '8379'
  bot_views: '2'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/178.html"
---
/\*\*  
\*&nbsp; mypipeserver.c: 服务器端程序  
\*&nbsp; Author: Navins  
\*&nbsp; Program Date: 2010-7-23  
\*&nbsp; Modified Date: 2010-7-23  
\*&nbsp; 使用Linux的命名管道机制，用C语言编写的服务器端程序。  
\*&nbsp; 程序中使用mkfifo函数创建命名管道，以只读方式open命名管道，隔3s读信息。  
\*\*/

#include\<stdio.h\>  
#include\<sys/types.h\>  
#include\<sys/stat.h\>  
#include\<fcntl.h\>  
#include\<unistd.h\>

#define FIFO\_CHANNEL "/home/zhulin/coding/my\_fifo"&nbsp; /\* 宏定义，fifo路径 \*/

int main()  
{  
&nbsp;int fd;  
&nbsp;char buf[80];  
&nbsp;  
&nbsp;if(mkfifo(FIFO\_CHANNEL,0777)==-1) /\* 创建命名管道，返回-1表示失败 \*/<!--more-->  
&nbsp;{  
&nbsp;&nbsp;perror("Can't create FIFO channel");  
&nbsp;&nbsp;return 1;  
&nbsp;}  
&nbsp;  
&nbsp;if((fd=open(FIFO\_CHANNEL,O\_RDONLY))==-1)&nbsp; /\* 以只读方式打开命名管道 \*/  
&nbsp;{  
&nbsp;&nbsp;perror("Can't open the FIFO");  
&nbsp;&nbsp;return 1;  
&nbsp;}

&nbsp;while(1)&nbsp; /\* 不断从管道中读取信息 \*/  
&nbsp;{  
&nbsp;&nbsp;read( fd, buf, sizeof(buf) );  
&nbsp;&nbsp;printf("Message from Client: %sn",buf );  
&nbsp;&nbsp;sleep(3); /\* sleep 3s \*/  
&nbsp;}

&nbsp;close(fd);&nbsp; /\* 关闭管道 \*/  
&nbsp;return 0;  
}

/\*\*  
\*&nbsp; mypipeclient.c: 客户端程序  
\*&nbsp; Author: Navins  
\*&nbsp; Program Date: 2010-7-23  
\*&nbsp; Modified Date: 2010-7-23  
\*&nbsp; 使用Linux的命名管道机制，用C语言编写的客户器端程序。  
\*&nbsp; 程序中使用open函数以读写方式打开命名管道，隔3s写信息。  
\*\*/

#include\<stdio.h\>  
#include\<sys/types.h\>  
#include\<sys/stat.h\>  
#include\<fcntl.h\>  
#include\<unistd.h\>

#define FIFO\_CHANNEL "/home/zhulin/coding/my\_fifo"&nbsp; /\* 宏定义，fifo路径 \*/

int main()  
{  
&nbsp;int fd;  
&nbsp;char s[]="Hello!";

&nbsp;if((fd=open(FIFO\_CHANNEL,O\_WRONLY))==-1)&nbsp; /\* 以读写方式打开命名管道，返回-1代表失败 \*/  
&nbsp;{  
&nbsp;&nbsp;perror("Can't open the FIFO");  
&nbsp;&nbsp;return 1;  
&nbsp;}

&nbsp;while(1)&nbsp; /\* 不断向管道中写信息 \*/  
&nbsp;{  
&nbsp;&nbsp;write( fd, s, sizeof(s) );  
&nbsp;&nbsp;printf("Write: %sn",s);  
&nbsp;&nbsp;sleep(3);&nbsp; /\* sleep 3s \*/  
&nbsp;}

&nbsp;close(fd);&nbsp; /\* 关闭管道 \*/  
&nbsp;return 0;  
}

使用fork函数，在一个程序里面模拟服务端和客户端。

#include\<stdio.h\>  
#include\<sys/types.h\>  
#include\<sys/stat.h\>  
#include\<unistd.h\>  
#include\<fcntl.h\>

int main(void)  
{  
&nbsp;char buf[80];  
&nbsp;int fd;  
&nbsp;pid\_t pid;  
&nbsp;unlink( "fifo" );  
&nbsp;mkfifo( "fifo", 0777 );

&nbsp;if( (pid=fork()) == 0 )  
&nbsp;{  
&nbsp;&nbsp;char s[] = "Hello!n";  
&nbsp;&nbsp;fd = open( "fifo", O\_WRONLY );&nbsp;&nbsp;  
&nbsp;&nbsp;while(1)  
&nbsp;&nbsp;{  
&nbsp;&nbsp;&nbsp;write( fd, s, sizeof(s) );  
&nbsp;&nbsp;&nbsp;sleep(3);  
&nbsp;&nbsp;}  
&nbsp;&nbsp;close( fd );  
&nbsp;}  
&nbsp;else if( pid \> 0 )  
&nbsp;{  
&nbsp;&nbsp;fd = open( "fifo", O\_RDONLY );  
&nbsp;&nbsp;while(1)  
&nbsp;&nbsp;{  
&nbsp;&nbsp;&nbsp;read( fd, buf, sizeof(buf) );  
&nbsp;&nbsp;&nbsp;printf("Message from Client: %sn",buf );  
&nbsp;&nbsp;&nbsp;sleep(3);  
&nbsp;&nbsp;}  
&nbsp;&nbsp;close( fd );  
&nbsp;}  
&nbsp;else  
&nbsp;{  
&nbsp;&nbsp;printf("Error");  
&nbsp;}  
&nbsp;return 0;  
}

