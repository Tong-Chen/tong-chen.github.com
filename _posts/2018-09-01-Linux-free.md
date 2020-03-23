---
title: 免费Linux系统和生信宝典原创学习教程
author: ct
layout: post
categories:
  - R
tags:
  - 生物信息
  - Bioinfo
  - 生信资料
  - 生信培训
---

生物信息的学习离不开Linux系统，不管自己写命令处理数据，还是使用现有的工具。Linux对我们来讲最重要的是它强大的命令行功能，可以快速、批量、灵活的处理数据的提取、统计和整理等耗时耗力的重复性工作。事实上在日常生信分析中，多数整理工作也都是用Linux命令的组合完成的，相比于写完整的Python或Perl程序更简便快捷；另外，生信分析用到的工具大都只在Linux下运行，而Linux发行版众多，更新速度不一，软件的安装是一个令人头大的事情。

另外对我们大部分朋友来说，接触电脑一直都是图形界面系统，通过单击、双击打开文件、切换目录、安装运行软件都已经运用的得心应手，对文件路径的概念也不太关注。乍一接触Linux，会对其组织逻辑不适应，生信宝典公众号最开始推出Linux教程就是关于[文件和目录](http://mp.weixin.qq.com/s/yKP1Kboji9N4p2Sl1Ovj0Q)的描述，以及与Windows系统的对应，方便做一个快速切换。

文后列出的Linux教程是属于比较精简的生信工作者常用的命令和命令组合。与传统的Linux书籍不同的地方有两点，

1. 摒弃大部分用不到的Linux命令，只保留生信常用的，学习起来更**有的放矢**。

2. 增加生信实战中Linux命令的组合，这是通用Linux教程中所没有的。通用教程只会提供一块块砖，我们是提供**组合好的模块**，直接可以应用，避免只见树木不见森林。

教程有了，还需要一个练习的环境。如果不熟悉Linux时自己安装是比较麻烦的，所以可以借助在线免费平台进行练习。这又体现了我们的教程的又一好处，测试数据自带于教程中，不依赖外部数据的导入，保证了自身的完整性。

推荐的免费平台有2个：[`linuxzoo`](http://linuxzoo.net/)和[`codenvy`](http://codenvy.io/)。

### linuxzoo

访问网址：<http://linuxzoo.net/>，按下图生信宝典录制的动画所示用邮箱注册，注册完之后理解可以使用。收到激活邮件点击后，可永久使用。

注册后，按图示点击选择喜欢的操作系统，这里选的是默认的`Centos`，然后就可以`connect`。最简单的打开方式是直接在浏览器打开使用, 点击`JScript Telnet`即可跳转登录界面。如果用根用户登录，输入用户名`root`和密码`secure`。其它用户名和密码都在首页展示，自己查询即可获得。

![](http://www.ehbio.com/ehbio_resource/linuxzoo.gif)

linuxzoo优点是有**根用户**权限，缺点是**不能**连接外网，但不影响我们大部分代码的练习。

### CODENVY

访问网址：<http://codenvy.io/>，也需要先注册，如果有Github和谷歌账号的话，可以直接登录。然后按图示`Create Workspace`，任选一个`STACK`就可以，都是基于Ubuntu系统的，然后等待完成初始化，即可使用了。

![](http://www.ehbio.com/ehbio_resource/codenvy.io.gif)

优点是有**根用户**权限，同时**可以**连接外网。

### 教程合集

后台回复 "生信宝典福利第一波" 获取完整版教程。

> [生信宝典-Linux教程.pdf](http://www.ehbio.com/tutorial/%E7%94%9F%E4%BF%A1%E5%AE%9D%E5%85%B8-Linux%E6%95%99%E7%A8%8B.pdf)

> [生信宝典Py3_course.pdf](http://www.ehbio.com/tutorial/%E7%94%9F%E4%BF%A1%E5%AE%9D%E5%85%B8Py3_course.pdf)

> [生信宝典-R学习教程.pdf](http://www.ehbio.com/tutorial/%E7%94%9F%E4%BF%A1%E5%AE%9D%E5%85%B8-R%E5%AD%A6%E4%B9%A0%E6%95%99%E7%A8%8B.pdf)

### 系列教程

* [生物信息之程序学习](http://mp.weixin.qq.com/s/xoLBg0pI9seEksa0hMXi0A)
* [关于编程学习的一些思考](https://mp.weixin.qq.com/s/QPesQBExnmaR6uLDTITdgQ)
* [该如何自学入门生物信息学](https://mp.weixin.qq.com/s/Y89T47NRWrCclh04dmyrKg)
* [如何优雅的提问](https://mp.weixin.qq.com/s/xCif04bqZB14Z4OvesK0SQ)
* [生信宝典视频教程](http://mp.weixin.qq.com/s/C4EBufEtFF6bhBKrH8NXng)
* [生信的系列书籍](http://mp.weixin.qq.com/s/IiehgNu3JGVTDa079ll1SQ)

### Linux 

* [Linux - 文件和目录](http://mp.weixin.qq.com/s/yKP1Kboji9N4p2Sl1Ovj0Q)
* [Linux - 文件操作](http://mp.weixin.qq.com/s/4bYMzJclf_xHpqdrlbvAdA)
* [Linux - 文件内容操作](http://mp.weixin.qq.com/s/QFgINAYcQA9kYYSA28wK-Q)
* [Linux - 环境变量和可执行属性](http://mp.weixin.qq.com/s/poFpNHQgHDr0qr2wqfVNdw)
* [Linux - 管道、标准输入输出](http://mp.weixin.qq.com/s/zL9Mw_2ig48gHrIjKM0CMw)
* [Linux - 命令运行监测和软件安装](http://mp.weixin.qq.com/s/TNU7X2mhfVVffaJ7NRBuNA)
* [Linux - 常见错误和快捷操作](http://mp.weixin.qq.com/s/cDIN4_R4nETEB5irmIGFAQ)
* [Linux - 文件列太多，很难识别想要的信息在哪列；别焦急，看这里。](http://mp.weixin.qq.com/s/1QaroFE7AH1pREuq-k2YAw)
* [Linux - 文件排序和FASTA文件操作](http://mp.weixin.qq.com/s/R1OHRhZoDJuAdyVdJr2xHg)
* [Linux - 应用Docker安装软件](http://mp.weixin.qq.com/s/HLHiWMLaWtB7SOJe_jP3mA)
* [Linux - Conda软件安装方法](http://mp.weixin.qq.com/s/A4_j8ZbyprMr1TT_wgisQQ)
* [Linux - 服务器数据定期同步和备份方式](http://mp.weixin.qq.com/s/c2cspK5b4sQScWYMBtG63g)
* [Linux - VIM的强大文本处理方法](https://mp.weixin.qq.com/s/4lUiZ60-aXLilRk9--iQhA)
* [Linux - 查看服务器配置信息](http://mp.weixin.qq.com/s/xq0JfkHJJeHQk1acjOAJUQ)
* [Linux - SED操作，awk的姊妹篇](http://mp.weixin.qq.com/s/cywkIeRbhkYTZvkwTeIVSA)
* [Linux - 常用和不太常用的实用awk命令](http://mp.weixin.qq.com/s/8wD14FXt7fLDo1BjJyT0ew)
* [Linux - 那些查找命令](http://mp.weixin.qq.com/s/xWwj04h4W6yEqQLOfuQ8qA)
* [Linux - 原来你是这样的软连接](https://mp.weixin.qq.com/s/q3ic5WSfLdAnqIhFQX-bUQ)
* [Bash概论 - Linux系列教程补充篇](http://mp.weixin.qq.com/s/lWNp_6W_jLiogmtlk9nO2A)

如果需要学习视频，我们的[生信程序基础课](https://ke.qq.com/course/289264)和[生信Linux学习视频](https://ke.qq.com/course/288048?tuin=20cd7788)正在团购中，欢迎观看。点击**阅读原文** (免费视频)可访问在线视频。


