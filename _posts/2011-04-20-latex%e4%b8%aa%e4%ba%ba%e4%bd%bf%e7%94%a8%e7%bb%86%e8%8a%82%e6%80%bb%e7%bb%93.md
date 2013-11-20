---
title: LaTex个人使用细节总结
author: 悟道
layout: post
permalink: /?p=855
categories:
  - tex
tags:
  - latex
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.文字下标(subscript) 和上标，科学记数法

<div class="wp_codebox">
  <table>
    <tr id="p85564">
      <td class="code" id="p855code64">
        <pre class="latex" style="font-family:monospace;">P<span style="color: #8020E0; font-weight: normal;">$_Y$</span>
10<span style="color: #8020E0; font-weight: normal;">$<span style="color: #800000; font-weight: normal;">\times</span>$</span>10<span style="color: #8020E0; font-weight: normal;">$^{<span style="color: #2020C0; font-weight: normal;">9</span>}$</span></pre>
      </td>
    </tr>
  </table>
</div>

<div class="wp_codebox">
  <table>
    <tr id="p85565">
      <td class="code" id="p855code65">
        <pre class="latex" style="font-family:monospace;">1<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctextsuperscript"><span style="color: #800000;">textsuperscript</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">st</span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

2.斜体(Italic)

<div class="wp_codebox">
  <table>
    <tr id="p85566">
      <td class="code" id="p855code66">
        <pre class="latex" style="font-family:monospace;"><span style="color: #800000; font-weight: normal;">\it</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">P<span style="color: #8020E0; font-weight: normal;">$_Y$</span></span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

3.单双引号，使用键盘的 Tab键上侧的连续键入两个&#8220;然后输入键盘的两个单引号‘’，这样可以得到双引号。一个\`加一个‘，得到单引号。

