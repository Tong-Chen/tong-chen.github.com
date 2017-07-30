---
title: 解决Google字体库和公共库加载缓慢问题
author: ct
layout: post
categories:
  - Other
tags:
  - Other
---

打开网页时通常会看到左下角出现`ajax.googleapis.com`, 然后系统就被卡住。

解决方法是使用360网站卫士提供的服务并修改`hosts`文件。

* 打开cmd.exe，运行以下命令：`ping fonts.useso.com`
  或`ping ajax.useso.com`，获得其IP地址`222.73.144.195`。

* 找到系统的`hosts`文件。Windows下在`C:\Windows\System32\drivers\etc`
  目录下，把下面2行写入这个文件。

	222.73.144.195 fonts.googleapis.com
	222.73.144.195 ajax.googleapis.com

参考：<http://bbs.kafan.cn/thread-1747376-1-1.html>
