---
title: bash脚本去除行首行尾的空格
author: 悟道
layout: post
categories:
  - bash
tags:
  - bash
---

<div class="wp_codebox">
  <table>
    <tr id="p1734">
      <td class="line_numbers">
        <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
</pre>
      </td>
      
      <td class="code" id="p173code4">
        <pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">#!/bin/bash</span>
<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">'This is used to delete the space begin and end of the line'</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">test</span> <span style="color: #007800;">$#</span> <span style="color: #660033;">-ne</span> <span style="color: #000000;">1</span>; <span style="color: #000000; font-weight: bold;">then</span>
        <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #000000;">1</span><span style="color: #000000; font-weight: bold;">&</span>gt;<span style="color: #000000; font-weight: bold;">&</span>amp;<span style="color: #000000;">2</span> <span style="color: #ff0000;">"Usage $0 file"</span>
        <span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span>
<span style="color: #000000; font-weight: bold;">fi</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">set</span> <span style="color: #660033;">-x</span>
&nbsp;
<span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #660033;">-i</span> <span style="color: #ff0000;">'s/^ *//g'</span> <span style="color: #007800;">$1</span>
<span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #660033;">-i</span> <span style="color: #ff0000;">'s/ *$//g'</span> <span style="color: #007800;">$1</span>
&nbsp;
<span style="color: #c20cb9; font-weight: bold;">sed</span> <span style="color: #660033;">-i</span> <span style="color: #ff0000;">'s/[ ][ ]*/ /g'</span> <span style="color: #007800;">$1</span></pre>
      </td>
    </tr>
  </table>
</div>

去除行首行尾多余的空格，把中间数量不等的空格替换为一个。主要用来处理uniq -c的输出文件。
