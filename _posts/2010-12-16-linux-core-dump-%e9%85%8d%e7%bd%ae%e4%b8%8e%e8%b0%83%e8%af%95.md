---
title: Linux Core Dump 配置与调试【转载】
author: 悟道
layout: post
permalink: /?p=559
categories:
  - C
  - 转载
tags:
  - C
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

Linux Core Dump 配置与调试

http://blog.csdn.net/ecjtuync/archive/2009/04/29/4133149.aspx

1.core文件的生成开关和大小限制  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;  
1）使用ulimit -c命令可查看core文件的生成开关。若结果为0，则表示关闭了此功能，不会生成core文件。  
2） 使用ulimit -cfilesize命令，可以限制core文件的大小（filesize的单位为kbyte）。若ulimit -cunlimited，则表示core文件的大小不受限制。如果生成的信息超过此大小，将会被裁剪，最终生成一个不完整的core文件。在调试此 core文件的时候，gdb会提示错误。

2.core文件的名称和生成路径  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
若系统生成的core文件不带其它任何扩展名称，则全部命名为core。新的core文件生成将覆盖原来的core文件。  
1）/proc/sys/kernel/core\_uses\_pid可以控制core文件的文件名中是否添加pid作为扩展。文件内容为1，表示添加pid作为扩展名，生成的core文件格式为core.xxxx；为0则表示生成的core文件同一命名为core。  
可通过以下命令修改此文件：  
echo &#8220;1&#8243; > /proc/sys/kernel/core\_uses\_pid  
2）proc/sys/kernel/core_pattern可以控制core文件保存位置和文件名格式。  
可通过以下命令修改此文件：  
echo &#8220;/corefile/core-%e-%p-%t&#8221; > core_pattern，可以将core文件统一生成到/corefile目录下，产生的文件名为core-命令名-pid-时间戳  
以下是参数列表:  
%p &#8211; insert pid into filename 添加pid  
%u &#8211; insert current uid into filename 添加当前uid  
%g &#8211; insert current gid into filename 添加当前gid  
%s &#8211; insert signal that caused the coredump into the filename 添加导致产生core的信号  
%t &#8211; insert UNIX time that the coredump occurred into filename 添加core文件生成时的unix时间  
%h &#8211; insert hostname where the coredump happened into filename 添加主机名  
%e &#8211; insert coredumping executable name into filename 添加命令名

3.用gdb查看core文件:  
下面我们可以在发生运行时信号引起的错误时发生core dump了.  
发生core dump之后, 用gdb进行查看core文件的内容, 以定位文件中引发core dump的行.  
gdb \[exec file\] \[core file\]  
如:  
gdb ./test test.core  
在进入gdb后, 用bt命令查看backtrace以检查发生程序运行到哪里, 来定位core dump的文件->行.

4.开发板上使用core文件调试  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;  
如果开发板的操作系统也是linux，core调试方法依然适用。如果开发板上不支持gdb，可将开发板的环境（头文件、库）、可执行文件和core文件拷贝到PC的linux下，运行相关命令即可。  
注意：待调试的可执行文件，在编译的时候需要加-g，core文件才能正常显示出错信息！

注意的问题：

在Linux下要保证程序崩溃时生成Coredump要注意这些问题：

　　一、要保证存放Coredump的目录存在且进程对该目录有写权限。存放Coredump的目录即进程的当前目录，一般就是当初发出命令启动该进程时所在的目录。但如果是通过脚本启动，则脚本可能会修改当前目录，这时进程真正的当前目录就会与当初执行脚本所在目录不同。这时可以查看”/proc/<进程pid>/cwd“符号链接的目标来确定进程真正的当前目录地址。通过系统服务启动的进程也可通过这一方法查看。

　　二、若程序调用了seteuid()/setegid()改变了进程的有效用户或组，则在默认情况下系统不会为这些进程生成Coredump。很多服务程序都会调用seteuid()，如MySQL，不论你用什么用户运行mysqld\_safe启动MySQL，mysqld进行的有效用户始终是msyql用户。如果你当初是以用户A运行了某个程序，但在ps里看到的这个程序的用户却是B的话，那么这些进程就是调用了seteuid了。为了能够让这些进程生成core dump，需要将/proc/sys/fs /suid\_dumpable文件的内容改为1（一般默认是0）。

　　三、这个一般都知道，就是要设置足够大的Core文件大小限制了。程序崩溃时生成的Core文件大小即为程序运行时占用的内存大小。但程序崩溃时的行为不可按平常时的行为来估计，比如缓冲区溢出等错误可能导致堆栈被破坏，因此经常会出现某个变量的值被修改成乱七八糟的，然后程序用这个大小去申请内存就可能导致程序比平常时多占用很多内存。因此无论程序正常运行时占用的内存多么少，要保证生成Core文件还是将大小限制设为unlimited为好。