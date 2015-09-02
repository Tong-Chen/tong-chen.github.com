---
title: wget命令总结
author: 悟道
layout: post
permalink: /?p=637
categories:
  - bash
  - 转载
tags:
  - bash
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

wget 是一个命令行的下载工具。对于我们这些 Linux 用户来说，几乎每天都在使用它。下面为大家介绍几个有用的 wget 小技巧，可以让你更加高效而灵活的使用 wget。

* $ wget -r -np -nd <a href="http://example.com/packages/" target="_blank">http://example.com/packages/</a>

这条命令可以下载 <a href="http://example.com/" target="_blank">http://example.com</a> 网站上 packages 目录中的所有文件。其中，**<span style="color: #ff0000;">-np 的作用是不遍历父目录，-nd 表示不在本机重新创建目录结构。</span>**

* $ wget -r -np -nd &#8211;accept=iso <a href="http://example.com/centos-5/i386/" target="_blank">http://example.com/centos-5/i386/</a>

与上一条命令相似，但多加了一个 <span style="color: #ff0000;"><strong>&#8211;accept=iso 选项，这指示 wget 仅下载 i386 目录中所有扩展名为 iso 的文件</strong></span>。你也可以指定多个扩展名，只需用逗号分隔即可。

* $ wget -i filename.txt

此命令常用于批量下载的情形，把所有需要下载文件的地址放到 filename.txt 中，然后 wget 就会自动为你下载所有文件了。

* $ wget -c <a href="http://example.com/really-big-file.iso" target="_blank">http://example.com/really-big-file.iso</a>

这里所指定的<span style="color: #ff0000;"><strong> -c 选项的作用为断点续传。</strong></span>

* $ wget -m -k (-H) <a href="http://www.example.com/" target="_blank">http://www.example.com/</a>

该命令可用来镜像一个网站，wget 将对链接进行转换。如果网站中的图像是放在另外的站点，那么可以使用 -H 选项。

有的网站内robots.txt内的内容会有限制，会有disallow:/的内容，这样的话直接用  
wget -r -np -nd &#8211;accept=md5 <a href="http://mirrors.kernel.org/opensuse/distribution/11.2/iso/" target="_blank">http://mirrors.kernel.org/opensuse/distribution/11.2/iso/</a>  
就不会下载后缀为md5的文件，会受robots文件的限制，加个-e robots=off就可以了。  
wget -e robots=off -r -np -nd -A md5 http://mirrors.kernel.org/opensuse/distribution/11.2/iso/  
(-A md5是&#8211;accept=md5的简写)

From   <http://colder.blog.163.com/blog/static/173946618201011271311475/>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

那我怎么设定下载时间呢？  
用at来就可以很好的定制工作时间：  
bash$ at 2300  
warning: commands will be executed using /bin/sh  
at> wget http://place.your.url/here  
at> press Ctrl-D  
这样，我们设定了下载工作在晚上11点进行。为了使这个安排能够正常进行，请确  
认atd这个后台程序正在运行。

crontab -e定制任务

0 23 \* \* 1-5 wget -c -N http://place.your.url/here  
0 6 \* \* 1-5 killall wget

这个crontab文件指定某些任务定期地执行。前五列声明是什么时候执行这个命令，而每行的剩余部分则告诉crontab执行什么内容。  
前两列指定了每天一到晚上11点就开始用wget下载，一到早上6点就停止一切wget下载。第三四列的*表示每个月的每一天都执行这个任务。第五列则指定了一个星期的哪几天来执行这个程序。 –”1-5″表示从星期一到星期五。

这样在每个工作日的晚上11点，下载工作开始，到了上午的6点，任何的wget任务就被停掉了。  
wget的这个”-N”参数将会检查目标文件的时间戳，如果匹配了，下载程序就会停止，因为它说明整个文件已经下载完全了。

如何下载动态变化的网页  
有些网页每天都要根据要求变化好几次.所以从技术上讲,目标不再是一个文件,它没有文件长度.因此”-c”这个参数也就失去了意义.  
例如:一个PHP写的并且经常变动的linux周末新闻网页:  
bash$ wget http://lwn.net/bigpage.php3

我办公室里的网络条件经常很差,给我的下载带了很大的麻烦,所以我写了个简单的脚本来检测动态页面是否已经完全更新了.  
#!/bin/bash

#create it if absent  
touch bigpage.php3

#check if we got the whole thing  
while ! grep -qi bigpage.php3  
do  
rm -f bigpage.php3

#download LWN in one big page  
wget http://lwn.net/bigpage.php3

done  
这个脚本能够保证持续的下载该网页,直到网页里面出现了”&#8221;,这就表示该文件已经完全更新了.

转载： <http://blog.csai.cn/user1/14696/archives/2007/15903.html>