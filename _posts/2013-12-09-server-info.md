---
title: 显示服务器配置信息
author: ct
layout: post
categories:
  - Bash
tags:
  - Bash
  - Bioinfo
---

学习Linux命令，我们需要有一台Linux服务器。有了服务器，就想看看它的性能怎样。翻出自己较早前写的一个脚本，一键查看系统大部分参数。

This is an old script used to display the hardware information of a server. Generated infos include hostname, IP, Bits-of-OS, CPU, memory, disk .etc.

```
#!/bin/bash
# -*- coding: UTF-8 -*-

#屏幕输出
echo "This lists the information of this computer."

#输出空行
echo

##tput setaf [0-7] –使用ANSI转义设置前景色
#Color Code for tput:  
#0 – Black  
#1 – Red  
#2 – Green  
#3 – Yellow  
#4 – Blue  
#5 – Magenta  
#6 – Cyan  
#7 – White  
##tput sgr0 – Turn off all attributes 

##`hostname` 返回主机名
#`/sbin/ifconfig` ifconfig是linux中用于显示或配置网络设备（网络接口卡）的命令
# sed -n '2p' 显示文件的第2行
# cut是一个选取命令，就是将一段数据经过分析，取出我们想要的内容
# -d ：自定义分隔符，默认为制表符。-f ：与-d一起使用，指定显示哪个区域。

echo "Hostname is $(tput setaf 3)`hostname`$(tput sgr0),\
Ip address is $(tput setaf 3)\
`/sbin/ifconfig | sed -n '2p' | cut -d ':' -f 2 | cut -d ' ' -f 1`.
$(tput sgr0)"
#---------------------------------------------------------------------------

#uname -a ：显示系统名、节点名称、操作系统的发行版号、操作系统版本、运行系统的机器 ID 号。
# Linux ehbio 2.6.32-642.4.2.el6.x86_64 #1 SMP Tue Aug 23 19:58:13 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
#
nuclear=`uname -a | cut -d ' ' -f 3`
bitInfo=`uname -a | cut -d ' ' -f 12`

# if语句，判断系统是64位还是32位
if test $bitInfo == "x86_64"; then
    bit=64
else
    bit=32
fi
#tput bold – Set bold mode 
#head -n	打印每个文件的前n行，而不是打印默认的前10行
# /etc/issue 查看系统登陆信息、发行版本信息
#
echo "The $(tput bold)${bit}$(tput sgr0) bt operating \
system is $(tput bold) `head -n 1 /etc/issue`\
$(tput sgr0), Nuclear info is $(tput setaf 1)\
${nuclear}$(tput sgr0)."
#打印空行

echo
# `sed -n '5p' /proc/cpuinfo 得到如下结果model name	: Intel(R) Xeon(R) CPU G7-4809 v2 @ 4.90GHz
#sed 's/[ ] */ /g'貌似什么也没做啊，这是不对的，这句话是把多个相连空格变为单个空格


echo "The CPU is$(tput setaf 4)`sed -n '5p' /proc/cpuinfo \
| cut -d ':' -f 2 | sed 's/[ ] */ /g'`$(tput sgr0)."

echo

echo "There are $(tput setaf 5)\
`cat /proc/cpuinfo | grep "physical id" | sort | uniq \
| wc -l`$(tput sgr0) physical cpu, \
each physical \
cpu has$(tput setaf 5)`sed -n '12p' /proc/cpuinfo | \
cut -d ':' -f 2`$(tput sgr0) cores,\
$(tput setaf 5)`sed -n '10p' /proc/cpuinfo | \
cut -d ':' -f 2`$(tput sgr0) threads."

echo

echo "There are $(tput setaf 5)\
`cat /proc/cpuinfo | grep "cpu cores" | wc -l`$(tput sgr0) logical cpu."

# sed元字符集 ^ 匹配行开始，如：/^sed/匹配所有以sed开头的行。* 匹配0个或多个字符，如：/ *sed/匹配所有模板是一个或多个空格后紧跟sed的行。
#sed 's/^ *//g' 删除开头的空格


#bc命令是一种支持任意精度的交互执行的计算器语言 bc -l 定义使用的标准数学库


mem=`head -n 1 /proc/meminfo | cut -d ':' -f 2 | sed 's/^ *//g' | cut -d ' ' -f 1`
memInM=$(echo "$mem/1024/1024" | bc -l)

echo

echo "The memory of this server is $(tput setaf 5)${memInM}$(tput sgr0)G."

echo

echo "The disk information is :"

#linux中df命令的功能是用来检查linux服务器的文件系统的磁盘空间占用情况。可以利用该命令来获取硬盘被占用了多少空间，目前还剩下多少空间等信息。
#-h 方便阅读方式显示

echo "`df -h`"
```