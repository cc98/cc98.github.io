---
layout: post
title: python初学教程（转载）
date: 2011-07-06 11:08:42.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Skills
tags: []
meta:
  _oembed_1348d506919bbaf3e23e619062ebd731: "{{unknown}}"
  _oembed_5f2827193e5d84350ac8da3516d5c0a6: "{{unknown}}"
  _oembed_172224227a05d5c976a58732048ec904: "{{unknown}}"
  _oembed_a39706612b171a33b4171e52fe638117: "{{unknown}}"
  _oembed_fa511b64b1635e20cc617f10ce2ba8f8: "{{unknown}}"
  _edit_last: '1'
  _oembed_7432773ef23c601c0c28ce8b1bf2a37d: "{{unknown}}"
  views: '1642'
  _oembed_04beed84030f75959b62ee0be27e2e99: "{{unknown}}"
  _oembed_6d48983c237edfd1a968767fc86f3b75: "{{unknown}}"
  bot_views: '8'
  _oembed_b3f56340d174dfdd08c70404bdb38ab9: "{{unknown}}"
  _oembed_e071cc8ef6c5a1e896d0aa03f7aefa74: "{{unknown}}"
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/skills/320.html"
---
Lesson 1&nbsp; **准备好学习Python的环境**  
下载的地址是：  
www.python.org  
为了大家的方便，我在校内作了copy：  
http://10.1.204.2/tool/compiler&IDE/Python-2.3.2-1.exe  
linux版本的我就不说了，因为如果你能够使用linux并安装好说明你可以一切自己搞定的。  
运行环境可以是linux或者是windows：  
1、linux  
redhat的linux安装上去之后一定会有python的（必须的组件），在命令行中输入python回车。这样就可以进入一个  
\>\>\>的提示符  
2、windows  
安装好了python之后，在开始菜单里面找到Python2.3-\>IDLE，运行也会进入一个有  
\>\>\>提示符的窗口  
开始尝试Python  
1、输入：  
welcome = "Hello!"  
回车  
然后又回到了\>\>\>  
2、输入：  
print welcome  
回车  
然后就可以看到你自己输入的问候了。  
Lesson 2&nbsp; **搞定环境之后的前行**  
Python有一个交互式的命令行，大家已经看到了吧。所以可以比较方便的学习和尝试，不用“新建－存档－编译－调试”，非常适合快速的尝试。  
一开始从变量开始（其实说变量，更准确的是对象，Python中什么都可以理解为对象）。  
**变量**  
welcome = "hello!"  
welcome就是变量名，字符串就是变量的类型，hello!就是变量的内容，""表示这个变量是字符串，""中间的是字符串的内容。  
熟悉其他语言的人，特别是编译类型的语言，觉得没有变量的声明很奇怪。在python中用赋值来表示我要这么一个变量，即使你不知道要放什么内容，只是要先弄一个地方来放你的东西，也要这么写：  
store = ""  
不过这个还是说明了store是字符串，因为""的缘故。  
**have a try**

**<!--more-->**

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37614#)

tmp\_storage = ""  
welcome = "hello!"  
tmp\_storage = welcome  
print tmp\_storage

你会发现同样的问候出现了。  
**字符串**  
字符串是用""标记的，但是用''也可以（不要说你看不出一个是双引号，一个是单引号），两者之间是有一丁点区别，不过你可以不用理会。其实是差不多的。字符串有很多自己的操作，最常用的是这样的：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37614#)

welcome = "hello"  
you = "world!"  
print welcome+you

运行之后就会发现她输出了helloworld!。  
**更多变量**  
变量还有几种类型。  
数  
字符串  
列表  
字典  
文件  
勿庸置疑，这些都是非常非常常用的。对于数字就不用讲了那就是：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37614#)

radius = 10  
pi = 3.14  
area = pi\*radius\*\*2  
print "the area is", area

