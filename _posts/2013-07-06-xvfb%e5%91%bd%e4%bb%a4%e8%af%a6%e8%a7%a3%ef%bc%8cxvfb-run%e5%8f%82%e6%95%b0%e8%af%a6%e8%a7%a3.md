---
layout: post
title: xvfb命令详解，xvfb-run参数详解
date: 2013-07-06 22:42:56.000000000 -07:00
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
  bot_views: '8'
  views: '2404'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/1043.html"
---
#### 最近在做一个生成网站缩略图的功能，从网上查到相关资料，现与大家分享，xvfb这个软件，安装上之后一条命令就能执行此操作。很容易的就生成了自己想要的缩略图。

```bash
xvfb-run --server-args="-screen 0, 1024x768x24" cutycapt --url=http://www.sina.com.cn --out=localfile1.png --body-string=utf-8
```

#### 下面是对这个软件参数的解释

#### NAME  
xvfb-run -运行在一个虚拟的X服务器环境中的指定的X客户端或命令。

#### SYNOPSIS  
xvfb的运行 [选项] 命令

#### DESCRIPTION  
xvfb-run是一个包装的Xvfb（1X）命令，在一个虚拟的X服务器环境，简化了任务的运行命令（通常是一个X客户端，或一个脚本，其中包含一个可以运行的客户端列表）。xvfb-run设置X授权机构的文件（或使用现有  
的用户指定的），写一个cookie（见XAUTH（1X）），然后启动的Xvfb X服务器作为后台进程的进程IDXvfb来存储供以后使用。指定的命令然后运行使用的X，显示相应的Xvfb服务器刚开始的X授权文件前面创建的。当命令退出  
时，其状态保存，被杀害的Xvfb服务器（使用以前存储的进程ID），在X授权机构的cookie删除，并授权文件删除（如果用户没有指定一个使用）。  
xvfb的运行，然后退出命令的退出状态，除了在错误条件（见EXIT STATUS以下）。xvfb-run需要XAUTH命令的功能。

#### <!--more-->

#### OPTIONS  
-a, –auto-servernum  
尝试得到一个免费的服务器数量，开始于99，或参数 –server-num.

#### -e file, –error-file=file  
将输出存储在文件XAUTH和Xvfb中。默认的是/dev/null。

#### -f file, –auth-file=file  
存储X验证数据文件。默认情况下，一个临时目录XVFB运行。 PID（PID是XVFB运行本身的进程ID）中创建的环境变量TMPDIR指定的目录（/tmp目录如果该变量为null，或者未设置），和临时文件（1）命令被  
用来创建该临时目录中的一个文件名为XAUTHORITY。

#### -h, –help  
显示用法信息并退出。

#### -n servernumber, –server-num=servernumber  
使用servernumber的服务器数量（但看到的-自动SERVERNUM选项以上）。默认值是99。

#### -l, –listen-tcp  
启用TCP 监听TCP端口监听在X服务器上。出于安全原因（为了避免拒绝服务攻击或攻击），默认情况下禁用TCP端口倾听。

#### -p protocolname, –xauth-protocol=protocolname  
使用protocolname X授权机构的协议使用。默认是’XAUTH’，解释为自己的默认协议，它是MIT-MAGIC-COOKIE-1。

#### -s arguments, –server-args=arguments  
传递参数到xvfb服务器。小心引用任何空格内可能发生的争议，预防他们为自己的论点xvfb运行分离器。同时，注意规范’-nolisten tcp’的争论可能会覆盖xvfb运行自己的- L的功能，——listen-tcp选项，  
以及规范的服务器数量（例如，“1”）可能会被忽略，因为这样的X服务器解析其参数列表。

#### -w delay, –wait=delay  
等待延迟秒后发射xvfb之前从指定的命令。默认值为3。  
ENVIRONMENT  
COLUMNS  
表明在特定的终端设备的宽度。这个值是用于格式化诊断消息。如果不是终端查询使用stty（1）确定其宽度。如果失败，值为“80”。