<div class="wp_codebox">
  <table>
    <tr id="p85567">
      <td class="code" id="p855code67">
        <pre class="latex" style="font-family:monospace;">``double quote''.   `single quote'</pre>
      </td>
    </tr>
  </table>
</div>

4.大于，小于，小于等于，大于等于，不等于

<div class="wp_codebox">
  <table>
    <tr id="p85568">
      <td class="code" id="p855code68">
        <pre class="latex" style="font-family:monospace;"><span style="color: #8020E0; font-weight: normal;">$3 <span style="color: #800000; font-weight: normal;">\lt</span> 4$</span>
<span style="color: #8020E0; font-weight: normal;">$4 <span style="color: #800000; font-weight: normal;">\gt</span> 3$</span>
<span style="color: #8020E0; font-weight: normal;">$4 <span style="color: #800000; font-weight: normal;">\geq</span> 3$</span>
<span style="color: #8020E0; font-weight: normal;">$3 <span style="color: #800000; font-weight: normal;">\leq</span> 4$</span>
<span style="color: #8020E0; font-weight: normal;">$4 <span style="color: #800000; font-weight: normal;">\neq</span> 3$</span></pre>
      </td>
    </tr>
  </table>
</div>

5.行间距，段间距

> \renewcommand{\baselinestretch}{1.2} %1.2倍行间距  
> \addtolength{\parskip}{\baselineskip} %段间距To increase \parskip to skip a line between paragraphs

6.列表调整

> \setlength{\leftmargin}{1.2em} %左边界  
> \setlength{\parsep}{0ex} %段落间距  
> \setlength{\topsep}{1ex} %列表到上下文的垂直距离  
> \setlength{\itemsep}{0.5ex} %条目间距  
> \setlength{\labelsep}{0.3em} %标号和列表项之间的距离,默认0.5em  
> \setlength{\itemindent}{1.1em} %标签缩进量  
> \setlength{\listparindent}{0em} %段落缩进量

7.\bigskip , \medskip, \smallskip

8.eps图形插入，编译方式,(epstopdf可直接转换eps为pdf格式)

> latex file.tex
> 
> dvipdf file.dvi
> 
> dvipdf -dAutoRotatePages=/None file.dvi（防止插入eps图形导致的页面旋转）

9.subfile可以处理多个tex文件组成的文档，既可以统一编译，也可以各自编译。

> \usepackage{subfiles} 主文件
> 
> \subfile{filename} 主文件
> 
> \documentclass[rootdoc.tex]{subfiles} 子文件
> 
> \include{file} 不能嵌套，自动分页，配合\includeonly
> 
> \input{file.tex} 可以嵌套，不分页

10.表格添加标题，缩小字体，添加标签(h指示表格位置here，!表示重写系统命令)，脚注见[here][1]

> \begin{table}[h!]\footnotesize
> 
> \caption{}
> 
> \begin{tabular}
> 
> \end{tabular}
> 
> \label{table1}
> 
> \end{table}

11.figure环境下，label必须在caption的后面， 一个更安全的方式如下

> \caption{sdskdjfsjkd\label{}}
> 
> &nbsp;

12.scetion后面第一段不缩进，在每个第一段前面加上\noindent.

13.参考文献不使用悬挂缩进

> \setlength \bibhang{0em}
> 
> \setlength \bibsep{0pt} 设定两个参考文献之间的距离
> 
> \renewcommand{\bibfont}{\small} 设定参考文献的字体大小

14.使用Time New Roman字体

> \usepackage{times}

15.手动指定fontsize

> \newcommand{\sixteen}{\fontsize{26pt}{\baselineskip}\selectfont}
> 
> {\sixteen 16pt fonts}
> 
> {\small small}
> 
> \tiny  
> \scriptsize  
> \footnotesize  
> \small  
> \normalsize  
> \large  
> \Large  
> \LARGE  
> \huge  
> \Huge

16.对齐

> \leftline{一行文字左对齐}   (\centering{} \rightline{})
> 
> \begin{flushleft}\end{flushleft}  一段文字左对齐  （center, flushright）

17. \\[3.5cm]  产生3.5cm的空白    \vfill   \hfill 填充空白以布满整页或一行

> &nbsp;

18.调整itemize内容的字体[[more][2]]

> \small
> 
> \begin{itemize}
> 
> \end{itemize}
> 
> &nbsp;

19.latex加入参考文献后的编译步骤

> latex manuscript.tex
> 
> bibtex manuscript.aux
> 
> latex manuscript.tex
> 
> latex manuscript.tex

20.elsarticle模板的使用，修改natbib的参数， 参见[here][3]

> \documentclass[authoryear,preprint,review,12pt,**square,comma**]{elsarticle}

21.给参考文献加上超链接

> \usepackage{hyperref}
> 
> \usepackage[colorlinks,linkcolor=red,anchorcolor=blue,citecolor=green]{hyperref} # 给超链接加上颜色取代默认的方框
> 
> %\href{url}{text}

22.字体颜色

> \usepackage{color}
> 
> {\color{blue}blue things}

23.item标题行后换行

> \item title \hfill \\

24.description使用, 注意是方括号，在article中使用参考<http://tex.stackexchange.com/questions/23207/beamer-like-description-environment>

> \begin{description}
> 
> \item [desc] Things
> 
> \end{description}

25.latex直接显示文字，不做编译

> \begin{verbatim} \ldots \end{verbatim}     #output   \ldots
> 
> \begin{verbatim*} \ldots    \ldots \  \end{verbatim}  # output  \ldots    \ldots  # space is labeled
> 
> The \verb|ldots| command   #output    The \ldots command
> 
> \begin{quote}    \end{quote}   #suitable for paragraphs, allowing indent
> 
> \begin{verse}    \end{verse}    #suitable for poets, allows using // at the end of the line

26.todonote使用

> \usepackage{todonotes}  
> \presetkeys{todonotes}{inline}{size=\tiny}{}

27.item项后换行

> \item {item name} \hfill \\

28.水平或垂直填充

> \vfill \hfill

29.正负号

> $\pm$

30.超链接中有井号，错误信息为Illegal parameter number in definition of \test，解决方式是\#.[参见][4]

31.调整erbatim中字体的大小

> \begin{verbatim}
> 
> \huge
> 
> \end{verbatim}
> 
> {\tiny
> 
> \begin{verbatim}
> 
> \end{verbatim}
> 
> }

32.latex定义subsubsubsection

http://www.latex-community.org/forum/viewtopic.php?f=5&#038;t=791

32.protect  http://people.csail.mit.edu/jrennie/latex/

33.Option clash&#8221; error

> If you want to give some speci c options to some packages, you  
> have to load them before the todonotes package or other package which load them by default parameters, otherwise you will get an &#8220;Option clash&#8221; error when latex works on the document.

34.latex 表格标题左对齐 [tex.stackexchange.com/questions/3176/how-can-i-left-align-a-caption][5]

> \usepackage[justification=jstified, singlelinecheck=false]{caption}
> 
> if subfig used,
> 
> \captionsetup{labelformat=simple, labelsep=period, textfont=footnotesize,  
> labelfont=sl, font=small, justification=justified,  
> singlelinecheck=false}

35.longtable使用footnotesize，并且不改变标题大小<tex.stackexchange.com/questions/44263/how-to-use-footnotesize-with-longtable-command>  <http://tex.stackexchange.com/questions/22730/how-to-change-font-size-of-longtable-lines-without-changing-font-size-of-caption>

>     {\footnotesize \begin{longtable}{lll} <data> \end{longtable}} 

36.图形或表格不浮动<http://tex.stackexchange.com/questions/8625/force-figure-placement-in-text>

> \usepackage{float}
> 
> \begin{figure}[H]
> 
> \end{figure}

37.http://dcwww.fys.dtu.dk/~schiotz/comp/LatexTips/LatexTips.html

38.Rotate words

> \usepackage{rotating}
> 
> \begin{sideways}Words\end{sideways}
> 
> http://andrewjpage.com/index.php?/archives/24-Latex-tables-and-rotated-text.html

39.

40.

41.

42.

43.

44.

45.

LaTeX会对表格或者图片的标题命令\caption{}中使用引用非常严苛（另外，section命令中使用脚注也是类似），可以把\protect命令放在命令前来修正。  
如：  
\caption{Data taken from \protect \cite{Efron79t}}  
\section{data taken from \protect \footnote{the email of author}}

&nbsp;

33.

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-未使用过的&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;  
1.\\[\*]，\*为指定的行间距。  
mbox{文本}可以将文本保持在同一行内。数学模式中一般以此加入中文。而且mbox里也可以出现数学模式。  
2.脚注  
在不能使用脚注的环境（数学模式、表格、盒子等）中，可以先声明一个脚注标记\footnotemark，在禁止模式外再加入脚注文本\footnotetext{脚注文本}。

3._{}    下标  
^{}     上标  
$ $   中间即是公式符号  
$ $   $ $   公式符号居中  
\vert 竖线  
\rangle 右方括弧  
\langle 左方括弧  
\frac{}{} 分数，前面是分子，后面是分母  
\sqrt{}   根号  
\left( \right) 完美括弧

 [1]: http://210.75.224.29/wordpress/?p=981
 [2]: http://tex.stackexchange.com/questions/10715/custom-font-size-for-itemize
 [3]: http://hi.baidu.com/bittnt/blog/item/6e5ee11349989433dc5401a8.html
 [4]: http://tex.stackexchange.com/questions/44738/hash-tag-in-href-causes-error
 [5]: tex.stackexchange.com/questions/3176/how-can-i-left-align-a-caption "tex.stackexchange.com/questions/3176/how-can-i-left-align-a-caption"