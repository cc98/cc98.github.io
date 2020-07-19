---
layout: post
title: vc中socket编程步骤及实例
date: 2010-08-09 22:41:30.000000000 -07:00
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
  _wp_old_slug: ''
  views: '3209'
  bot_views: '5'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/114.html"
---
sockets（套接字）编程有三种，流式套接字（SOCK\_STREAM），数据报套接字（SOCK\_DGRAM），原始套接字（SOCK\_RAW）；基于TCP的socket编程是采用的流式套接字。在这个程序中，将两个工程添加到一个工作区。要链接一个ws2\_32.lib的库文件。

服务器端编程的步骤：

1：加载套接字库，创建套接字(WSAStartup()/socket())；

2：绑定套接字到一个IP地址和一个端口上(bind())；

3：将套接字设置为监听模式等待连接请求(listen())；

4：请求到来后，接受连接请求，返回一个新的对应于此次连接的套接字(accept())；

5：用返回的套接字和客户端进行通信(send()/recv())；

6：返回，等待另一连接请求；

7：关闭套接字，关闭加载的套接字库(closesocket()/WSACleanup())。

服务器端代码如下：

<!--more-->

#include \<stdio.h\>  
#include \<Winsock2.h\>  
void main()  
{  
&nbsp;WORD wVersionRequested;  
&nbsp;WSADATA wsaData;  
&nbsp;int err;  
&nbsp;  
&nbsp;wVersionRequested = MAKEWORD( 1, 1 );  
&nbsp;  
&nbsp;err = WSAStartup( wVersionRequested, wsaData );  
&nbsp;if ( err != 0 ) {  
&nbsp; return;  
&nbsp;}  
&nbsp;  
&nbsp;if ( LOBYTE( wsaData.wVersion ) != 1 ||  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HIBYTE( wsaData.wVersion ) != 1 ) {  
&nbsp;&nbsp; WSACleanup( );  
&nbsp; return;  
&nbsp;}  
&nbsp;SOCKET sockSrv=socket(AF\_INET,SOCK\_STREAM,0);

&nbsp;SOCKADDR\_IN addrSrv;  
&nbsp;addrSrv.sin\_addr.S\_un.S\_addr=htonl(INADDR\_ANY);  
&nbsp;addrSrv.sin\_family=AF\_INET;  
&nbsp;addrSrv.sin\_port=htons(6000);  
&nbsp;  
&nbsp;bind(sockSrv,(SOCKADDR\*)addrSrv,sizeof(SOCKADDR));

&nbsp;listen(sockSrv,5);

&nbsp;SOCKADDR\_IN addrClient;  
&nbsp;int len=sizeof(SOCKADDR);  
&nbsp;while(1)  
&nbsp;{  
&nbsp;&nbsp; SOCKET sockConn=accept(sockSrv,(SOCKADDR\*)addrClient,len);  
&nbsp; char sendBuf[50];  
&nbsp;&nbsp; sprintf(sendBuf,"Welcome %s to here!",inet\_ntoa(addrClient.sin\_addr));  
&nbsp;&nbsp; send(sockConn,sendBuf,strlen(sendBuf)+1,0);  
&nbsp; char recvBuf[50];  
&nbsp;&nbsp; recv(sockConn,recvBuf,50,0);  
&nbsp;&nbsp; printf("%sn",recvBuf);  
&nbsp;&nbsp; closesocket(sockConn);  
&nbsp;}

}

客户端编程的步骤：

1：加载套接字库，创建套接字(WSAStartup()/socket())；

2：向服务器发出连接请求(connect())；

3：和服务器端进行通信(send()/recv())；

4：关闭套接字，关闭加载的套接字库(closesocket()/WSACleanup())。

客户端的代码如下：

#include \<stdio.h\>  
#include \<Winsock2.h\>  
void main()  
{  
&nbsp;WORD wVersionRequested;  
&nbsp;WSADATA wsaData;  
&nbsp;int err;  
&nbsp;  
&nbsp;wVersionRequested = MAKEWORD( 1, 1 );  
&nbsp;  
&nbsp;err = WSAStartup( wVersionRequested, wsaData );  
&nbsp;if ( err != 0 ) {  
&nbsp; return;  
&nbsp;}  
&nbsp;  
&nbsp;if ( LOBYTE( wsaData.wVersion ) != 1 ||  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HIBYTE( wsaData.wVersion ) != 1 ) {  
&nbsp;&nbsp; WSACleanup( );  
&nbsp; return;  
&nbsp;}  
&nbsp;SOCKET sockClient=socket(AF\_INET,SOCK\_STREAM,0);  
&nbsp;  
&nbsp;SOCKADDR\_IN addrSrv;  
&nbsp;addrSrv.sin\_addr.S\_un.S\_addr=inet\_addr("127.0.0.1");  
&nbsp;addrSrv.sin\_family=AF\_INET;  
&nbsp;addrSrv.sin\_port=htons(6000);  
&nbsp;connect(sockClient,(SOCKADDR\*)addrSrv,sizeof(SOCKADDR));  
&nbsp;send(sockClient,"hello",strlen("hello")+1,0);  
&nbsp;char recvBuf[50];  
&nbsp;recv(sockClient,recvBuf,50,0);  
&nbsp;printf("%sn",recvBuf);  
&nbsp;  
&nbsp;closesocket(sockClient);  
&nbsp;WSACleanup();  
}