下次讲列表和字典  
Lesson 3&nbsp; **Python中的数学结构**  
数学中你学什么东西最多遍？我想根据我的一点浅薄经验（ ![]({{ site.baseurl }}/assets/images/silence.gif)虽然我是数学系的），学得最多的是集合，无论什么数学书都从集合开始讲起。然后讲函数呢，又必然把映射再讲一遍。可以说，集合和映射是数学中最基本的结构了。  
Python对于数据结构非常明智的内置了两个，回想我写C的程序，往往是一开始就是用struct拼一个链表出来（ ![]({{ site.baseurl }}/assets/images/sweatingbullets.gif)重复劳动）。Python中提供了列表（list）和字典（dict）两种数据结构。他们分别对应的原型是集合和映射。这个你应该明白了，只是表示方法有一点不一样而已。  
**列表**  
列表的英文名是list嘛，所以我取一个名字叫

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37623#)

my\_list = []  
这个就产生了一个空的列表。然后给它赋值  
my\_list = [1,2]  
print my\_list  
my\_list.append(3)  
print my\_list

非常容易明白的。append前面加了一个点，这个表示append是my\_list方法。我实在不想又去给你解释什么是对象，什么是成员方法，然后扯出一大段出来。  
list是可以索引的：  
print my\_list[1]  
不过你或许会不明白为什么是2，而不是显示的是1。因为索引从0开始，要输出第一个元素：  
print my\_list[0]  
**字典**

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37623#)

contact = {}

这个产生了一个空字典，contact。然后往里面填充内容：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37623#)

contact={}  
contact["name"]="taowen"  
contact["phone"]=68942443

name就是你查字典的时候要查找的单词，taowen就是查到的内容。不过你现在不是查，而是在写这个字典。同理添加了phone这个词条。  
现在添加好了，看看contact的内容，怎么查看？自己想办法吧。。。  
如果你悟性够，就会发现python很多操作是通用的，既然能够print 1, print "", print my\_list，那么其他数据类型的变量就没有理由不能用了。  
**结合列表和字典**

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37623#)

contact\_list=[]  
contact1={}  
contact1['name']='taowen'  
contact1['phone']=68942443  
contact\_list.append(contact1)  
contact2={}  
contact2['name']='god'  
contact2['phone']=44448888  
contact\_list.append(contact2)

呵呵，够复杂的吧。你可以想出我为什么要用两个contact字典呢？。。。  
Lesson 4&nbsp; **用不同的方式来操作Python**  
到现在为止，我们用的都是交互式的命令行来操作的，的却是很方便，是吧？不过，复杂一些的情况就不那么好使了，来换一种方式来操作Python  
在IDLE中点击File-\>New Window，出现一个新窗口（对于linux下，你要用vim或者emacs或者pico把文本的源文件写好了）。为了方便，先点击File-\>Save，填入my\_try.py。这样能够让编辑器知道在编辑python的源文件，会把你输入的代码进行一点上色的处理。  
填入下面的代码：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37626#)

i = 5  
n = 0  
while i\>0:  
n = n + i  
i = i - 1  
print n

你会发现输入:之后，自动会给缩进。而且也没有在python中发现和C/C++中类似的{}标记也没有pascal中的begin end;，其实缩进就是python中表示一段代码的从属关系的标记方法。表示n=n+1和i=i-1这两句都是while的。程序的运行逻辑应该不用解释了吧。就是运行5+4+3+2+1的结果。  
运行代码  
按F5，可能提示你没有存盘，照着办就是了。  
发挥你的能力，计算从1到10的所有偶数的和（提示，可能没有你想象的那么智能）。  
Lesson 5&nbsp; **Python中的输入与判断**  
健全的程序大凡都需要输入的功能，所以要学习一下简单的输入：  
输入要使用的是raw\_input或者input函数，区别是raw\_input直接把你的输入作为字符串返回，而input则在raw\_input的基础上把字符串转换为数字返回（如果你输入$@#$$怎么办？自己试试看）。我们就利用这两个输入函数来作一些有趣的事情。

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37636#)

your\_name = raw\_input("please input your name:")  
hint = "welcome! %s" % your\_name  
print hint

不简单吧，还有%呢。%s表示在这个位置插入一个字符串，%表示把后面提供的参数“推”入前面的字符串中，所以推的结果是把%s推出去了，把your\_name给填入那个地方了。printf知道吧，C中的printf就是一样的嘛。

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37636#)

inputed\_num = 0  
while 1:  
inputed\_num = input("input a number between 1 and 10n")  
if inputed\_num \>= 10:  
pass  
elif inputed\_num \< 1:  
pass  
else:  
break  
print "hehe, don't follow, won't out"

