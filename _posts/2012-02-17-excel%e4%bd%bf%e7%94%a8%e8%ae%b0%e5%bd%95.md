---
title: Excel使用记录
author: 悟道
layout: post
permalink: /?p=1509
categories:
  - office
tags:
  - excel
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

#——————————————————————

如果公式不工作，先查看下数据类型是否为“常规”。

#——————————————————————

1.统计某个字段出现的次数

> =countif(D1:D10, &#8216;chr*&#8217;)

2.利用if做列之间的比较，相当于diff

> IF(&#8216;boolean expression&#8217;, &#8216;value for true&#8217;, &#8216;value for false&#8217;)
> 
> IF(AND(A1=B1,A1=C1),1,0)

3.excel中求对数

> log(number,base)

4.excel中提取字符串

> =RIGHT(B3,LEN(B3)-FIND(&#8220;:&#8221;,B3))  【B3：mmu04740:Olfactory transduction&#8212;得到Olfactory transduction】

5.excel中转换大小写

> Upper, lower, proper

6.excel中使用grep

> =VLOOKUP(O2,$A$2:$L$239,2)

7.excel中做出正负不同颜色的柱状图

> 选定注&#8211;右键（系列格式填充）&#8211;填充（选择以互补色代表负值，选择颜色）

8.excel中正负柱不同标签

> 选定一个柱，右键添加数据标签&#8211;选定数据标签&#8211;设置格式（选择“类别名称”，调整对齐方式）

9.excel中单元格自动换行和取消自动换行

> Alt+Enter可以让单元格内文字自动换行，取消时可点击右键，选择单元格格式，对齐方式，勾掉自动换行

10.

11.

12.

13.

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

&#8212;&#8212;&#8212;&#8212;-