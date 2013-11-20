---
title: 终端输出格式化（颜色，粗体，下划线）文本
author: 悟道
layout: post
permalink: /?p=957
categories:
  - bash
tags:
  - bash
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

Linux的bash终端为命令的运行提供了极大的方便，但其单调的输出不方便强调重点，醒目标记。这里使用[tput][1]来帮助输出格式化的文本。

首先介绍下基本使用：

`user: echo $(tput bold)BOld text $(tput sgr0)`

**BOld text**

`user:echo $(tput setaf 1)Red text$(tput sgr0)`

<span style="color: #ff0000;">Red text</span>

但是这样使用毕竟不太直观和方便，可以把这些格式存入**.bashrc**文件中，赋予它含义。

在**.bashrc**中可以有两种方式来使用，第一个使用**export**

<div class="wp_codebox">
  <table>
    <tr id="p95799">
      <td class="code" id="p957code99">
        <pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtund</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput sgr <span style="color: #000000;"></span> <span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>    <span style="color: #666666; font-style: italic;"># Underline</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtbld</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput bold<span style="color: #7a0874; font-weight: bold;">&#41;</span>       <span style="color: #666666; font-style: italic;"># Bold</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtred</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>    <span style="color: #666666; font-style: italic;"># Red</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtgrn</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">2</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>    <span style="color: #666666; font-style: italic;"># Green</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtylw</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">3</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>    <span style="color: #666666; font-style: italic;"># Yellow</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtblu</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">4</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>    <span style="color: #666666; font-style: italic;"># Blue</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtpur</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">5</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>    <span style="color: #666666; font-style: italic;"># Purple</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtcyn</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">6</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>    <span style="color: #666666; font-style: italic;"># Cyan</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtwht</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">7</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>    <span style="color: #666666; font-style: italic;"># White</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">txtrst</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput sgr0<span style="color: #7a0874; font-weight: bold;">&#41;</span>       <span style="color: #666666; font-style: italic;"># Text reset</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">bldred</span>=<span style="color: #800000;">${txtbld}</span><span style="color: #800000;">${txtred}</span> <span style="color: #666666; font-style: italic;">#  red</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">bldblu</span>=<span style="color: #800000;">${txtbld}</span>$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">4</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #666666; font-style: italic;">#  blue</span>
<span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">bldwht</span>=<span style="color: #800000;">${txtbld}</span>$<span style="color: #7a0874; font-weight: bold;">&#40;</span>tput setaf <span style="color: #000000;">7</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #666666; font-style: italic;">#  white</span></pre>
      </td>
    </tr>
  </table>
</div>

&nbsp;

这样在使用方法如下(注意$后面跟的是{})：

user: echo ${txtbld}BOld text${txtrst}  
**BOld text**

优点是可以在脚本中调用。

另外一种方法是用alias

<div class="wp_codebox">
  <table>
    <tr id="p957100">
      <td class="code" id="p957code100">
        <pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtund</span>=<span style="color: #ff0000;">"tput sgr 0 1"</span>    <span style="color: #666666; font-style: italic;"># Underline</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtbld</span>=<span style="color: #ff0000;">"tput bold"</span>       <span style="color: #666666; font-style: italic;"># Bold</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtred</span>=<span style="color: #ff0000;">"tput setaf 1"</span>    <span style="color: #666666; font-style: italic;"># Red</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtgrn</span>=<span style="color: #ff0000;">"tput setaf 2"</span>    <span style="color: #666666; font-style: italic;"># Green</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtylw</span>=<span style="color: #ff0000;">"tput setaf 3"</span>    <span style="color: #666666; font-style: italic;"># Yellow</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtblu</span>=<span style="color: #ff0000;">"tput setaf 4"</span>    <span style="color: #666666; font-style: italic;"># Blue</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtpur</span>=<span style="color: #ff0000;">"tput setaf 5"</span>    <span style="color: #666666; font-style: italic;"># Purple</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtcyn</span>=<span style="color: #ff0000;">"tput setaf 6"</span>    <span style="color: #666666; font-style: italic;"># Cyan</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtwht</span>=<span style="color: #ff0000;">"tput setaf 7"</span>    <span style="color: #666666; font-style: italic;"># White</span>
<span style="color: #7a0874; font-weight: bold;">alias</span> <span style="color: #007800;">txtrst</span>=<span style="color: #ff0000;">"tput sgr0"</span>       <span style="color: #666666; font-style: italic;"># Text reset</span></pre>
      </td>
    </tr>
  </table>
</div>

&nbsp;

这样在使用方法如下(注意$后面跟的是())：

user: echo $(txtbld)BOld text$(txtrst)  
**BOld text**

缺点是：不可以在脚本中调用，原因不知。

解决方法有一个，把每行alias命令生成一个可执行文件，并保存到${PATH}中任一路径下，作为命令使用。

文件内容格式为：

<div class="wp_codebox">
  <table>
    <tr id="p957101">
      <td class="code" id="p957code101">
        <pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">#!/bin/bash</span>
&nbsp;
tput bold
tput setaf <span style="color: #000000;">1</span></pre>
      </td>
    </tr>
  </table>
</div>

参考：<http://linuxtidbits.wordpress.com/2008/08/11/output-color-on-bash-scripts/>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

> \e[01;37mstring\e[00m

\e 高级选项输出到窗口 （PHP，Python 中用 \033 代替）  
[ 非打印字符开始  
] 非打印字符结束  
string 待打印的字符串

样式代码  
01;37m  
m 表示结束

\e[00m 恢复正常  
第一组：  
00 普通  
01 高亮  
02 闪烁  
04 下划线  
07 使用较淡的颜色作为背景  
09 删除线

第二组：  
30 black  
31 red  
32 green  
33 brown  
34 blue  
35 purple  
36 cyan  
37 white

备注：上面的 3 替换成 4 的话，就是相应的背景色  
高级用法（同时使用前景色，背景色）：01;37;46m

一个Python脚本在终端输出带颜色的文字

<div class="wp_codebox">
  <table>
    <tr id="p957102">
      <td class="code" id="p957code102">
        <pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
<span style="color: #808080; font-style: italic;"># encoding=utf-8</span>
&nbsp;
<span style="color: #ff7700;font-weight:bold;">if</span> __name__ == <span style="color: #483d8b;">'__main__'</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">"<span style="color: #000099; font-weight: bold;">\0</span>33[01;31mtest<span style="color: #000099; font-weight: bold;">\0</span>33[00m"</span></pre>
      </td>
    </tr>
  </table>
</div>

<https://gist.github.com/801785>

&nbsp;

其它参考资料：

http://tldp.org/LDP/abs/html/colorizing.html

&nbsp;

 [1]: http://linux.about.com/library/cmd/blcmdl1_tput.htm