pass就是pass了，过了嘛，什么都不干了。break就是跳出这个while 1（无穷循环，1总是真的，while总是执行）。n是换行，不会全部忘光了吧。  
Lesson 6&nbsp; **Python余兴节目**

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37700#)

from Tkinter import \*  
root = Tk()  
w = Label(root, text="Hello, world!")  
w.pack()  
root.mainloop()

呵呵，一次太超前了一点，不过也不是解释不清楚。我干脆也不解释了吧。给大家增进一点兴趣。  
－－－－－－－－－  
还是解释一下  
fromt Tkinter import \*  
是引入一个模块，这个模块用来创建GUI（Graphic User Interface）窗口  
Tk()创建了一个主窗口  
Label()创建一个标签  
Label的第一个参数是root表明Label是在这个主窗口中的。  
w.pack()是指用缺省的方式把Label放置在主窗口中  
root.mainloop()开始了一个循环，是等待你的输入的循环。  
Lesson 7&nbsp; **Python基本语法要素齐动员**  
现在的目的是尽量想出一个用的东西仅限于内置的变量类型和语句的一个综合的例子，我想还是那个联系人表的例子吧

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37736#)

################  
#呵呵，还忘记了讲注释  
#第一个算是完整的程序  
################  
contact = {}  
contact\_list = []  
while 1:  
contact['name'] = raw\_input("please input name: ")  
contact['phone'] = raw\_input("please input phone number: ")  
contact\_list.append(contact.copy())  
go\_on = raw\_input("continue?n")  
if go\_on == "yes":  
pass  
elif go\_on == "no":  
break  
else:  
print "you didn't say non"  
i = 1  
for contact in contact\_list:  
print "%d: name=%s" % (i, contact['name'])  
print "%d: phone=%s" % (i, contact['phone'])  
i = i + 1

首先是回忆一下字符串  
字符串既能够用""也能够用''。然后是很有特色的%操作，起到格式化字符串的作用，前面仅仅在字符串中有一个%s，现在有%d和%s两个，分别代表插入十进制数值和字符串于%x标记的位置处。  
然后是列表  
列表是顺序的序列，用append在后面附加，也能构用索引值索引。所以我们完全可以用一个变量保存len(contact\_list)得到的长度，然后一个个的遍历，不过这里展示了另外一种非常方便的方法。而且值得注意的是append()中的参数，我使用了contact.copy()，你可以尝试着把copy()给去掉，观察结果你就知道了所谓的append是怎么干的了，特别是你对指针之类的东西很有感觉的话（但是在Python中是没有指针这个概念的）  
再来看看字典  
字典是键（key）和值（value）的对应组合成的无序的序列。所以你存的时候要指明键（name或者phone），而且取的时候也是一样的。  
接下来是判断  
if是很好用的，==表示判断两个是否相等，=表示把右边的赋给左边的。而且可以直接判断字符串是否相等，这个太方便了，如果你曾经用过strcpy()的话，就知道了。elif是表示else if的意思，如果if不满足就判断elif的条件是否满足，最后是到else中去。  
循环是个主体  
while和for都是循环。不过这里while就没什么说的了，又是很经典的while 1，死循环，然后必须在里面用break来跳出。for和C中的for是不一样的，for in才是一个完整的语句，指的是从一个能够逐一取值的序列中（比如list），一个一个的取出值赋给for后面指定的变量中，直到取空，循环结束。其实回想一般用C中的for的经历，也大体如此。而且你还可以用for i in range(1,100)来指定一个范围从多少到多少。可以说for in充分体现了python的体贴周到，用起来很直观，不会绕弯。  
接下来就是运行了，大家慢慢调试吧。下次可能是讲异常处理，因为我觉得在深入到使用各种高级的要素之前，先要学会怎么去处理异常。最常见的异常应该是input()，然后你给出的输入是一个无法转换为数字的字符串了，那么我们就要来处理它。  
Lesson 8&nbsp; **Python中的错误检测**  
写程序什么最重要？完成功能最重要。但是程序中难免要有用户的输入，对于这些写的时候未可预知的因素中间可能出现的错误，一般称作异常。对于异常情况的处理，不同语言有不同的做法，比如检查函数的返回值之类的，但是那种办法会把代码弄成一团浆糊。Python在这个方面是比较先进的，我们从一个例子来看看：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37828#)

