---
layout: post
title: Debian/Ubuntu Linux（VPS）搭建L2TP/IPSec VPN服务器
date: 2014-01-25 22:57:08.000000000 -08:00
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
  bot_views: '7'
  views: '4102'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/1093.html"
---
尝试过直接用PPTP搭建VPN，但效果不理想，然后转而搭建一个L2TP/IPSec&nbsp;VPN服务器，期间遇到过很多问题，尝试过CentOS，最后还是在Ubuntu下终于顺利解决了。留给大家参考。

**说明：**

YOUR-HOST-IP：指你主机的公网IP地址，如果你没有公网IP地址，请直接关闭此页面！

YOUR-PSK-SECRET：指你的IPSec预设共享密钥

&nbsp;

**操作：** &nbsp;

a）安装依赖软件

$sudo&nbsp;apt-get&nbsp;install&nbsp;ppp&nbsp;openswan&nbsp;xl2tpd&nbsp;iptables&nbsp;lsof

&nbsp;

注意：如果安装过程中遇到如下错误，请确认系统中是否已安装xl2tp类似服务。我被此问题困扰了很久，最终通过仔细翻阅错误日志（/var/log/syslog）才发现原来此错误是由于xl2tpd启动需要绑定的1701端口被占用导致。

```bash
Setting up xl2tpd (1.2.7+dfsg-1) ... Starting xl2tpd: invoke-rc.d: initscript xl2tpd, action "start" failed. dpkg: error processing xl2tpd (--configure): subprocess installed post-installation script returned error exit status 1 Errors were encountered while processing: xl2tpd E: Sub-process /usr/bin/dpkg returned an error code (1)
```

&nbsp;<!--more-->

b）配置PPP

$sudo&nbsp;vim&nbsp;/etc/ppp/options.xl2tpd

```actionscript3
require-mschap-v2 ms-dns 208.67.222.222 ms-dns 208.67.220.220 asyncmap 0 auth crtscts lock hide-password modem debug name l2tpd proxyarp lcp-echo-interval 30 lcp-echo-failure 4 mtu 1400 noccp connect-delay 5000
```

注意：

1)&nbsp;此处我选择使用openDNS服务，如果你有其他选择请修改ms-dns配置项。

2)&nbsp;最后三行的配置项是针对OS&nbsp;X/iOS而设置，如果不添加此三行，windows/andriod均可正常连接VPN服务，但OS&nbsp;X/iOS则无法连接。

&nbsp;

c）配置IPSec

$sudo&nbsp;vim&nbsp;/etc/ipsec.conf

```actionscript3
# conforms to second version of ipsec.conf specification version2.0 # basic configuration config setup # NAT-TRAVERSAL support, see README.NAT-Traversal nat\_traversal=yes # exclude networks used on server side by adding %v4:!a.b.c.0/24 virtual\_private=%v4:10.0.0.0/8,%v4:192.168.0.0/16,%v4:172.16.0.0/12 # OE is now off by default. Uncomment and change to on, to enable. oe=off # which IPsec stack to use. auto will try netkey, then klips then mast protostack=auto conn L2TP-PSK-NAT rightsubnet=vhost:%priv also=L2TP-PSK-noNAT conn L2TP-PSK-noNAT authby=secret pfs=no auto=add keyingtries=3 rekey=no ikelifetime=12h keylife=1h type=transport left=YOUR-HOST-IP leftprotoport=17/1701 right=%any rightprotoport=17/%any dpddelay=40 dpdtimeout=130 dpdaction=clear
```

&nbsp;

注意：最后三行dpd\*配置项是为OS&nbsp;X/iOS而配置，如果你的OS&nbsp;X/iOS设备仍然无法连接VPN服务器，请适当修改dpddelay和dpdtimeout项的值。修改后仍然无法连接者，去看/var/log/syslog日志吧！

&nbsp;

d）配置XL2TPD

$sudo&nbsp;vim&nbsp;/etc/xl2tpd/xl2tpd.conf

&nbsp;

```actionscript3
[global] ipsec saref = yes [lns default] ip range = 10.1.2.2-10.1.2.254 local ip = 10.1.2.1 refuse chap = yes refuse pap = yes require authentication = yes length bit = yes pppoptfile = /etc/ppp/options.xl2tpd ppp debug = yes
```

&nbsp;

注意：

1)&nbsp;ip&nbsp;range配置项是客户端分配IP段定义，此处一般无需修改。如果你的系统中与此值存在冲突，我想你已经明白如何做了！

2)&nbsp;ppp&nbsp;debug配置项指定是否开启PPP调试日志，默认PPP日志会输出到/var/log/syslog文件。

&nbsp;

e）配置IPSec预设共享密钥

$sudo&nbsp;vim&nbsp;/etc/ipsec.secrets

_#&nbsp;PSK_

_YOUR-HOST-IP&nbsp;%any&nbsp;:&nbsp;PSK&nbsp;"YOUR-PSK-SECRET"_

&nbsp;

f）配置iptables规则，（我这里eth1为机器的外网网卡）

