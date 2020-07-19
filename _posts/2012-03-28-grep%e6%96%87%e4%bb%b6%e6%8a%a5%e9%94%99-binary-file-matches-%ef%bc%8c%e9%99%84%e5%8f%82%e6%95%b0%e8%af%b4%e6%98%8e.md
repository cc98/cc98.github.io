---
layout: post
title: grep文件报错 “Binary file ... matches” ，附参数说明
date: 2012-03-28 22:31:55.000000000 -07:00
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
  bot_views: '5'
  views: '4305'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/share/462.html"
---
问题：grep一个文件时，报错“Binary file ... matches”

使用命令 more时，内容可以正常看到

原因：文件为binary文件  
解决：strings vers.log.2010-03-09 | grep -i ‘mezimedia’  
或者 grep&nbsp;-a&nbsp;-i ‘mezimedia’ vers.log.2010-03-09

grep命令是linux下的行过滤工具，其参数繁多，下面就一一介绍个个参数的作用，希望对大家有所帮助。

grep -- print lines matching a pattern (将符合样式的该行列出)

◎语法: grep [options]  
PATTERN [FILE...]  
grep用以在file内文中比对相对应的部分，或是当没有指定档案时，  
由标准输入中去比对。 在预设的情况下，grep会将符合样式的那一行列出。

此外，还有两个程序是grep的变化型，egrep及fgrep。  
其中egrep就等同于grep -E ，fgrep等同于grep -F 。

<!--more-->

◎参数

1.&nbsp;-A NUM，--after-context=NUM  
除了列出符合行之外，并且列出后NUM行。

ex:&nbsp;&nbsp;&nbsp;$&nbsp; **grep&nbsp;-A 1&nbsp;panda file**  
(从file中搜寻有panda样式的行，并显示该行的后1行)

2.&nbsp;-a或--text  
grep原本是搜寻文字文件，若拿二进制的档案作为搜寻的目标，  
则会显示如下的讯息:&nbsp;Binary file 二进制文件名 matches&nbsp;然后结束。

若加上-a参数则可将二进制档案视为文本文件搜寻，  
相当于--binary-files=text这个参数。

ex:&nbsp;&nbsp;&nbsp; (从二进制档案mv中去搜寻panda样式)  
(错误!!!)  
$&nbsp; **grep&nbsp;panda&nbsp;mv**  
Binary file mv matches  
(这表示此档案有match之处，详见--binary-files=TYPE )  
$  
(正确!!!)  
$&nbsp; **grep&nbsp;-a&nbsp;panda&nbsp;mv**

3.&nbsp;-B NUM，--before-context=NUM  
与 -A NUM 相对，但这此参数是显示除符合行之外  
并显示在它之前的NUM行。

ex:&nbsp;&nbsp;&nbsp; (从file中搜寻有panda样式的行，并显示该行的前1行)  
$&nbsp; **grep&nbsp;-B 1&nbsp;panda file**

4.&nbsp;-C [NUM], -NUM, --context[=NUM]  
列出符合行之外并列出上下各NUM行，默认值是2。

ex:&nbsp;&nbsp;&nbsp; (列出file中除包含panda样式的行外并列出其上下2行)  
(若要改变默认值，直接改变NUM即可)  
$&nbsp;**grep&nbsp;-C[NUM]&nbsp;panda file**

5.&nbsp;-b, --byte-offset  
列出样式之前的内文总共有多少byte ..

ex:&nbsp;&nbsp;$&nbsp; **grep&nbsp;-b&nbsp;panda file**  
显示结果类似于:  
&nbsp;&nbsp; 0:panda  
66:pandahuang  
123:panda03

6.&nbsp;--binary-files=TYPE  
此参数TYPE预设为binary(二进制)，若以普通方式搜寻，只有2种结果:  
1.若有符合的地方：显示Binary file 二进制文件名 matches  
2.若没有符合的地方：什么都没有显示。

若TYPE为without-match，遇到此参数，  
grep会认为此二进制档案没有包含任何搜寻样式，与-I&nbsp;参数相同。

若TPYE为text, grep会将此二进制文件视为text档案，与-a&nbsp;参数相同。

**Warning** : --binary-files=text 若输出为终端机，可能会产生一些不必要的输出。

7.&nbsp;-c, --count  
不显示符合样式行，只显示符合的总行数。  
若再加上-v,--invert-match，参数显示不符合的总行数。

