---
layout: post
title: '[Zend]An internal error occurred during: "Selection Job titile".'
date: 2010-08-26 08:04:02.000000000 -07:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Solutions
tags: []
meta:
  _edit_last: '1'
  _wp_old_slug: ''
  views: '7145'
  bot_views: '11'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/solutions/146.html"
---
Using Zend Stdio, there&nbsp;suddenly comes out this error:An internal error occurred during: "Selection Job titile". ...

It is reported came in all kinds of os, including Windows, Linux, Mac, etc.

Eclipse wiki provide a way to solve this as below, but it doesn't work on my computer.

- You may encounter this error message: _Problem occurred: 'Selection Job titile' has encountered a problem._ If so, you need to install [DLTK 1.0.I200807181303](http://download.eclipse.org/technology/dltk/downloads/ "http://download.eclipse.org/technology/dltk/downloads/") (or newer). Unpack the zip into your dropins folder (see [From Zips](http://wiki.eclipse.org/PDT/Installation#From_Zips) above). See also [bug 242947](https://bugs.eclipse.org/bugs/show_bug.cgi?id=242947 "https://bugs.eclipse.org/bugs/show\_bug.cgi?id=242947").
<dl>
<dd>
<ul>
<li>Another variation reported to work: PDT 2.0.0 N20080823 + DLTK Core 0.95.0.v20080716 + DLTK RDS 0.95.0.v20080623</li>
</ul>
</dd>
</dl>

&nbsp;

At last, I found solutions on Zend Forums, some one asked this&nbsp;problems there.

Solution 1:

The files in which you have this error is not at your workspace or you have it on created files at projects in workspace.  
I`m asking you, because now I reproduced it at external files for Zend Studio 7.1  
If I import the files at some workspace project - no error is appear anymore.

Recommended! Refresh your workspace several times, then&nbsp;no error appears.&nbsp;

Solution 2:

Go to preferences -\> PHP -\> Editor -\> Mark Occurrences  
and remove the tick before "Class methods and declarations"  
Click apply and click OK

With this disabled, I can at least continue my work again. Hope this works for more peops.