print input()

呵呵，看不同吧。其实input是输入，print是输出。也就是把输入的东西立即输出。但是这个和

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37828#)

print raw\_input()

有什么不同呢？  
不同的地方是，input()会在raw\_input()接收了“字符串”的输入之后进行一些处理，比如你是输入1+2，然后输出的就是3了，而raw\_input就是原原本本的1+2的输出了。用代码表示就是

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37828#)

eval(raw\_input())

eval是求表达式的值，任何一个简单的python表达式，就像1+2这样的作为字符串送入，就能把值从eval处理之后取出来。  
现在你实验一下"sdfsdf”之后，你会发现提示你

引用:

Traceback (most recent call last):  
File "\<pyshell#4\>", line 1, in -toplevel-  
input()  
File "\<string\>", line 0, in -toplevel-  
NameError: name 'sdfsdf' is not defined

如果输入其他稀奇古怪的字符串还可能有其他的出错提示，我们现在要做的就是捕捉这种由用户输入引起的错误。这么来作：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37828#)

try:  
print input()  
except:  
print 'there is an error in your input'

这下你无论怎么输入都不会有什么其他的提示了，就是自己设定的print语句作为提示。现在把try except的组合去掉，回到print input()你再尝试一下：  
1/0  
这个显然是一个错误，被零除的错误。那么专门来捕捉一下这个错误：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37828#)

try:  
print input()  
except ZeroDivisionError:  
print 'can not be divided by zero'

这下你能够捕捉到被零除的错误了。然后你再尝试其他的输入，可能错误就没有被捕捉了。所以再补上：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37828#)

try:  
print input()  
except ZeroDivisionError:  
print 'can not be divided by zero'  
except:  
print 'there is an error in your input'

注意，捕捉所有错误的except必须放在所有的except的最后一位。明白了？OK  
还有更多的能够捕捉的错误，自己查手册吧（暂时看不了手册没关系，慢慢来嘛）。以后还能够自己raise（引发）异常呢。不过那都是比较高级的应用了，对于出错处理从一开始就有这个印象，并牢记在心中对于以后写大一些的软件很有好处。  
Lesson 9&nbsp; **走向模块化的第一步**  
大规模的程序设计需要你把一个大的程序拆分成n个模块。然后把模块进行组合，交互成为一个完整的程序。你不可能像现在这样，从顶写到尾。。。  
那么我们从函数开始。

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37872#)

def square(x):  
return x\*\*2  
print square(5)

简单吧，这个是我看过的函数定义中最简洁的。def表示这个开始定义一个函数，x是参数，参数是不需要类型的，因为python是不需要明确指出类型的。return是返回值，返回的值插入到调用函数的地方。再复杂一些

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37872#)

def multiply(a, b):  
return a\*b  
print multiply(1,2)

这是两个参数的函数。那么返回两个值呢？

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37872#)

def swap(a, b):  
return (b,a)  
print swap(1,2)

呵呵，其实这里返回的并不是两个值，而是一个值。怎么说呢。(b, a)就是一个东西，是一个元组（turple），你可以用这样的方式成生一个元组，并使用它。元组是基本的变量类型：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37872#)

my\_turple = (1, 2, 3)  
my\_list = []  
for i in my\_turple:  
my\_list.append(i)  
print my\_list

其实元组和列表非常像，但是列表的长度是可以变化的，而且成员是可以改变的。但是元组是什么都不能变的，是只读的。  
对于高级一点的话题：传递进来的参数是否可以被修改，这个问题取决于你传递了什么近来。如果是数字或者字符串，是不能够改变的，但是如果是这样的：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37872#)

def test\_func(list\_be\_passed):  
list\_be\_passed[0] = 'towin'  
my\_list = ['taowen']  
print my\_list  
test\_func(my\_list)  
print my\_list

就能够改变传递近来的参数了，所以处理的时候要小心，必要的时候copy一下再传递。  
函数简单吧，但是很好用的。想起C中的函数那么那么多麻烦，真是感慨万千啊。下面是应该讲GUI编程呢，还是面向对象呢？思考一下  
Lesson 10&nbsp; **Python的文件操作**  
文件操作....是一个语言和外界联系的主要方法....现在以txt为例简单的讲一下...  
首先是建立关联...假设在存在以下文件 c:a.txt

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37902#)

