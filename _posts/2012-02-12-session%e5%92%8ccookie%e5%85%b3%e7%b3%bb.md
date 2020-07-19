---
layout: post
title: Session和Cookie关系
date: 2012-02-12 23:15:59.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Share
tags: []
meta:
  _edit_last: '1'
  bot_views: '2'
  views: '2573'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/419.html"
---
| 网上看到，留作记录。

PHP中的session可以默认情况下是使用客户端的Cookie(以便和普通意义上的Cookie区别,我称之为session cookie,普通意义上的Cookie为Cookie)来保存session id的,但是PHP中的session是否只能使用session cookie呢?当然不是,否则何必还弄个session出来,不如直接用Cookie算了.Session的一大优点就是当客户端的Cookie被禁用时会自动把session id附在URL中,这样再通过session id就能记住session变量了.&nbsp;$ T5 I# S: c: W9 B. X7 T- b  
下面我写两个文件来证实一下,首先在浏览器中设置禁用Cookie.&nbsp;\* ], N/ Q1 \_7 Z9 ) E& p' g  
\<? //文件名为test1.php  
session\_start();&nbsp;4 k! Z) o' q$ z) B- w/ o+ L! V  
session\_register("url");  
$url="test2.php";  
echo "\<a href=$url\>goto test2.php\</a\>  
";  
?\>  
<!--more-->  
\<?//文件名为test2.php  
session\_start();  
if (session\_is\_registered("url")) {  
echo "Congratulations." q$ c" U- w# i/ B- j5 R' B&nbsp;&nbsp;J  
";  
$url="test1.php";&nbsp;$ t) ]&nbsp;&nbsp;Q7 N&nbsp;&nbsp;S1 D\* R( b4 Z  
echo "\<a href=$url\>goto test1.php\</a\>  
";  
}  
else echo "Failed.\* E5 d4 E6 G4 u. f&nbsp;&nbsp;`& M  
";&nbsp;/ [2 e% w( [$ k( G. O  
?\>&nbsp;% ]( V; d) i0 m% F9 t" W" ]3 h  
现在在浏览器中输入"http://localhost/test1.php",把鼠标移到链接上看看状态栏上的地址,不是简单的"http://localhost/test2.php",而是这种形式:"http://localhost/test2.php?PHPSESSID=6e3610749f7ded3784bc4a4dd10f879b".你还可以查看Html的源文件,源文件是这种形式:&nbsp;, A& V4 Z" L0 s  
\<a href="test2.php?PHPSESSID=6e3610749f7ded3784bc4a4dd10f879b"\>goto test2.php\</a\>  
所以说这完全是PHP的功劳,和浏览器无关,也就是说无论你用什么浏览器session都有效,而不是有的人认为的只对IE有用.  
但是,我们的超链接是语句是由echo语句输出的,如果超链接不包含在PHP的标签\<? ?\>之内会怎样呢?还是写个例子来验证一下,把test1.php稍作修改:&nbsp;$ {0 G, a1 F. ?/ p/ y\* a/ W  
\<?&nbsp;) I9 r- F) F. j8 P  
session\_start();&nbsp;6 ?$ P" J& i- e  
session\_register("url");&nbsp;0 A# O. ?7 J4 O$ ]  
$url="test2.php";  
echo "\<a href=$url\>goto test2.php\</a\>( T6 c: b' d! g& x$ X, \_  
";&nbsp;. K7 l; ^' p+ a&nbsp;&nbsp;]& Z; t' h+ r

?\>  
\<a href="test2.php"\>(Html形式)goto test2.php\</a\>&nbsp;\* e3 k\* I0 L& ]# 7 |$ K  
在浏览器中输入"http://localhost/test1.php",分别把鼠标移到两个链接上看看有没有不同?可以看到,两个链接是完全相同的,后面都会自动附带session id.所以不必担心没被包含在PHP标签中的链接会失效,PHP不会这么笨的.&nbsp;5 Q7 c, ^9 v/ G, r; Q8 t  
但是在使用时要注意必须先用session\_start()函数告诉PHP开始用session,哪怕你在这个文件中只有html代码,如:  
\<? session\_start();?\>&nbsp;\* I5 y4 N4 Y# S8 g  
\<html\>&nbsp;( H&nbsp;&nbsp;v, `+ M# }  
\<head\>&nbsp;1 l% D5 s9 [6 D' N/ q6 {  
\<body\>&nbsp;0 E$ y& ~& H- L5 i! u4 A( o0 l&nbsp;&nbsp;p  
\<a href=test2.php\>gogogo\</a\>  
…………&nbsp;) K\* i1 j% i& p) Y, P$ I0 c

记得有人说过这个优点只能在linux/unix下才能发挥出来,而我用的Win2000p+Apache1.3.17+Php4.0.4pl1,PHP为Apache模块方式,却照样可以.恰恰相反,我转到linux下去测试时反而不行了.其实是在编译时的一个选项--enable-trans-sid控制了这项功能能否有用.而按照PHP默认来编译时是没有打开这项功能的,只需重新编译时加入它就可以了.我的配置为Apache1.3.17+Php4.0.4pl1,PHP为Apache模块方式,在linux重新编译后用Netscape Navigator4.7测试可以通过(这更证明了和浏览器无关).&nbsp;8 O- `( U( t) y  
只靠session是不能跨窗口使用的,即使你启用了Cookie,当你在一个窗口中有一个合法的session id(记录在session cookie中,不是URL中),再新开一个窗口进入相同页面时,你会重新拥有一个新的session id,而与前一个窗口互不影响.要想跨窗口使用同一个session id就只能在URL后指定session id,也就是说如果你把带有session id的的窗口的URL复制,在新开的窗口中粘贴一下,还是照样使用的.知道了session id的这个原理要实现跨窗口session还是不难的,可以把Cookie与session结合起来,首先取得当前合法的session id,然后把它记录在Cookie中,在其它窗口读取Cookie就可获得当前的Session id了.具体实现我记得在phpuser上有一篇文章专门讨论过.  
最后再说一下:&nbsp;. x( P\* V) z; M( `  
①经常有人问到"为什么copy你写好的代码,却会出错,你也太……",再把出错提示拿来一看:  
Warning: open(/tmpsess\_eca1da208748db2e9c6bec1fccc182b4, O\_RDWR) failed: m (2) in c:/www/test1.php on line 2&nbsp;% U" Q9 Z, {\* z5 v+ t# A  
其实是他自己的问题:session存放的路径/tmp不存在.有两种办法:一是在根目录(一般是C:)建一个名为tmp的目录;二是修改php.ini文件&nbsp;6 p\* t) ]&nbsp;&nbsp;V& m. `1 |% M+ `  
session.save\_path = /tmp ;&nbsp;4 t\* U6 P) ~7 Y  
把/tmp目录用绝对路径指定一个目录(当然必须存在),如我的php.ini中  
session.save\_path = G:PHPtempsession ;  
②还有一种情况的出错信息为:&nbsp;& s5 y; F: h) }9 G7 B' D3 D  
Warning: Cannot send session cache limiter - headers already sent (output started at  
c:/www/test1.php:1) in c:/www/test1.php on line 2  
这是因为你在用session\_start()之前已经数据输出到客户端了,比如说Html标签、文字甚至是空格都不行,所以最好在程序第一句就用session\_start().

 |

