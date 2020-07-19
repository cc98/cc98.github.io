---
layout: post
title: Mac OS X Snow Leopard(安装教程)
date: 2010-07-09 17:12:06.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Share
tags:
- apple
- Guide
- Mac OS
meta:
  _edit_last: '1'
  _wp_old_slug: ''
  bot_views: '6'
  views: '4158'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/48.html"
---
<p>昨天刚在笔记本上装了mac os，现在使用双系统（win7+mac），电脑配置一般，但运行速度也都还不错，一般运行没感觉有什么影响。个人感觉苹果的驱动方面也没那么难搞，thinkpad的TrackPoint也都直接能用，声卡找万能<a href="http://www.namipan.com/d/VoodooHDA.kext.zip/cefd54a12f7661ee8262648f8cd780ec0e555fc050760200" target="_blank">VoodooHDA.kext</a> 驱动一般都行；显卡，[<span style="color: #ff0000;">nVidia</span>]<a href="http://home.pcbeta.com/link.php?url=http://goo.gl/fLJK" target="_blank">Natit+NVinject+NVEnabler</a>(任选一个使用就可以，不要一起使用！)，但是最高还是只能1280*800的，一般还是没影响。有线网卡直接能用，无线网卡就悲剧了。。</p>
<p>推荐！新手安装指南：<a href="http://bbs.pcbeta.com/thread-592288-1-1.html">一步一步在Windows安装苹果雪豹系统</a></p>
<p>公认网上最详细的教程。一步一步照着做，挺简单的。</p>
<p>但最后一步，原文中这样写的</p>
<p>“将雪豹安装DVD从硬盘赶走，取回6.3G的空间。很简单，用第一步的方法，打开磁盘管理，对准6.3G的分区，右键点击删除卷。如果你删除了雪豹分区就是白忙一次了。6.3G变成未分配空间后，在D盘按右键扩展卷，狂按下一步即完成任务。”</p>
<p><strong>注意：</strong>如果你这6.3G不是从D盘缩小得到，就不能通过D盘扩大容量把这个空间加进去。</p>
<p><strong>删除之后，会导致选择bootthink会直接重启，</strong>这个是普遍遇到的问题!</p>
<p><!--more--></p>
<p>以下引用pcbeta上的 [教程] 解决Bootthink自动重启问题</p>
<p>解决方法：<span style="color: #ff0000;">为HFS分区重新标记AF标识</span>。（同样适合其它原因导致分区被改变或破坏）”<br />
其实将雪豹的系统分区（即所谓的HFS分区）重新标记为AF标识，也就是将雪豹的系统分区ID改为AF即可，这个是不需要额外的软件的，windows自带的磁盘分区命令即可实现。实践证明，这样改完了之后就可以安全删除雪豹的安装分区了（6.3G那个），解决了bootThink重启的问题。具体的步骤如下：<br />
1.<span style="color: #000000;">将雪豹安装DVD从硬盘赶走，取回6.3G的空间。很简单，用第一步的方法，打开磁盘管理，对准6.3G的分区，右键点击删除卷。如果你删除了雪豹分区就是白忙一次了。6.3G变成未分配空间后，在D盘按右键扩展卷，狂按下一步即完成任务。</span>“------<br />
2.打开windows开始菜单，在运行栏中输入：cmd，回车，打开windows命令窗口<br />
3.在命令窗口中键入：diskpart，回车，启动该程序，可能在vista或7中还会询问权限之类的，只管点是就好，打开diskpart窗口<br />
4.当光标前面变成DISKPART&gt;后，键入select disk 0 回车（此步即选择你安装雪豹的那个硬盘，如果是单硬盘的话，一般都是disk 0，注意disk和0之间有空格！！）<br />
5窗口提示：磁盘0是所选磁盘，再键入list partition 回车，屏幕显示硬盘上的各个分区<br />
6找到你的雪豹系统所在的分区，记住分区号，这里假设是x分区（你不会不知道你的雪豹安装在哪个分区了吧？？！晕，看大小不就知道了,hehehe）<br />
7.键入：select partition x，回车，屏幕提示：分区x是所选分区<br />
8键入：set ID=AF 回车，屏幕提示：diskpart已成功更改分区ID，大功告成！<br />
重启电脑，试试你的bootThink不会重启了吧，等你的好消息！再次感谢TCNJ0405</p>
<p>此外，你用diskpart运行set ID=AF时，<strong><span style="color: #ff0000;">也许会遇到不能进行操作的问题，</span></strong>OVERRIDE也不行。改用Acronis Disk Director标记也同样不行！</p>
<p><strong>引起的原因</strong>：因为在前面的步骤中，windows里面装的MacDrive在运行，结束掉进程也不行，要把这个卸载了重启，set id=AF就可以了。设置好之后，重启，再把MacDrive装上就可以再查看苹果的分区了。</p>
<p>另外：作者提供的MacDrive--License失效，在这里提供一个小工具<a href="http://www.fantasyblog.org/wp-content/uploads/2010/07/MacDriver-8-creak.zip">MacDriver 8 creak.rar </a><strong>以下是具体破解方法</strong></p>
<p>1、安装“一步一步在Windows安装苹果雪豹系统”帖子中提供的MacDrive 8。</p>
<p>2、解压MacDriver 8 creak.rar。</p>
<p>3、打开MacDrive+8+keygen.exe，<span style="color: #ff0000;">选择MacDrive v7</span><span style="color: #ff0000;">，是7，不是8！</span>然后单击Generate。将得到的Serial填入Active MacDrive 8中的Serial Number一栏。选择Show Other Activation Options，并单击下一步。</p>
<p>4、再单击下一步</p>
<p>5、将Computer ID填入到MacDrive+8+keygen.exe的Computer ID栏中，并单击Active。</p>
<p>6、将得到的Act. Code填入到Active MacDriver 8的Activation Code一栏，单击下一步完成注册。</p>
<p>Congratulations！</p>
<p><strong> </strong></p>
<p><strong>最后再附Kext安装方法</strong></p>
<p>在Bootthink下面安装kext非常简单，把下载回来的以.kext为后缀的文件夹，移动到路径C:DarwinSystemLibrarySLExtensions下面即可。Bootthink在启动苹果时会加载这些kext。以往的kext安装要在苹果下面进行，还需要处理权限问题。<span style="color: #000000;"><br />
</span><br />
<span style="font-family: 微软雅黑;"><span style="color: #000000;">------------------------
  
常用的一些kext：&nbsp;—— bootthink原来已经带有，这个kext模拟真正苹果机上的SMC部件，必备  
  
NullCPUPowerManagement.kext&nbsp;  
&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;—— 将电源管理功能禁用，解决IntelCPUPowerManagement.kext的HPET错误  
  
OpenHaltRestart.kext　　　—— 解决重启/关机无法断电问题  
PlatformUUID.kext　　　　 —— 解决Unable to determine UUID for host. Error : 35的问题  
2个要一起使用，提供传统PS/2插口鼠标/键盘或笔记本触摸板支持  
  
或  
ApplePS2Controller.kext  
AppleACPIPS2Nub.kext 组合  
2个要一起使用，如果Voodoo不工作，你可用ApplePS2Controller代替。

FakeSMC.kext

VoodooPS2Controller.kext&nbsp;&nbsp;  
AppleACPIPS2Nub.kext 组合

最后再次感谢samsonwts。。大家一起装雪豹玩玩，一起折腾。。