$sudo iptables -t nat -A POSTROUTING -s 10.161.173.0/24 -o eth1 -j MASQUERADE

&nbsp;

g）保存并配置重启后的iptables。

$ iptables-save \> /etc/iptables-rules

修改/etc/network/interfaces，在eth1下up语句前添加：

pre-up iptables-restore \< /etc/iptables-rules

&nbsp;

h）添加L2TP/IPSec&nbsp;VPN账号

$sudo&nbsp;vim&nbsp;/etc/ppp/chap-secrets

&nbsp;

_#user&nbsp;&nbsp;&nbsp;&nbsp;server&nbsp;&nbsp;&nbsp;&nbsp;password&nbsp;&nbsp;&nbsp;&nbsp;ip_

_test&nbsp;&nbsp;&nbsp;&nbsp;\*&nbsp;&nbsp;&nbsp;&nbsp;test-passwd&nbsp;&nbsp;&nbsp;&nbsp;\*_

_test2 &nbsp; &nbsp;xl2tpd&nbsp;&nbsp;&nbsp;&nbsp;test2-passwd&nbsp;&nbsp;&nbsp;&nbsp;\*_

&nbsp;

i）配置/etc/sysctl.conf，以允许转发。首先，找到net.ipv4.ip\_forward项，修改为：

net.ipv4.ip\_forward=1

然后，运行如下命令：

#sysctl -p

&nbsp;

j）重启IPSec

$sudo&nbsp;/etc/init.d/ipsec&nbsp;restart

&nbsp;

k）重启XL2TPD

$sudo&nbsp;/etc/init.d/xl2tpd&nbsp;restart

&nbsp;

注意：如果服务都能正常启动，但客户端无法连接VPN服务器，你可以停止xl2tpd（$sudo&nbsp;/etc/init.d/xl2tpd&nbsp;stop）后在命令行使用$sudo&nbsp;xl2tpd&nbsp;-D命令以调试模式启动，然后就看日志吧！

&nbsp;

阿里云服务器搭建vpn需要注意两点：

① PPTP配置里面的 localip&nbsp;&nbsp; remoteip 的IP段要和内网IP属于同一网段

②执行 这个的时候 iptables -t nat -A POSTROUTING -s 10.129.9.0/24 -o eth1 -j MASQUERADE  
 要把“eth1” 修改成你对应的外网网卡，阿里云的服务器是双网卡的可能跟别的有些不同。

&nbsp;

**附服务器接入常见问题总结：**

**1、VPN客户端拨入时出现721错误：**

这种情况大数多原因为客户系统，如果为WINXP并且安装了SP2，则可能会出现这种情况，解决方法为：修改注册表HKEY\_LOCAL\_MACHINE[SYSTEM](http://www.ha97.com/tag/system "SYSTEM")CurrentControlSetControlClass{4D36E972-E325-11CE-BFC1-08002bE10318}，其中其中 是 WAN 微型端口 (PPTP) 驱动程序的网络适配器，在此项中新建一个DWORD 值ValidateAddress，然后设置为0即可。  
服务器端PPP协议配置不正确也会导致此类错误。

**2、VPN客户端拨入时出现800错误：**

这种情况大数多原因为客户系统连接服务器时使用域名，因临时DNS无法解析而出现这种错误，可更换DNS试一下，如果还是出错此类错误，则可能是无法连接到VPN服务器，可能是VPN服务器关闭或出现故障，也可能是客户电脑上的防火墙阻止了VPN连接请求，可关闭防火墙试一下。  
有些使用中转服务器连接到VPN服务器的客户端，也可能出现此类错误，原因为中转服务器中转功能出现故障。

**3、VPN客户端拨入时出现619错误：**

这种情况大数多原因为客户机连接Internet的网关（如家庭宽带路由或公司上网网关路由或防火墙）NAT-T功能关闭或对VPN支持性不好，主要是对GRE及PPTP协议的NAT-T不支持。可打开网关路由的NAT-T功能，如果还是出现错误，则需要更换网关设备，现在市面上大多数设备已经支持。

**4、VPN客户端拨入时出现691错误：**

这种情况大数多原因为客户机连接VPN服务器异常中断，因多数服务器限制一个帐户同时只有一个人使用，所以一旦异常断开，则需等待3分钟左右。有些VPN服务器没有设置异常断线检查功能也可能导致用户一旦异常断开后很长时间不能连接。所以解决办法为在服务器上设置异常断线检查程序或功能。

**5、VPN客户端拨入时出现733错误：**

这种情况大数多原因为客户机拨入VPN服务器后无法获取IP地址，可修复DHCP服务器或设置静态IP地址或地址池。

**6、VPN客户端拨入时出现734 ppp链接控制协议终止：**

这种情况多数为VPN服务器配置有问题，如果是PPP配置有问题，不支持MPPE加密或支持度不好。请重新编译PPP及MPPE相关程序。对于用于游戏代理的用户，可不使用加密（需在服务器端不要求加密）。

**7、VPN客户端拨入时出现718错误：**

拨入时用户名和密码出错误，有时也因为服务器端认证服务出现故障。