8.&nbsp;-d ACTION, --directories=ACTION  
若输入的档案是一个资料夹，使用ACTION去处理这个资料夹。  
预设ACTION是read(读取)，也就是说此资料夹会被视为一般的档案；  
若ACTION是skip(略过)，资料夹会被grep略过：  
若ACTION是recurse(递归)，grep会去读取资料夹下所有的档案，  
此相当于-r 参数。

9.&nbsp;&nbsp;-E, --extended-regexp  
采用规则表示式去解释样式。

10.&nbsp;&nbsp;-e PATTERN, --regexp=PATTERN  
把样式做为一个partern，通常用在避免partern用-开始。

11.&nbsp;&nbsp;-f FILE, --file=FILE  
事先将要搜寻的样式写入到一个档案，一行一个样式。  
然后采用档案搜寻。  
空的档案表示没有要搜寻的样式，因此也就不会有任何符合。

ex: (newfile为搜寻样式文件)  
$ **grep&nbsp;-f&nbsp;newfile file**

12.&nbsp;&nbsp;-G, --basic-regexp  
将样式视为基本的规则表示式解释。(此为预设)

13.&nbsp;&nbsp;-H, --with-filename  
在每个符合样式行前加上符合的文件名称，若有路径会显示路径。

ex: (在file与testfile中搜寻panda样式)  
$ **grep&nbsp;-H&nbsp;panda file ./testfile**  
file:panda  
./testfile:panda  
$

14.&nbsp;&nbsp;-h, --no-filename  
与-H参数相类似，但在输出时不显示路径。

15.&nbsp;&nbsp;--help  
产生简短的help讯息。

16.&nbsp;&nbsp;-I  
grep会强制认为此二进制档案没有包含任何搜寻样式，  
与--binary-files=without-match参数相同。

ex:&nbsp;&nbsp;$&nbsp; **grep&nbsp;-I&nbsp;panda mv**

17.&nbsp;&nbsp;-i, --ignore-case  
忽略大小写，包含要搜寻的样式及被搜寻的档案。

ex:&nbsp;&nbsp;$&nbsp; **grep&nbsp;-i&nbsp;panda mv**

18.&nbsp;&nbsp;-L, --files-without-match  
不显示平常一般的输出结果，反而显示出没有符合的文件名称。

19.&nbsp;&nbsp;-l, --files-with-matches  
不显示平常一般的输出结果，只显示符合的文件名称。

20.&nbsp;&nbsp;--mmap  
如果可能，使用mmap系统呼叫去读取输入，而不是预设的read系统呼叫。  
在某些状况，--mmap 能产生较好的效能。 然而，--mmap  
如果运作中档案缩短，或I/O 错误发生时，  
可能造成未定义的行为(包含core dump)，。

21.&nbsp;&nbsp;-n, --line-number  
在显示行前，标上行号。

ex:&nbsp;&nbsp;$&nbsp; **grep&nbsp;-n&nbsp;panda file**  
显示结果相似于下:  
行号:符合行的内容

22.&nbsp;&nbsp;-q, --quiet, --silent  
不显示任何的一般输出。请参阅-s或--no-messages

23.&nbsp;&nbsp;-r, --recursive  
递归地，读取每个资料夹下的所有档案，此相当于 -d recsuse 参数。

24.&nbsp;&nbsp;-s, --no-messages  
不显示关于不存在或无法读取的错误讯息。

小注: 不像GNU grep，传统的grep不符合POSIX.2协议，  
因为缺乏-q参数，且他的-s 参数表现像GNU grep的 -q 参数。  
Shell Script倾向将传统的grep移植，避开-q及-s参数，  
且将输出限制到/dev/null。

POSIX: 定义UNIX及UNIX-like系统需要提供的功能。

25.&nbsp;&nbsp;-V, --version  
显示出grep的版本号到标准错误。  
当您在回报有关grep的bugs时，grep版本号是必须要包含在内的。

26.&nbsp;&nbsp;-v, --invert-match  
显示除搜寻样式行之外的全部。

27.&nbsp;&nbsp;-w, --word-regexp  
将搜寻样式视为一个字去搜寻，完全符合该"字"的行才会被列出。

28.&nbsp;&nbsp;-x, --line-regexp  
将搜寻样式视为一行去搜寻，完全符合该"行"的行才会被列出。

来自：[http://shanchao7932297.blog.163.com/blog/static/136362420113634354832/](http://shanchao7932297.blog.163.com/blog/static/136362420113634354832/)

