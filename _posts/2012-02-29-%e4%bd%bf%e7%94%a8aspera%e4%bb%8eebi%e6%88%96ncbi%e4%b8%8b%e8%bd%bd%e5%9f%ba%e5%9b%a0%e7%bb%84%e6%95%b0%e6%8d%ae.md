---
title: 使用Aspera从EBI或NCBI下载基因组数据
author: 悟道
layout: post
permalink: /?p=1556
categories:
  - bioinformatics
tags:
  - bioinformatics
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<div>
  <p>
    做基因组数据分析，可能经常从NCBI的GEO/SRA或者EBI的ENA数据库下载高通量的数据，动辄几十G的数据用wget下载实在太纠结，这时就要用到神器-Aspera了。
  </p>
  
  <p>
    使用Aspera，最简单的方法当然就是使用浏览器插件Aspera Connect了，跟迅雷、Flashget的用法差不多，直接单击Aspera支持的下载地址，就自动切换到Aspera的窗口开始下载了。
  </p>
  
  <p>
    当我们登录到自己的服务器终端里面的时候，可能更希望在终端里直接下载数据，而不是先把数据下载到自己的硬盘里，再上传到服务器，这种情况下带有窗口界面的Aspera Connect就无法使用了吗？
  </p>
  
  <p>
    当然可以，Aspera Connect安装包里内置了Aspera的命令行工具，这里对其安装和使用方法简要介绍一下:
  </p>
  
  <h3>
    安装
  </h3>
  
  <p>
    首先，到<a href="http://www.asperasoft.com/en/downloads/8?list">aspera网站</a>下载你的操作系统对应的aspera connect。(如果选Linux，下载以后会是一个几M大，内嵌二进制代码的shell脚本。。) 。不需要root或者sudo权限，直接安装之：<br /> <strong>$ sh aspera-connect-2.4.7.37118-linux-64.sh</strong><br /> 安装好以后，会在HOME目录下新建一个叫.aspera的目录，有两个文件比较重要:<br /> 一个是ascp的可执行文件:<br /> <strong>~/.aspera/connect/bin/ascp</strong><br /> 另一个ascp的密钥文件:<br /> <strong>~/.aspera/connect/etc/asperaweb_id_dsa.putty</strong>
  </p>
  
  <p>
    建议将密钥备份到HOME目录下方便使用:<br /> <strong>$ cp ~/.aspera/connect/etc/asperaweb_id_dsa.putty ~/</strong><br /> 再把ascp可执行文件的路径加入PATH变量中，或者将其拷贝到当前目录。
  </p>
  
  <h3>
    使用
  </h3>
  
  <p>
    执行以下两条命令(注意最后要加.)<br /> 从EBI下载:<br /> <strong>$ ascp -i ~/asperaweb_id_dsa.putty era-fasp@fasp.sra.ebi.ac.uk:/vol1/ERA012/ERA012008/sff/library08_GJ6U61T06.sff .</strong><br /> 从NCBI下载:<br /> <strong>$ ascp -i ~/asperaweb_id_dsa.putty anonftp@ftp-private.ncbi.nlm.nih.gov:/sra/sra-instant/reads/ByRun/litesra/SRR/SRR096/SRR096072/SRR096072.lite.sra .</strong>
  </p>
  
  <p>
    这个时候的速度相比于wget，应该已经很快了，大约能达到9Mb/s以上，如果还嫌慢，可以在-i 参数的前面添加几项设置，像这样:<br /> ascp -QT -l 100M -i ~/asperaweb_id_dsa.putty era-fasp@fasp.sra.ebi.ac.uk:/vol1/ERA012/ERA012008/sff/library08_GJ6U61T06.sff .这样可以将速度提高到20Mb/s左右，偶尔能达到100Mb/s。
  </p>
  
  <h3>
    ascp下载地址的获取
  </h3>
  
  <p>
    以EBI上的SRR346368这套数据为例。首先到<a href="http://www.ebi.ac.uk/ena/data/view/SRR346368">EBI页面</a>里，找到你想要下载的文件，将指针移到这个文件的”ftp”这一列，即可看到其ftp地址，例如: ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR346/SRR346368/SRR346368.fastq.gz,<br /> 然后呢:将 ftp://ftp.sra.ebi.ac.uk 换成 era-fasp@fasp.sra.ebi.ac.uk即可:<br /> <strong>$ ascp -i ~/asperaweb_id_dsa.putty era-fasp@fasp.sra.ebi.ac.uk:/vol1/fastq/SRR346/SRR346368/SRR346368.fastq.gz .</strong><br /> NCBI的SRA数据库也是同样的方法，即可获取其ascp下载地址。
  </p>
  
  <h3>
    更多的说明
  </h3>
  
  <p>
    请参见官方的SRA下载手册:<br /> NCBI: <a href="http://www.ncbi.nlm.nih.gov/books/NBK47540" target="_blank">http://www.ncbi.nlm.nih.gov/books/NBK47540</a>/<br /> EBI: <a href="http://www.ebi.ac.uk/ena/about/sra_data_download" target="_blank">http://www.ebi.ac.uk/ena/about/sra_data_download</a>
  </p>
  
  <p>
    P.S. 好像我身边的人喜欢EBI的偏多，因为对于同一套公开数据，EBI可以下载到原始测序文件(Fastq格式)，而NCBI中只能下载压缩转换格式后的文件(SRA格式)。不知道大家喜欢用哪一种？
  </p>
