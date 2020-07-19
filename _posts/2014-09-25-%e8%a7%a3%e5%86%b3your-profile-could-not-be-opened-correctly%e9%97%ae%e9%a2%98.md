---
layout: post
title: 解决Your profile could not be opened correctly问题
date: 2014-09-25 12:40:55.000000000 -07:00
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
  wp_review_bordercolor: "#e7e7e7"
  wp_review_bgcolor2: "#ffffff"
  wp_review_bgcolor1: "#e7e7e7"
  wp_review_fontcolor: "#555555"
  wp_review_color: "#1e73be"
  _layout: inherit
  wp_review_location: bottom
  views: '531'
  _thumbnail_id: '1142'
author:
  login: navins
  email: navins@qq.com
  display_name: navins
  first_name: ''
  last_name: ''
permalink: "/solutions/1151.html"
---
Google Chrome Problem detail:

Your profile could not be opened correctly.

Some features may be unavailable. Please check that the profile exists and you have permission to read and write its contents.

&nbsp;

Solution:

1. If the browser is open, close it down.
2. Open a terminal and run:&nbsp;`mv ~/.config/google-chrome ~/.config/google-chrome-old`
3. Launch google-chrome, you will be asked to choose your search engine, your choice.
4. Close coogle-chrome (yes, click the close button)
5. After closing the browser you will have a new user profile at&nbsp;`~/.config/google-chrome`
6. Then let's copy your profile into the new place by running the next in the terminal.&nbsp;`cp -r ~/.config/google-chrome-old/Default ~/.config/google-chrome/`

&nbsp;

