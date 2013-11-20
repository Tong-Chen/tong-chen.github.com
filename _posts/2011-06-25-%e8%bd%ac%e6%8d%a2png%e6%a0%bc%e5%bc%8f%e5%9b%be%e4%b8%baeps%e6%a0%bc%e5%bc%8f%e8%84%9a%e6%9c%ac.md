---
title: 转换png格式图为eps格式脚本
author: 悟道
layout: post
permalink: /?p=1047
categories:
  - bash
  - pic
tags:
  - bash
  - pic
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<div class="wp_codebox">
  <table>
    <tr id="p1047123">
      <td class="code" id="p1047code123">
        <pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">#!/bin/bash</span>
<span style="color: #007800;">prefix</span>=<span style="color: #000000; font-weight: bold;">`</span><span style="color: #c20cb9; font-weight: bold;">basename</span> <span style="color: #007800;">$1</span> .png<span style="color: #000000; font-weight: bold;">`</span>
pngtopnm <span style="color: #007800;">$1</span> <span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #007800;">$prefix</span>.pnm
pnmtops <span style="color: #660033;">-noturn</span> <span style="color: #660033;">-rle</span> <span style="color: #007800;">$prefix</span>.pnm <span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #007800;">$prefix</span>.ps <span style="color: #000000;">2</span><span style="color: #000000; font-weight: bold;">&gt;/</span>dev<span style="color: #000000; font-weight: bold;">/</span>null
<span style="color: #c20cb9; font-weight: bold;">ps2epsi</span> <span style="color: #007800;">$prefix</span>.ps
&nbsp;
<span style="color: #000000; font-weight: bold;">/</span>bin<span style="color: #000000; font-weight: bold;">/</span><span style="color: #c20cb9; font-weight: bold;">rm</span> <span style="color: #660033;">-f</span> <span style="color: #007800;">$prefix</span>.ps
<span style="color: #000000; font-weight: bold;">/</span>bin<span style="color: #000000; font-weight: bold;">/</span><span style="color: #c20cb9; font-weight: bold;">rm</span> <span style="color: #660033;">-f</span> <span style="color: #007800;">$prefix</span>.pnm
<span style="color: #c20cb9; font-weight: bold;">mv</span> <span style="color: #007800;">$prefix</span>.epsi <span style="color: #007800;">$prefix</span>.eps</pre>
      </td>
    </tr>
  </table>
</div>

一点解释：为什么选用ps2epsi而不是ps2eps?  
原因：后者转换后会缺失上半部分。

脚本缺点：转换后图例有些模糊，图形需要放大才能显示清晰，矢量图越大越清晰。