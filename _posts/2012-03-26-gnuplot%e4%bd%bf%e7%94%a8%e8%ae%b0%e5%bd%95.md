---
title: gnuplot使用记录
author: 悟道
layout: post
permalink: /?p=1886
categories:
  - gnuplot
tags:
  - gnuplot
  - pic
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.取消legend， 参见<http://t16web.lanl.gov/Kawano/gnuplot/legend-e.html#2.1>

> set nokey  
> plot f(x) notitle, &#8220;file.dat&#8221; title &#8220;data&#8221;

2.设置legend的位置

> set key left bottom #other choice top right  
> set key 100,100

3.gunplot 图形的坐标<http://t16web.lanl.gov/Kawano/gnuplot/label2-e.html#4.4>

> gnuplot> set label &#8220;(0,0) first&#8221; at first 0, first 0  
> gnuplot> set label &#8220;(0,0) graph&#8221; at graph 0, graph 0  
> gnuplot> set label &#8220;(0,0) screen&#8221; at screen 0, screen 0

4.画垂直线<http://stackoverflow.com/questions/6980119/drawing-vertical-lines-in-between-bezier-curves>

<http://stackoverflow.com/questions/4457046/how-do-i-draw-a-vertical-line-in-gnuplot>

<http://tex.stackexchange.com/questions/16828/gnuplottex-automatic-plotting-and-vertical-line-indication>

> set arrow from 0,0.05 to 0,0.14 nohead lt 0 lw 0.5
> 
> #没有头的箭头，lt 0表示dashed line，lw 0.5表示线宽0.5

5.gnuplot设置图例的字体大小

> set key font &#8220;,16&#8243;  
> set terminal png font &#8220;/Library/Fonts/Arial.ttf&#8221; 14

6.Could not find/open font when opening font &#8220;arial&#8221;, using internal non-scalable font

<pre class="brush: bash; title: ; notranslate" title="">ubuntu software center : ttf-mscorefonts
</pre>

7.

8.

9.

10.

11.

12.

13.

14.