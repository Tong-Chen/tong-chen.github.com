---
title: Latex绘制表格
author: 悟道
layout: post
permalink: /?p=570
categories:
  - tex
tags:
  - latex
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

LaTeX 中经常会碰到绘制表格.

下面通过一个例子来体会 LaTeX 的表格功能 .

<div class="wp_codebox">
  <table>
    <tr id="p57039">
      <td class="code" id="p570code39">
        <pre class="latex" style="font-family:monospace;"><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">article</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">multirow</span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span>
LaTeX table example<span style="color: #E02020; ">\\</span>
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">table</span></span><span style="color: #E02020; ">}[</span><span style="color: #C08020; font-weight: normal;">!hbp</span><span style="color: #E02020; ">]</span>
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tabular</span></span><span style="color: #E02020; ">}{</span><span style="color: #E02020; "><span style="color: #2020C0; font-weight: normal;">|c|c|c|c|c|</span></span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
lable 1-1 <span style="color: #E02020; ">&</span> label 1-2 <span style="color: #E02020; ">&</span> label 1-3 <span style="color: #E02020; ">&</span> label 1 -4 <span style="color: #E02020; ">&</span> label 1-5 <span style="color: #E02020; ">\\</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
label 2-1 <span style="color: #E02020; ">&</span> label 2-2 <span style="color: #E02020; ">&</span> label 3-3 <span style="color: #E02020; ">&</span> label 4-4 <span style="color: #E02020; ">&</span> label 5-5 <span style="color: #E02020; ">\\</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
<span style="color: #800000; font-weight: normal;">\multirow</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">*</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Multi-Row</span><span style="color: #E02020; ">}</span> <span style="color: #E02020; ">&</span> <span style="color: #800000; font-weight: normal;">\multicolumn</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2</span><span style="color: #E02020; ">}{</span><span style="color: #E02020; "><span style="color: #2020C0; font-weight: normal;">|c|</span></span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Multi-Column</span><span style="color: #E02020; ">}</span> <span style="color: #E02020; ">&</span> <span style="color: #800000; font-weight: normal;">\multicolumn</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2</span><span style="color: #E02020; ">}{</span><span style="color: #E02020; "><span style="color: #2020C0; font-weight: normal;">|c|</span></span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #800000; font-weight: normal;">\multirow</span>{2</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">*</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Multi-Row and Col</span><span style="color: #E02020; ">}}</span> <span style="color: #E02020; ">\\</span>
<span style="color: #800000; font-weight: normal;">\cline</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2-3</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">&</span> column-1 <span style="color: #E02020; ">&</span> column-2 <span style="color: #E02020; ">&</span> <span style="color: #800000; font-weight: normal;">\multicolumn</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2</span><span style="color: #E02020; ">}{</span><span style="color: #E02020; "><span style="color: #2020C0; font-weight: normal;">|c|</span></span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}\\</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
<span style="color: #800000; font-weight: normal;">\multirow</span>{3</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">*</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Multi-Row</span><span style="color: #E02020; ">}</span> <span style="color: #E02020; ">&</span> 1 <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #E02020; ">&</span> 1 <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #E02020; ">&</span> 1 <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
<span style="color: #800000; font-weight: normal;">\multirow</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">4</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">*</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Multi-Row</span><span style="color: #E02020; ">}</span> <span style="color: #E02020; ">&</span> <span style="color: #800000; font-weight: normal;">\multirow</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">*</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Multi too</span><span style="color: #E02020; ">}</span> <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #800000; font-weight: normal;">\cline</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">3-5</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">&</span> <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #800000; font-weight: normal;">\cline</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">3-5</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">&</span> <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #800000; font-weight: normal;">\cline</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2-5</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">&</span> <span style="color: #800000; font-weight: normal;">\multirow</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">*</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Multi also</span><span style="color: #E02020; ">}</span> <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #800000; font-weight: normal;">\cline</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">3-5</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">&</span> <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #800000; font-weight: normal;">\cline</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">3-5</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">&</span> <span style="color: #E02020; ">&</span> 2 <span style="color: #E02020; ">&</span> 3 <span style="color: #E02020; ">&</span> 4<span style="color: #E02020; ">\\</span>
<span style="color: #800000; font-weight: normal;">\cline</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">1-5</span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tabular</span></span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ccaption"><span style="color: #800000;">caption</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">My first table</span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">table</span></span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

保存, 编译, 看看是什么样子, 下面来解释.

\documentclass{article}%开始文档

\usepackage{multirow}%使用多栏宏包

\begin{document}%开始文档

LaTeX table example\\

\begin{table}[!hbp]%开始表格*【可以不用】*

<span style="color: #ff6600;">%其中参数[!hbp] 的意思是:</span>

<span style="color: #ff6600;">%! 表示尽可能的尝试, h (here) 当前位置显示表格,</span>

<span style="color: #ff6600;">%如果实在不行显示在 b (bottom)底部.</span>

\begin{tabular}{|c|c|c|c|c|}%开始绘制表格

% {|c|c|c|c|c|} 表示会有5列, 每个的方式未居中(c),

%也可以改成靠左(l)和靠右(r) 其中 | 表示绘制列线

\hline %绘制一条水平的线

\hline %再绘制一条水平的线

lable 1-1 & label 1-2 & label 1-3 & label 1 -4 & label 1-5 \\

%这事表格的第一行, 其中5个元素, 用 &隔开.

\hline

label 2-1 & label 2-2 & label 3-3 & label 4-4 & label 5-5 \\

%这事表格的第二行, 其中5个元素, 用 &隔开.

\hline

%下面这一段有点复杂, 参加后面的解释, 可以自己修改慢慢体会.

\multirow{2}{\*}{Multi-Row} & \multicolumn{2}{|c|}{Multi-Column} & \multicolumn{2}{|c|}{\multirow{2}{\*}{Multi-Row and Col}} \\

%**上面开始两行合并, 然后又是正常的两列合并, 接下来是两行两列合并**

\cline{2-3} %绘制第2列和第3列的横线

& column-1 & column-2 & \multicolumn{2}{|c|}{}\\

%补偿上面的两列合并的那一行

\hline %

\end{tabular}

\caption{My first table} %表格的名称

\end{table}

\end{document}

其中，multirow{2}{\*}{text}的第一个参数表示行的数目，\*表示由系统自动调整文字，text表示要写入的文字

multicolumn与multicolumn类似，功能是跨多列， \multicolumn{2}{|c|}{text}表示跨2行，文字采用中心对齐的方式，text是要写入的文字。

multicolumn和multirow可以组合使用，跨多行多列，只需要将multirow作为multicolumn的text即可。

最后，\cline用于画横线 \cline{i-j}表示从第i列画到第j列.

[<img class="alignnone size-full wp-image-678" title="table" src="http://210.75.224.29/wordpress/wp-content/uploads/2010/12/table.png" alt="" width="579" height="442" />][1]

其它内容详见<http://en.wikibooks.org/wiki/LaTeX/Tables>

&nbsp;

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

\multirow{2}{3cm}{text} 可以设定宽度，[参见][2]

&nbsp;

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

再附一个复杂的例子：

> \begin{table}[!h]\footnotesize  
> \centering  
> \begin{tabular}{|l|l|l|l|l|l|l|l|l|l|}  
> \cline{1-3}  
> \multicolumn{2}{|c|}{Cell type} & F14-6  
> &\multicolumn{7}{l}{} \\  
> \cline{1-4}  
> \multirow{4}{\*}{ES} & \multirow{2}{\*}{F14-6} &  
> \multirow{2}{*}{15809}  
> &\multirow{2}{*}{cL11}  
> &\multicolumn{6}{l}{\multirow{2}{*}{}} \\  
> & & &  
> & \multicolumn{6}{l}{} \\  
> \cline{2-5}  
> &\multirow{2}{\*}{cL11} & \red{2444} & \multirow{2}{\*}{16101}  
> &\multirow{2}{*}{2-3-3}  
> &\multicolumn{5}{l}{\multirow{2}{*}{}} \\  
> \cline{3-3}  
> & & \blue{1923} & &  
> &\multicolumn{5}{l}{}\\  
> \cline{1-6}  
> \multirow{4}{\*}{2N ips} & \multirow{2}{\*}{2-3-3} & \red{2904} &  
> \red{2514} & \multirow{2}{*}{15959}  
> &\multirow{2}{*}{5-13}  
> &\multicolumn{4}{l}{\multirow{2}{*}{}} \\  
> \cline{3-4}  
> & & \blue{2556} & \blue{2952} & &  
> &\multicolumn{4}{l}{}\\  
> \cline{2-7}  
> & \multirow{2}{*}{5-13} & \red{2308} & \cellcolor[gray]{0.9}\red{1852} & \red{1943} &  
> \multirow{2}{*}{15681}  
> &\multirow{2}{*}{10-1-1}  
> &\multicolumn{3}{l}{\multirow{2}{*}{}} \\  
> \cline{3-5}  
> & & \blue{2991} & \cellcolor[gray]{0.9}\blue{3380} & \blue{2626} & &  
> &\multicolumn{3}{l}{}\\  
> \cline{1-8}  
> \multirow{8}{\*}{4N ips} & \multirow{2}{\*}{10-1-1} & \red{2349} &  
> \cellcolor[gray]{0.9}\red{1907} & \red{1976} & \red{2316}  
> &\multirow{2}{*}{16011}  
> &\multirow{2}{*}{14-2-2}  
> &\multicolumn{2}{l}{\multirow{2}{*}{}} \\  
> \cline{3-6}  
> & & \blue{2650} & \cellcolor[gray]{0.9}\blue{3024} & \blue{2342} & \blue{1722} & &  
> &\multicolumn{2}{l}{}\\  
> \cline{2-9}  
> & \multirow{2}{*}{14-2-2} & \cellcolor[gray]{0.9}\red{1884} & \cellcolor[gray]{0.9}\red{1790} & \cellcolor[gray]{0.9}\red{1637} &  
> \red{1889} & \red{1473} & \multirow{2}{*}{15457}  
> &\multirow{2}{*}{27-3-5}  
> &\multicolumn{1}{l}{\multirow{2}{*}{}}\\  
> \cline{3-7}  
> & & \cellcolor[gray]{0.9}\blue{3188} & \cellcolor[gray]{0.9}\blue{3490} & \cellcolor[gray]{0.9}\blue{3329} & \blue{2555} &  
> \blue{2553} & &  
> &\multicolumn{1}{l}{}\\  
> \cline{2-10}  
> & \multirow{2}{*}{27-3-5} & \red{2624} & \red{2350} & \red{2429}  
> & \red{2816} & \red{2260} & \cellcolor[gray]{0.9}\red{3217} & \multirow{2}{*}{16107}  
> &\multirow{2}{*}{33-2-5} \\  
> \cline{3-8}  
> & & \blue{2187} & \blue{2660} & \blue{2117} & \blue{1959} &  
> \blue{1782} & \cellcolor[gray]{0.9}\blue{1469} &  
> & \\  
> \cline{2-10}  
> &\multirow{2}{*}{33-2-5} & \cellcolor[gray]{0.9}\red{2775} & \red{2366} & \red{2802} &  
> \cellcolor[gray]{0.9}\red{3414} & \cellcolor[gray]{0.9}\red{2929} & \cellcolor[gray]{0.9}  
> \red{3804} & \red{2438} &  
> \multirow{2}{*}{16106} \\  
> \cline{3-9}  
> & & \cellcolor[gray]{0.9}\blue{1777} & \blue{2104} & \blue{2285} & \cellcolor[gray]{0.9}\blue{1848} &  
> \cellcolor[gray]{0.9}\blue{1730} & \cellcolor[gray]{0.9}\blue{1441} & \blue{2068} & \\  
> \hline  
> \end{tabular}  
> \caption{Summary of DE genes among 8 samples. \\Black numbers  
> represent the amount of genes expressed in the left cell line.  
> Red ones indicate the count of genes up-regulated in the left cell  
> line when comparing with the top cell line. Blue ones mean  
> opposite.\\  
> Gray background indicates the disparity between up and  
> down-regulated genes.}  
> \label{de.gene}  
> \end{table}

[<img class=" wp-image-1956 alignleft" title="table" src="http://210.75.224.29/wordpress/wp-content/uploads/2010/12/table1.png" alt="" width="417" height="263" />][3]

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

&nbsp;

 [1]: http://210.75.224.29/wordpress/wp-content/uploads/2010/12/table.png
 [2]: http://tex.stackexchange.com/questions/2441/how-to-add-a-forced-line-break-inside-a-table-cell
 [3]: http://210.75.224.29/wordpress/wp-content/uploads/2010/12/table1.png