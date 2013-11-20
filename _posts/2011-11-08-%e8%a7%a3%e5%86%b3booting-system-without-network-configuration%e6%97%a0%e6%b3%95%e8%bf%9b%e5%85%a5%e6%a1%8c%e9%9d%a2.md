---
title: 解决booting system without network configuration无法进入桌面
author: 悟道
layout: post
permalink: /?p=1235
categories:
  - linux
tags:
  - linux
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

ubuntu11.10升级之后出现的问题

问题的症结在于：Failed to connect to socket /var/run/dbus/system\_bus\_socket: Connection refused。  
这个是系统启动停留在那个booting system with。。。界面时输出的日志。

今天又尝试了以前看到的一些解决方案，试了一些，果然可以啦。

方案地址：<https://bugs.launchpad.net/ubuntu/+source/dbus/+bug/811441>

按ctrl+alt+F1(F2-F6)进入命令行界面，具体操作如下：

<div>
  <blockquote>
    <div>
          sudo mkdir /run<br /> sudo mkdir /run/lock<br /> sudo mv /var/run/* /run<br /> sudo mv /var/lock/* /run/lock</p> <p>
        sudo rm -rf /var/run<br /> sudo rm -rf /var/lock
      </p>
      
      <p>
        sudo ln -s /run /var/run<br /> sudo ln -s /run/lock /var/lock
      </p>
    </div>
  </blockquote>
</div>

> <div>
>       sudo shutdown -r now
> </div>

<div>
  转载：<a href="http://www.the5fire.net/resolve-ubuntu-boot.html">http://www.the5fire.net/resolve-ubuntu-boot.html</a>
</div>