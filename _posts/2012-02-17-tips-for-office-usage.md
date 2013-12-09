---
title: Hints for office usage
layout: post
categories:
  - office
  - excel
  - word
  - powerpoint
  - letter
tags:
  - office
  - excel
  - word
  - powerpoint
---



####Excel part

#####Excel functions

One main hint, if the formula you typed in does not work, please check if the data type in that column is `regular`.
如果公式不工作，先查看下数据类型是否为“常规”。


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

10. Check if a string contains a pattern (0 represents un-contain)
{% highlight bash%}
=IF(ISERROR(FIND("GUCC",K7)),0,FIND("GUCC",K7))
#ISERROR can be used at other positions when you do not like the returnned error things.
{% endhighlight %}

11.

12.

13.

#### Word part
1. word右边显示超出边界

<pre class="brush: bash; title: ; notranslate" title="">去页面设置把你的纸张方向改为横向，然后把表格的列调小，然后在把纸张方向调回来。
先在页面设置中把纸张改成大一号，如原来是16开，就改成8开。
这样表格就应该可以完全显示了，然后再设置表格的列宽，
把它调整到合适的大小，再到页面设置中把纸张调整成正常即可。</pre>

2.word中短行连成长行

<pre class="brush: bash; title: ; notranslate" title="">编辑 → 替换 查找内容：[^11^13]{1,}  高级 → √使用通配符 → 全部替换</pre>

3.word中不能使用搜狗拼音

<pre class="brush: bash; title: ; notranslate" title="">文件-选项-高级-输入法控制处于活动状态 【勾掉】
</pre>

#### PPT part
1.快速插入多张图片

插入&#8211;相册&#8211;新建相册&#8211;从文件；然后把新建好相册拷贝到正在工作的PPT中。

Or you can reference to [including many pics in pdf](http://tianxia-world.tk/2013/10/many-pics-included-in-pdf/).

2.字体修改

标题和正文中与模板相关的字体使用“母板视图”统一修改。

自己插入的文本框的字体，由“母板视图”&#8212;“字体”&#8212;“新建主题字体”修改。

“母板视图”&#8212;“插入&#8211;占位符”可以自定义文本域，如幻灯片底部的参考文献，便于统一修改。

3.表格中插入图片

选中单元格后，用边框与填充，选择图片。
