---
title: windows+putty+firefox 和 windows+putty+chrom+SwitchySharp
author: 悟道
layout: post
permalink: /?p=1938
categories:
  - fan
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

## windows+putty+firefox

具体方法：  
1. 下载使用PuTTY  
2. 在PuTTY设置中，SSH的Tunnel选项中下，自定义一个Source port(12345)，并选择Dynamic和Auto项。  
3. 连接到服务器，输入用户名和密码，此时就在本地和服务器之间建立了一个SSH隧道，可以使用SOCKS代理。  
4. 在Firefox的代理设置中，选择SOCKS代理，IP设为127.0.0.1，端口号设为刚才在PuTTY中设置的端口号(12345)。  
5. 此时Firefox将网页的请求都通过主机与服务器之间的SSH隧道传输，可以访问实验室内部资源。

&nbsp;

## windows+putty+chrom+SwitchySharp

具体方法：

1. 下载使用PuTTY  
2. 在PuTTY设置中，SSH的Tunnel选项中下，自定义一个Source port(12345)，并选择Dynamic和Auto项。  
3. 连接到服务器，输入用户名和密码，此时就在本地和服务器之间建立了一个SSH隧道，可以使用SOCKS代理。

4.在switchySharp选项&#8211;情景模式&#8212;手动设置&#8212;SOCKS代理127.0.0.1（固定的，不改动）， 端口12345（端口可改）。选择socks v5。

[<img class="alignleft size-medium wp-image-1942" title="1" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/04/1-300x165.png" alt="socks 127.0.0.1 12345 socksv5" width="300" height="165" />][1]

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

5.如果翻墙，还需设置switchySharp选项&#8211;切换规则，

规则列表url为：http://autoproxy-gfwlist.googlecode.com/svn/trunk/gfwlist.txt

[<img class="alignleft size-medium wp-image-1943" title="2" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/04/2-300x160.png" alt="" width="300" height="160" />][2]

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

免费ssh代理

http://www.cjb.net/shell.html

blog.onlybird.com

feelssh.com

 [1]: http://210.75.224.29/wordpress/wp-content/uploads/2012/04/1.png
 [2]: http://210.75.224.29/wordpress/wp-content/uploads/2012/04/2.png