This is line #1  
This is line #2  
This is line #3  
END

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37902#)

\>\>\> xxx = file('c:\a.txt', 'r')

关键字的第一部分，是文件路径及名称。注意这里面，路径需要用\  
第二部分，是对文件的模式或者叫权限，一般有以下3种 "r" (read)， "w" (write)和 "a"(append).  
之后，就可以利用  
xxx\_content = infile.read()  
xxx\_content = infile.readlines()  
来读取文件内容了

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37902#)

\>\>\> xxx = file('c:\a.txt', 'r')  
\>\>\> xxx\_content = xxx.read()  
\>\>\> print xxx\_content  
This is line #1  
This is line #2  
This is line #3  
END  
\>\>\> xxx.close()  
\>\>\>  
\>\>\> infile = file('c:\a.txt', 'r')  
\>\>\> xxx = file('c:\a.txt', 'r')  
\>\>\> for xxx\_line in xxx.readlines():  
print 'Line:', xxx\_line  
Line: This is line #1  
Line: This is line #2  
Line: This is line #3  
Line: END  
\>\>\> xxx.close()  
\>\>\>

然后是文件的写入

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37902#)

\>\>\> xxx=file('c:\test.txt','w')  
\>\>\> xxx.write('billrice')  
\>\>\> xxx.write('testtest')  
\>\>\> xxx.write('entern')  
\>\>\> xxx.writelines(['billrice','ricerice'])  
\>\>\> xxx.close()  
\>\>\>  
\>\>\> xxx=file('c:\test.txt','r')  
\>\>\> content=xxx.read()  
\>\>\> print content  
billricetesttestenter  
billricericerice  
\>\>\>

需要注意的是...在xxx.close()之前，c盘下面只有一个空空的test.txt，xxx.close()的作用相当于最后的存盘。  
Lesson 11&nbsp; **走向模块化的第二步**  
函数上面还能是什么呢？内嵌函数^\_^，其实python是支持的。不过用起来会让你吐血的，LGB名称查找规则。。。（寒）。python是面向对象的，对于面向对象的支持挺好玩的。

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37947#)

class person:  
def \_\_init\_\_(self):  
self.name = 'taowen'  
self.id = 20022479  
def say\_id(self):  
print "%s's id is %d" % (self.name, self.id)  
me = person()  
me.say\_id()

比较复杂了吧。如果不熟悉面向对象的概念的，可能会觉得晕。我来解释一下。所谓面向对象是把数据和操作数据的函数放到同一个类中去，然后用类来创建对象，操作的时候能够比较方便（很不精确的说法，任何一个OO高手都可以把我骂得屁都不是 ![]({{ site.baseurl }}/assets/images/sweatingbullets.gif)）。  
类  
类是class关键来定义的。class person:就是说定义一个类，名字叫person。  
对象  
对象是用类来产生的。所以me就是对象，产生的办法就是像调用函数一样，person()，而且()中是能够放参数的，什么时候要参数，看下面的“初始化函数“  
初始化函数  
类可以有自己的初始化函数，每次类被创建的时候（调用person()这样的语句的时候），都会调用它。这个在C++中的名称是构造函数。\_\_init\_\_是必须的名字，你不能用其他名字来当初始化函数。但是你可以没有初始化函数。  
类的数据  
类的数据是所有类产生的对象共享的数据。这里没有用到类的数据，要写的话是这样：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=37947#)

class person:  
school = 'bit'  
def \_\_init\_\_(self):  
self.name = 'taowen'  
self.id = 20022479  
def say\_id(self):  
print "%s's id is %d" % (self.name, self.id)  
me = person()  
me.say\_id()  
print me.school