===============================================

完美分界线，以下为示例：

1.TCP服务器端:

#include  
#include

void main()  
{  
WORD wVersionRequested;  
WSADATA wsaData;  
int err;

wVersionRequested = MAKEWORD( 1, 1 );

err = WSAStartup( wVersionRequested, &wsaData );  
if ( err != 0 ) {  
return;  
}  
if ( LOBYTE( wsaData.wVersion ) != 1 ||  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HIBYTE( wsaData.wVersion ) != 1 ) {  
WSACleanup( );  
return;  
}  
SOCKET sockSrv=socket(AF\_INET,SOCK\_STREAM,0);

SOCKADDR\_IN addrSrv;  
addrSrv.sin\_addr.S\_un.S\_addr=htonl(INADDR\_ANY);  
addrSrv.sin\_family=AF\_INET;  
addrSrv.sin\_port=htons(6000);

bind(sockSrv,(SOCKADDR\*)&addrSrv,sizeof(SOCKADDR));

listen(sockSrv,5);

SOCKADDR\_IN addrClient;  
int len=sizeof(SOCKADDR);

while(1)  
{  
SOCKET sockConn=accept(sockSrv,(SOCKADDR\*)&addrClient,&len);  
char sendBuf[100];  
sprintf(sendBuf,"Welcome %s to [http://www.sunxin.org](http://www.sunxin.org)",  
&nbsp;&nbsp; inet\_ntoa(addrClient.sin\_addr));  
send(sockConn,sendBuf,strlen(sendBuf)+1,0);  
char recvBuf[100];  
recv(sockConn,recvBuf,100,0);  
printf("%sn",recvBuf);  
closesocket(sockConn);  
}  
}

2.TCP客户端：

#include  
#include

void main()  
{  
WORD wVersionRequested;  
WSADATA wsaData;  
int err;

wVersionRequested = MAKEWORD( 1, 1 );

err = WSAStartup( wVersionRequested, &wsaData );  
if ( err != 0 ) {  
return;  
}  
if ( LOBYTE( wsaData.wVersion ) != 1 ||  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HIBYTE( wsaData.wVersion ) != 1 ) {  
WSACleanup( );  
return;  
}  
SOCKET sockClient=socket(AF\_INET,SOCK\_STREAM,0);

SOCKADDR\_IN addrSrv;  
addrSrv.sin\_addr.S\_un.S\_addr=inet\_addr("127.0.0.1");  
addrSrv.sin\_family=AF\_INET;  
addrSrv.sin\_port=htons(6000);  
connect(sockClient,(SOCKADDR\*)&addrSrv,sizeof(SOCKADDR));

char recvBuf[100];  
recv(sockClient,recvBuf,100,0);  
printf("%sn",recvBuf);  
send(sockClient,"This is lisi",strlen("This is lisi")+1,0);

closesocket(sockClient);  
WSACleanup();  
}

3.UDP服务器端

#include  
#include

void main()  
{  
WORD wVersionRequested;  
WSADATA wsaData;  
int err;

wVersionRequested = MAKEWORD( 1, 1 );

err = WSAStartup( wVersionRequested, &wsaData );  
if ( err != 0 ) {  
return;  
}  
if ( LOBYTE( wsaData.wVersion ) != 1 ||  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HIBYTE( wsaData.wVersion ) != 1 ) {  
WSACleanup( );  
return;  
}

SOCKET sockSrv=socket(AF\_INET,SOCK\_DGRAM,0);  
SOCKADDR\_IN addrSrv;  
addrSrv.sin\_addr.S\_un.S\_addr=htonl(INADDR\_ANY);  
addrSrv.sin\_family=AF\_INET;  
addrSrv.sin\_port=htons(6000);

bind(sockSrv,(SOCKADDR\*)&addrSrv,sizeof(SOCKADDR));

SOCKADDR\_IN addrClient;  
int len=sizeof(SOCKADDR);  
char recvBuf[100];

recvfrom(sockSrv,recvBuf,100,0,(SOCKADDR\*)&addrClient,&len);  
printf("%sn",recvBuf);  
closesocket(sockSrv);  
WSACleanup();  
}

4.UDP客户端

#include  
#include

void main()  
{  
WORD wVersionRequested;  
WSADATA wsaData;  
int err;

wVersionRequested = MAKEWORD( 1, 1 );

err = WSAStartup( wVersionRequested, &wsaData );  
if ( err != 0 ) {  
return;  
}  
if ( LOBYTE( wsaData.wVersion ) != 1 ||  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HIBYTE( wsaData.wVersion ) != 1 ) {  
WSACleanup( );  
return;  
}

SOCKET sockClient=socket(AF\_INET,SOCK\_DGRAM,0);  
SOCKADDR\_IN addrSrv;  
addrSrv.sin\_addr.S\_un.S\_addr=inet\_addr("127.0.0.1");  
addrSrv.sin\_family=AF\_INET;  
addrSrv.sin\_port=htons(6000);

sendto(sockClient,"Hello",strlen("Hello")+1,0,  
(SOCKADDR\*)&addrSrv,sizeof(SOCKADDR));  
closesocket(sockClient);  
WSACleanup();  
}

