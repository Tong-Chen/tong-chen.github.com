---
title: Basic LAMP usages
author: ct
layout: post
categories:
  - Docker
tags:
  - Docker
---


### 记录无法归类的小问题及解决方法

Q:每次打开pdf文件时都会弹出一个内容准备进度”对话框，
提示说正在准备文档以供阅读，请稍候。

A:在Adobe reader安装路径下搜索'accessibility.api'，然后删掉。

Q: Windows下转换的UTF-8文件通常为UTF-8 BOM, 文件的行首存在字符
`<U+FEFF>`，怎么查看和去除？

A: 在vim中执行`:set nobomb` and `:wq` 
或在终端执行 `perl -pi~ -CSD -e 's/^\x{fffe}//' file`
执行`less -a file`可以看有无特殊字符。

Q: vim配置文件位置？
A: /etc/vimrc or ~/.vimrc

Q: 查看端口对应的进程
A: lsof -Pnl +M -i4

Q: R包安装的位置
A: /usr/lib64/R/library