对象的数据  
对象的数据是用  
self.变量名 = 。。。  
来生成的。这里self.name就是对象的数据。对象的数据和类的数据不同，因为对象之间的数据是互不共享的，而类的数据是被所有由类生成的对象共享的。  
对象的函数（类的函数）  
两个没有区别，是类的就是对象的。其实就是类的（我说的是底层实现，不过不用管，如果关心怎么实现的，等我写Hacking OO吧，还没影呢）。say\_id就是对象的函数，你能够调用它。每个对象的函数都需要一个self参数，表示[color]这个对象[/color]。  
为什么使用面向对象编程  
除去让人觉得你比较专业外，当然由切实的好处。比较浅显的是你能够表达一定的层次关系，类与类之间能够有包含和继承的关系（当然你现在还不会。。。）。而且对象能够把数据和操作数据的函数放在一起，能够比较清晰。虽然有所谓的数据隐藏的概念，但是在python中其实就是一个不要直接调用对象中的数据的约定，而要用一个函数作为中转。其实不懂面向对象很正常，其实有的时候就是要在用的中间感悟的。什么时候把用函数编程用牛了，用出个道道来了，说不定你已经感觉到了什么是面向对象编程。另外：所谓什么OO，都是一些认为规定，不用语法支持，只要心中有这个想法（什么想法？自己悟啊 ![]({{ site.baseurl }}/assets/images/lol.gif)），就能够写出OO的代码，不管你用的是什么语言，什么语法。  
Lesson 12&nbsp; **python to exe**  
about py2exe  
本文讲述如何将一个python源代码编译成一个exe.....我会的只是最初步最基本的.....实际上那个py2exe似乎有着更强大的功能  
1：下载安装py2exe.....from http://twh@bitunion.org  
2：假设你写好了一个python程序....guess\_number.py.......存在了c:Python23下面  
3：再写一个setup.py....也存在c:Python23下面......内容如下

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=38382#)

# setup.py  
from distutils.core import setup  
import py2exe  
setup(name="guess\_number",  
scripts=["guess\_number.py"],  
)

其中name和scripts是需要你到时候具体修改的....  
4：找到windows的dos模式（命令提示符）.....或者自己做个快捷方式也可以....  
C:Python23\>  
C:Python23\>python setup.py py2exe  
构造就开始了....  
几秒钟以后....  
在你的C:Python23就会出现两个文件夹build和dist，前面那个里面似乎是源程序（这个我不太清楚）....dist里面的就是编译好的.exe了.....ok....  
btw....等国两天有了实际应用再来翻译这些东西  
Specifying additional files  
Some applications need additional files at runtime, this maybe configuration files, fonts, bitmaps, whatever.  
py2exe can copy these files into subdirectories of distmyscript if they are specified in the setup script with the data\_files option. data\_files should contain a sequence of (target-dir, files) tuples, where files is a sequence of files to be copied.  
Here's an example:

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=38382#)

# setup.py  
from distutils.core import setup  
import glob  
import py2exe  
setup(name="myscript",  
scripts=["myscript.py"],  
data\_files=[("bitmaps",  
["bm/large.gif", "bm/small.gif"]),  
("fonts",  
glob.glob("fonts\*.fnt"))],  
)

This would create a subdirectory bitmaps in distmyscript, containing the two bitmaps, and a subdirectory fonts, containing all the \*.fnt files.  
 ![]({{ site.baseurl }}/assets/images/icon12.gif)  