</div>

&nbsp;

转载自：http://www.samuthing.com/?p=347

&nbsp;

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;附件部分&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

本人实现一个脚本来简化使用

<div class="wp_codebox">
  <table>
    <tr id="p1556147">
      <td class="code" id="p1556code147">
        <pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
<span style="color: #808080; font-style: italic;"># -*- coding: utf-8 -*-</span>
<span style="color: #808080; font-style: italic;">#from __future__ import division, with_statement</span>
<span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
Copyright 2010, 陈同 (chentong_biology@163.com).  
Please see the license file for legal information.
===========================================================
'</span><span style="color: #483d8b;">''</span>
__author__ = <span style="color: #483d8b;">'chentong & ct586[9]'</span>
__author_email__ = <span style="color: #483d8b;">'chentong_biology@163.com'</span>
<span style="color: #808080; font-style: italic;">#=========================================================</span>
<span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
<span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">os</span>
&nbsp;
<span style="color: #ff7700;font-weight:bold;">def</span> main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">"Download data from ncbi or ebi with ascp"</span>
    lensa = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> lensa <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">2</span>:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">'Using python %s url[point to a file or <span style="color: #000099; font-weight: bold;">\</span>
directory] type[default ebi. <span style="color: #000099; font-weight: bold;">\</span>
another choice is ncbi] <span style="color: #000099; font-weight: bold;">\</span>
dest[default ./]'</span> <span style="color: #66cc66;">%</span> <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span>
        <span style="color: #dc143c;">sys</span>.<span style="color: black;">exit</span><span style="color: black;">&#40;</span><span style="color: #ff4500;"></span><span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">#------------------------------------</span>
    url=<span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> lensa == <span style="color: #ff4500;">3</span>:
        <span style="color: #008000;">type</span> = <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
        <span style="color: #008000;">type</span> = <span style="color: #483d8b;">'ebi'</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span> == <span style="color: #ff4500;">4</span>:
        dest = <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
        dest = <span style="color: #483d8b;">'.'</span>
    <span style="color: #808080; font-style: italic;">#-------------------------------</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #ff7700;font-weight:bold;">not</span> url.<span style="color: black;">startswith</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"ftp://ftp"</span><span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">"Wrong format, should be ftp://ftp.sra.ebi.ac.uk/"</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">"Wrong URL:"</span>, url
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">type</span> == <span style="color: #483d8b;">'ebi'</span>:
        url = url.<span style="color: black;">replace</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'ftp://ftp'</span>, <span style="color: #483d8b;">'era-fasp@fasp'</span><span style="color: black;">&#41;</span>
        url = url.<span style="color: black;">replace</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'/'</span>, <span style="color: #483d8b;">':/'</span>, <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">type</span> == <span style="color: #483d8b;">'ncbi'</span>:
        url = url.<span style="color: black;">replace</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'ftp://ftp-trace.ncbi.nlm.nih.gov'</span>, \
            <span style="color: #483d8b;">'anonftp@ftp-private.ncbi.nlm.nih.gov:'</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">"Wrong type %s"</span> <span style="color: #66cc66;">%</span> <span style="color: #008000;">type</span>
    <span style="color: #dc143c;">cmd</span> = \
        <span style="color: #483d8b;">'ascp -QTr -k1 -l 200M -i ~/.aspera/connect/etc/asperaweb_id_dsa.putty '</span>\
        + url + <span style="color: #483d8b;">' '</span> + dest + <span style="color: #483d8b;">'&gt;ascp.log 2&gt;&1'</span>
    <span style="color: #dc143c;">os</span>.<span style="color: black;">system</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">cmd</span><span style="color: black;">&#41;</span>
<span style="color: #ff7700;font-weight:bold;">if</span> __name__ == <span style="color: #483d8b;">'__main__'</span>:
    main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

&nbsp;