#### TMPDIR  
指定的目录中运行的地方xvfb临时对X权威文件存储目录；如果只使用了-f or –auth-file选项是没有被指定。

#### OUTPUT FILES  
除非-f or –auth-file 选项是指定的，临时的在其中创建目录和文件（和删除）来存储X权威的饼干的xvfb服务器和客户端使用的（S）在其下运行。看到tempfile（1）。如果F或——授权文件，然后指定x权威文件只写，不能创建或删除（尽管XAuth创建一个权威文件本身如果要求使用使用不已经存在）。与用户指定的名称错误文件用 -e 或创建——error-file选项。

&nbsp;

Xvfb命令参数详情：

use: X [:\<display\>] [option]  
-a # default pointer acceleration (factor)  
-ac disable access control restrictions  
-audit int set audit trail level  
-auth file select authorization file  
-br create root window with black background  
+bs enable any backing store support  
-bs disable any backing store support  
-c turns off key-click  
c # key-click volume (0-100)  
-cc int default color visual class  
-nocursor disable the cursor  
-core generate core dump on fatal error  
-dpi int screen resolution in dots per inch  
-dpms disables VESA DPMS monitor control  
-deferglyphs [none|all|16] defer loading of [no|all|16-bit] glyphs  
-f # bell base (0-100)  
-fc string cursor font  
-fn string default font name  
-fp string default font path  
-help prints message with these options  
-I ignore all remaining arguments  
-ld int limit data space to N Kb  
-lf int limit number of open files to N  
-ls int limit stack space to N Kb  
-nolock disable the locking mechanism  
-nolisten string don't listen on protocol  
-noreset don't reset after last client exists  
-background [none] create root window with no background  
-nr (Ubuntu-specific) Synonym for -background none  
-reset reset after last client exists  
-p # screen-saver pattern duration (minutes)  
-pn accept failure to listen on all ports  
-nopn reject failure to listen on all ports  
-r turns off auto-repeat  
r turns on auto-repeat  
-render [default|mono|gray|color] set render color alloc policy  
-retro start with classic stipple and cursor  
-s # screen-saver timeout (minutes)  
-t # default pointer threshold (pixels/t)  
-terminate terminate at server reset  
-to # connection time out  
-tst disable testing extensions  
ttyxx server started from init on /dev/ttyxx  
v video blanking for screen-saver  
-v screen-saver without video blanking  
-wm WhenMapped default backing-store  
-wr create root window with white background  
-maxbigreqsize set maximal bigrequest size  
+xinerama Enable XINERAMA extension  
-xinerama Disable XINERAMA extension  
-dumbSched Disable smart scheduling, enable old behavior  
-schedInterval int Set scheduler interval in msec  
-sigstop Enable SIGSTOP based startup  
+extension name Enable extension  
-extension name Disable extension  
-query host-name contact named host for XDMCP  
-broadcast broadcast for XDMCP  
-multicast [addr [hops]] IPv6 multicast for XDMCP  
-indirect host-name contact named host for indirect XDMCP  
-port port-num UDP port number to send messages to  
-from local-address specify the local address to connect from  
-once Terminate server after one session  
-class display-class specify display class to send in manage  
-cookie xdm-auth-bits specify the magic cookie for XDMCP  
-displayID display-id manufacturer display ID for request  
[+-]accessx [timeout [ timeout\_mask [ feedback [ options\_mask] ] ] ]  
enable/disable accessx key sequences  
-ardelay set XKB autorepeat delay  
-arinterval set XKB autorepeat interval  
-screen scrn WxHxD set screen's width, height, depth  
-pixdepths list-of-int support given pixmap depths  
+/-render turn on/off RENDER extension support(default on)  
-linebias n adjust thin line pixelization  
-blackpixel n pixel value for black  
-whitepixel n pixel value for white  
-fbdir directory put framebuffers in mmap'ed files in directory  
-shmem put framebuffers in shared memory