相关资料出处....  
http://starship.python.net/crew/theller/py2exe/  
Lesson 13&nbsp; **写一个简单的界面很容易**  
图形界面是非常有吸引力的东西。但是制作出来似乎不是那么容易，这个观点对于用C来笨拙写windows的窗口程序来说，是比较正确的。微软公司出品的windows是一个图形界面的操作系统，这个和dos或者linux这些不一样，他们一开始出来是针对字符界面的，然后再在上面加上一些库来提供图形的功能。windows则不同，它是包含在自己的最原始的功能之中，而这些图形功能的提供是在user32.dll这样的system目录下的dll文件中以函数导出的形式提供的，但是要使用这些东西必须使用c语言的函数接口，而且编写麻烦。有一个很大的wndproc中要填入所有的事件处理代码，非常丑陋。而作为脚本语言，所应该有的简洁性，python对这个进行了封装。但是事情不是如你所想象。中间过程非常复杂，而且python用的也不是自己的库，还是tcl的一个tk的库再封装了一次。虽然经过层层封装，裹得非常严实，但是除了影响其在比较高性能的图形场合下的应用之外，并没有带来太大的麻烦。你能够用很少的代码，来完成其他语言+库要很大行代码才能表达的图形样式，虽然非常简陋，不过足够使用。而且python除了自己原包装带的这个tkinter库之外，还有其他的第三方的选择，比较丰富，而且也有能够胜任各种应用的选择。甚至，还有opengl和directx的库的封装库，能够用来编写2d和3d的游戏，这个非常的诱人哦 ![]({{ site.baseurl }}/assets/images/03.gif)。但是我不会， ![]({{ site.baseurl }}/assets/images/sad.gif)  
图形界面的奥秘其实并不深奥。我相信很多人学习windows编程都是从写一个窗口开始的，而且都是从尝试理解那个消息和事件驱动的模型入手的。大体的过程是这样的，窗口就是用象素画出来的。你可以把一个窗口想象成一个窗口，也可以把窗口看成一堆象素的集合。就像有人说看女色不过是皮肉色相一样。而且窗口中的按钮，编辑矿，各种图标，无论是什么看起来像一个”物体“的东西，其实本质上都是有应用程序或者是库或者是操作系统调用显卡的驱动，通过显卡的功能在屏幕上绘画一些点出来。而所谓的”物体“有很多称法，在windows中一般成为控件（control）。  
而对于图形界面的操控一般是通过鼠标和键盘来完成的。鼠标在屏幕上有一个自己的形象，那就是一个箭头（当然你也可以调整这个图形为其他好玩的东西，it is your freedom）。而键盘呢则一般表示为一个虚线的框，表示这个是键盘的”焦点“所在的地方。或者是编辑框中闪动的竖杠。这两点中有一个共同点，就是都有一个位置来确定要操作的对象。你点下鼠标的时候，你操作的就是鼠标的箭头尖端指向的那个空间，而键盘按下也是在其焦点所在的控件那儿放声。发生的是什么呢？发生的过程从硬件层面到软件层面之后，最终是被操作系统接收。操作系统能够知道你是点击的是鼠标还是键盘，在什么一个地方点下的，而且按下的是左键还是右键。操作系统还知道当前窗口各处摆放的位置。综合各路的信息，操作系统就能够知道把这个”事件“作为”消息“发送给哪个窗口来处理。从中应该能够明白什么叫事件，而消息呢则是一个C中的结构体，其中有几个field中间放了有关这个事件的信息，然后就像一封信一样从操作系统投递到了窗口所在的应用程序。然后应用程序有一个事先注册的”窗口过程“，其实就是一个函数，用来接收这封“信”。其实就是接收到传过来的参数。然后再进行一些判断，作出一定的响应。这个就是所谓的事件驱动。在没有冗长的代码，和展示所有细节的情况下，如果你真的以前对这个过程一无所知，肯定会觉得非常茫然。这个一笔带过的叙述其实只是让你有一个感性的认识。其实在python中使用窗口根本不用管诸葛么多。基本上只是把自己要的窗口和控件，给一些位置的参数，一些文字的提示内容的参数就能把窗口摆好，显示出来。然后再通过代码告诉python，当“这个按钮按下的时候执行这个函数”，然后就能让窗口有响应。最后记得给一个退出窗口的办法就一切OK了。其中能省的复杂度基本上都被库给隐藏掉了。付出的代价是慢一些，但是我就不相信你能感觉出来，除非你用的电脑连vcd都看不流畅。所以大可放心的享受这种便利。  
OK，下面来正式的看看怎么在python中创建一个窗口，然后显示出来。

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=53593&highlight=#)

from Tkinter import \*  
root = Tk()  
root.mainloop()

就3行就能够把主窗口显示出来了。root是一个变量名称，其代表了这个主窗口。以后创建控件的时候指定控件创建在什么窗口之中，就要用这个root来表示了。而Tk()是一个Tkinter库之中的函数（其实是类的构造函数，构造了一个对象）。而mainloop则是主窗口的成员函数，也就是表示让这个root工作起来，开始接收鼠标的和键盘的操作。你现在就能够通过鼠标缩放以及关闭这个窗口了。注意到窗口的标题是tk，我们可以进行一些修改  
root= Tk(className='bitunion')  
然后窗口的标题就变成了bitunion了。下面要作的是把这个窗口的内容填充一下，让其有一些东西。先加入一个标签，所谓标签就是一行字。

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=53593&highlight=#)

from Tkinter import \*  
root = Tk(className='bitunion')  
label = Label(root)  
label['text'] = 'be on your own'  
label.pack()  
root.mainloop()

