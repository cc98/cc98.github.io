---
layout: post
title: fstat、stat、lstat Differs
date: 2010-07-24 00:48:35.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Labrary
tags:
- C
- Linux
meta:
  _edit_last: '1'
  _wp_old_slug: ''
  views: '2296'
  bot_views: '5'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/labrary/104.html"
---
stat系统调用系列包括了fstat、stat和lstat，它们都是用来返回“相关文件状态信息”的，三者的不同之处在于设定源文件的方式不同。

**1**

首先隆重介绍的是一个非常重要的”VIP”人物，他是fstat, stat和lstat三者都要用到的一个结构体类型，名字叫做struct stat。可以说，没有这个struct stat的支持，上述三个系统调用将寸步难行。

这个struct stat结构体在不同的UNIX/Linux系统中的定义是有小的区别的，但你完全不用担心，这并不会影响我们的使用。

在struct stat结构体中我们常用的且各个平台都一定有的域是：

**st\_mode 文件权限和文件类型信息&nbsp;（记住这个黑体橘红色）**

st\_ino&nbsp;&nbsp; 与该文件关联的inode

st\_dev&nbsp;&nbsp; 保存文件的设备

st\_uid&nbsp;&nbsp; 文件属主的UID号

st\_gid&nbsp;&nbsp; 文件属主的GID号

st\_atime 文件上一次被访问的时间

st\_ctime 文件的权限、属主、组或内容上一次被修改的时间

st\_mtime 文件的内容上一次被修改的时间。（和st\_ctime的不同之处显而易见）

st\_nlink&nbsp; 该文件上硬连接的个数

我分别提取了solaris（UNIX）和fedora（Linux）的struct stat结构体的原始定义：大家可以自己比对一下便可以发现两者确实有所不同，但主要的域是完全相同的。

<!--more-->

**solaris的struct stat定义：**

struct stat {  
dev\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_dev;  
ino\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_ino;  
mode\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_mode;  
nlink\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_nlink;  
uid\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_uid;  
gid\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_gid;  
dev\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_rdev;  
off\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_size;  
timestruc\_t&nbsp;&nbsp;&nbsp;&nbsp; st\_atim;  
timestruc\_t&nbsp;&nbsp;&nbsp;&nbsp; st\_mtim;  
timestruc\_t&nbsp;&nbsp;&nbsp;&nbsp; st\_ctim;  
blksize\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_blksize;  
blkcnt\_t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_blocks;  
char&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; st\_fstype[\_ST\_FSTYPSZ];  
};

**fedora的struct stat定义：**

struct stat  
{  
\_\_dev\_t st\_dev;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Device.&nbsp; \*/  
unsigned short int \_\_pad1;  
\_\_ino\_t st\_ino;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* File serial number.&nbsp; \*/  
\_\_mode\_t st\_mode;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* File mode.&nbsp; \*/  
\_\_nlink\_t st\_nlink;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Link count.&nbsp; \*/  
\_\_uid\_t st\_uid;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* User ID of the file’s owner. \*/  
\_\_gid\_t st\_gid;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Group ID of the file’s group.\*/  
\_\_dev\_t st\_rdev;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Device number, if device.&nbsp; \*/  
unsigned short int \_\_pad2;  
\_\_off\_t st\_size;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Size of file, in bytes.&nbsp; \*/  
\_\_blksize\_t st\_blksize;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Optimal block size for I/O.&nbsp; \*/  
\_\_blkcnt\_t st\_blocks;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Number 512-byte blocks allocated. \*/  
struct timespec st\_atim;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Time of last access.&nbsp; \*/  
struct timespec st\_mtim;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Time of last modification.&nbsp; \*/  
struct timespec st\_ctim;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /\* Time of last status change.&nbsp; \*/  
unsigned long int \_\_unused4;  
unsigned long int \_\_unused5;  
};

**2**

大家一定注意到了，在上面列举域的时候，我在st\_mode处使用了 **黑体橘红色** 标识，原因在于这个域不像其他域那么容易使用，其他的域的值显而易见，而st\_mode域是需要一些宏予以配合才能使用的。其实，通俗说，这些宏就是一些特定位置为1的二进制数的外号，我们使用它们和st\_mode进行”&”操作，从而就可以得到某些特定的信息。

**文件类型标志包括：**

S\_IFBLK：文件是一个特殊的块设备

S\_IFDIR：文件是一个目录

S\_IFCHR：文件是一个特殊的字符设备

S\_IFIFO：文件是一个FIFO设备

S\_IFREG：文件是一个普通文件（REG即使regular啦）

S\_IFLNK：文件是一个符号链接

**其他模式标志包括：**

S\_ISUID：文件设置了SUID位

S\_ISGID：文件设置了SGID位

S\_ISVTX：文件设置了sticky位

**用于解释st\_mode标志的掩码包括：**

S\_IFMT：文件类型

S\_IRWXU：属主的读/写/执行权限，可以分成S\_IXUSR, S\_IRUSR, S\_IWUSR

S\_IRWXG：属组的读/写/执行权限，可以分成S\_IXGRP, S\_IRGRP, S\_IWGRP

S\_IRWXO：其他用户的读/写/执行权限，可以分为S\_IXOTH, S\_IROTH, S\_IWOTH

**还有一些用于帮助确定文件类型的宏定义，这些和上面的宏不一样，这些是带有参数的宏，类似与函数的使用方法：**

S\_ISBLK：测试是否是特殊的块设备文件

S\_ISCHR：测试是否是特殊的字符设备文件

S\_ISDIR：测试是否是目录（我估计find . -type d的源代码实现中就用到了这个宏）

S\_ISFIFO：测试是否是FIFO设备

S\_ISREG：测试是否是普通文件

S\_ISLNK：测试是否是符号链接

S\_ISSOCK：测试是否是socket

**3**

我们已经学习完了struct stat和各种st\_mode相关宏，现在就可以拿它们和stat系统调用相互配合工作了！

int fstat(int filedes, struct stat \*buf);

int stat(const char \*path, struct stat \*buf);

int lstat(const char \*path, struct stat \*buf);

聪明人一眼就能看出来fstat的第一个参数是和另外两个不一样的，对！fstat区别于另外两个系统调用的地方在于，fstat系统调用接受的是 一个“文件描述符”，而另外两个则直接接受“文件全路径”。文件描述符是需要我们用open系统调用后才能得到的，而文件全路经直接写就可以了。

stat 和lstat的区别：当文件是一个符号链接时，lstat返回的是该符号链接本身的信息；而stat返回的是该链接指向的文件的信息。（似乎有些晕吧，这 样记，lstat比stat多了一个l，因此它是有本事处理符号链接文件的，因此当遇到符号链接文件时，lstat当然不会放过。而 stat系统调用没有这个本事，它只能对符号链接文件睁一只眼闭一只眼，直接去处理链接所指文件喽）

