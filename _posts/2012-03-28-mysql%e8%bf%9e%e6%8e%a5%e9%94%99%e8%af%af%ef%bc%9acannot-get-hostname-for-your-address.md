---
title: MySql连接错误：Cannot get hostname for your address
author: 悟道
layout: post
permalink: /?p=1907
categories:
  - sql
tags:
  - sql
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

某Web应用的数据库部署在 100.ZZZ.YYY.XXX 的 MySql 5.5.5 实例（新装机器）上，

但是当用PHP或者Python从远端机器上试图访问该数据库时，会得到如下错误提示：

“Can&#8217;t get hostname for your address”。

需要琢磨一下才能明白，这句提示是 MySql Server 返回给客户端的。

也就是说，MySql Server在试图对客户端IP地址进行反向域名解析，试图得到主机名，然而我们发起访问的客户端要么是自己

的机器，要么是机房的服务器，所以无法得到主机名，MySql Server 遂报错，拒绝客户端连接。

事件日志的报告  
此时 MySql Server 所在服务器上，Windows 事件日志出现了如下错误：

事件类型: 警告  
事件来源: MySQL  
事件种类: 无  
事件 ID: 100  
日期: 2010-01-01  
事件: 11:29:13  
用户: N/A  
计算机: SERVERII  
描述:  
IP address &#8217;100.ZZZ.YYY.XXX&#8217; could not be resolved: getnameinfo() returned error (code: 11004).

For more information, see Help and Support Center at http://www.mysql.com. 

简单解释

MySQL server received a request from you to allow you to connect to the database. So next thing it tried to do is to check what name is bound to your IP address (name resolution) and it failed to do so. So it just denied you access.

可以这么理解mysql处理客户端解析的过程：  
1，当 mysql client 发起连接请求时，MySql Server 会主动去查 client 的主机名。  
2，首先查找Windows系统目录下 /etc/hosts 文件，搜索域名和IP的对应关系。  
3，如果hosts文件没有，则查找DNS设置，如果没有设置DNS服务器，会立刻返回失败；如果设置了DNS服务器，就进行反向解析，直到timeout。

解决办法  
第一种方法 修改Hosts

在 MySql Server 所在服务器上，修改 Windows 的 hosts 文件，增加一行记录，如：

100.ZZZ.YYY.XXX dummy.ju690.cn

然后在 100.ZZZ.YYY.XXX 机器上用 Python 发起连接请求，经测试，可以正常连接，说明 MySql Server 这下可以通过 getnameinfo() 解析出100.ZZZ.YYY.XXX 的主机名了。

但这种方法很机械，所以一般采用下面这种方法。  
第二种 修改MySql 的配置文件 my.ini

The solution:  
Just add skip-name-resolve option to your MySQL configuration file (my.ini).

在 MySql Server 的配置文件 My.ini 中，增加如下两行：

[mysqld]

skip-name-resolve

它将禁止 MySql Server 对外部连接进行 DNS 解析，使用这一选项可以消除 MySql 进行 DNS 解析的时间。

但需要注意，如果开启该选项，则所有远程主机连接授权都要使用IP地址方式，否则MySQL将无法正常处理连接请求。

参考：

http://www.ixdba.net/article/89/2127.html

http://blog.chinaunix.net/u/25264/showart_1936561.html

可能的后果

如果开启 skip-name-resolve 选项，要确认 MySql 是否采用过主机名的授权，  
在 mysql 中运行如下命令：

mysql> select user,host from mysql.user where host <> &#8216;localhost&#8217; ;

一般会得到以“%”授权（也就是任何地址）的记录：

+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;-+  
| user | host |  
+&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;+&#8212;&#8212;&#8212;&#8212;-+  
| root | % |  
| user_sync | 192.168.0.113 |

如果有host名是什么“DB1”“DB2”的，那么删除授权表中有 hostanme 的记录，然后重启mysqld。

参考http://www.cnblogs.com/zhengyun\_ustc/archive/2010/10/13/skip\_name_resolve.html