我们很惊讶的发现窗口变小了，但是其中多了一行字。变小了是因为窗口中已经放了东西了，python的Tkinter非常智能，能够根据内容自动缩放，而不用和传统的windows程序一样，手工的指定绝对坐标了。对于label，它还是一个变量而已。不过这个变量代表了一个标签，也就是那一行字。而这个label的创建是用Label，而Label的参数是root表明了这个控件是root主窗口的成员控件，或者说是子窗口。label['text']表示设置这个标签的text属性为'be on your own'，也就是文字内容了。label.pack和root.mainloop一样费解，但是内涵一样深刻。你现在可以简单理解为把label显示出来的功能，因为你把pack去掉，那你就看不到东西了。其实pack是和控件的布局排版有关西的。  
再添加一个按钮就能够有更加丰富的内容了，方法是很类似的。看着吧：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=53593&highlight=#)

from Tkinter import \*  
root = Tk(className='bitunion')  
label = Label(root)  
label['text'] = 'be on your own'  
label.pack()  
button = Button(root)  
button['text'] = 'change it'  
button.pack()  
root.mainloop()

只不过把button替换了label而Button替换了Label。注意一下Button和Label这些都是Tkinter这些库提供的，而button和Button这样大小写之间的差别仅仅是巧合，你能够随便的给变量取名字，但是Button和Label这些则是需要记住的东西，写代码的时候要经常用到的名字。但是点击按钮你会比较失望，因为并没有什么反应。不过也是当然的事情，你并没有告诉计算机对于这样一个按钮的点击操作需要作出一个什么样的反应来反馈给用户。而这个指定作出什么反应的工作只需要一个行，但是作出具体什么样反应的描述则需要新建一个函数来进行处理。

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=53593&highlight=#)

from Tkinter import \*  
def on\_click():  
label['text'] = 'no way out'  
root = Tk(className='bitunion')  
label = Label(root)  
label['text'] = 'be on your own'  
label.pack()  
button = Button(root)  
button['text'] = 'change it'  
button['command'] = on\_click  
button.pack()  
root.mainloop()

button['command'] = on\_click表示对于button（按钮）的点击属性用on\_click这个函数来处理。而on\_click函数也很简洁，只是把label的文本重新设置一下。这个完成了一个事件消息的处理，如果用C来写，需要比这个长更加不好懂的写法。另外你是否会对on\_click中出现label这个变量比较奇怪呢？明明在on\_click前面没有定义label这个变量啊。如果我在C中这么写程序，编译器一定会告诉我出错的。而python是怎么知道label这个变量存在，然后没有报错的呢？其实python在你写的时候根本就不用知道其是否存在，只是要在运行的时候找得到label就可以了。而运行的前后关系，是通过时间来关联的而不是代码上前后行的关系。这里由于label = Label(root)先于on\_click执行，所以当on\_click执行的时候，label就是一个已经定义的变量。如果没有定义呢？那就报告出错喽。  
最后一个例子：

代码:  
[[复制到剪贴板]](http://www.bitunion.org/viewthread.php?tid=53593&highlight=#)

from Tkinter import \*  
def on\_click():  
label['text'] = text.get()  
root = Tk(className='bitunion')  
label = Label(root)  
label['text'] = 'be on your own'  
label.pack()  
text = StringVar()  
text.set('change to what?')  
entry = Entry(root)  
entry['textvariable'] = text  
entry.pack()  
button = Button(root)  
button['text'] = 'change it'  
button['command'] = on\_click  
button.pack()  
root.mainloop()

这个就比较复杂了。里面有一个StringVar。这个代表一个字符串，但是跟一般字符串不一样。一般的这样'dfsdf'的字符串是不可变的，你只能把变量指定为不同的字符串，但是字符串本身的内容是不可改变的。而StringVar则是可变的字符串。所以了set和get来设置和取得其内容。主要是entry（单行输入框）要求一个这样的属性来设置和接收其输入框的内容。一开始可能不习惯，但是用多了之后会觉得很方便的，因为只要用这个变量text，就能一直得到当前输入框的内容。当你能够完整的把这个例子看懂的时候，你已经入门了。但是离自己写一个有窗口的应用程序还有一定距离。主要是缺少更加丰富的控件和事件响应的处理能力，以及合理排版布局的能力。这个下次再说

&nbsp;

