---
title: Latex使用beamer篇
author: 悟道
layout: post
permalink: /?p=1071
categories:
  - tex
tags:
  - beamer
  - latex
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.列模式下，两列顶端对齐

> \begin{columns}[t]
> 
> \begin{column}{0.5\textwidth}
> 
> \end{column}
> 
> \end{columns}

2.幻灯片一页的大小可伸缩

> \begin{frame}[shrink]

3.幻灯片标题页去掉导航条等东西

> \frame
> 
> \begin{frame}[t]  #上
> 
> \begin{frame}[b]  #下

6.改变表格的大小

> \resizebox{\textwidth}{!}{
> 
> \begin{tabular}
> 
> &#8230;&#8230;
> 
> \end{tabular}
> 
> }

7. 一个宏命令方便在幻灯片中插入图片

<div class="wp_codebox">
  <table>
    <tr id="p1071126">
      <td class="code" id="p1071code126">
        <pre class="latex" style="font-family:monospace;"><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cnewcommand"><span style="color: #800000;">newcommand</span></a> <span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #800000; font-weight: normal;">\framedgraphic</span></span><span style="color: #E02020; ">}[</span><span style="color: #C08020; font-weight: normal;">2</span><span style="color: #E02020; ">]</span> <span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">
    <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">#1</span><span style="color: #E02020; ">}</span>
        <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">center</span></span><span style="color: #E02020; ">}</span>
            <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cincludegraphics"><span style="color: #800000;">includegraphics</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">width=\<a href="http://www.golatex.de/wiki/index.php?title=%5Ctextwidth"><span style="color: #800000;">textwidth</span></a>, height=0.8<span style="color: #800000; font-weight: normal;">\textheight</span>,
               keepaspectratio</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">#2</span><span style="color: #E02020; ">}</span>
        <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">center</span></span><span style="color: #E02020; ">}</span>
    <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

8.生成文章中带有字母标记的图

<div class="wp_codebox">
  <table>
    <tr id="p1071127">
      <td class="code" id="p1071code127">
        <pre class="latex" style="font-family:monospace;"><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">article</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">graphicx</span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #2C922C; font-style: italic;">%this can be used to test this tex without needing the pictures.</span>
<span style="color: #2C922C; font-style: italic;">%\usepackage[demo]{graphicx} </span>
&nbsp;
<span style="color: #2C922C; font-style: italic;">%position=t --- put the label at top center</span>
<span style="color: #2C922C; font-style: italic;">%singlelinecheck=off --- put the label at top left</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">position=t, singlelinecheck=off</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">subfig</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">caption</span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Crenewcommand"><span style="color: #800000;">renewcommand</span></a><span style="color: #800000; font-weight: normal;">\thesubfigure</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #800000; font-weight: normal;">\Alph</span>{subfigure</span><span style="color: #E02020; ">}}</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">figure</span></span><span style="color: #E02020; ">}[</span><span style="color: #C08020; font-weight: normal;">!ht</span><span style="color: #E02020; ">]</span>
    <span style="color: #800000; font-weight: normal;">\captionsetup</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">subfigure</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">labelformat=simple</span><span style="color: #E02020; ">}</span>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ccentering"><span style="color: #800000;">centering</span></a>
    <span style="color: #800000; font-weight: normal;">\subfloat</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">]{<span style="color: #2020C0; font-weight: normal;">\<a href="http://www.golatex.de/wiki/index.php?title=%5Cincludegraphics"><span style="color: #800000;">includegraphics</span></a><span style="color: #E02020; ">[</span>width=0.9<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctextwidth"><span style="color: #800000;">textwidth</span></a></span>]{picture</span><span style="color: #E02020; ">}}</span> <span style="color: #800000; font-weight: normal;">\quad</span>
    <span style="color: #800000; font-weight: normal;">\subfloat</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">]{<span style="color: #2020C0; font-weight: normal;">\<a href="http://www.golatex.de/wiki/index.php?title=%5Cincludegraphics"><span style="color: #800000;">includegraphics</span></a><span style="color: #E02020; ">[</span>width=0.9<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctextwidth"><span style="color: #800000;">textwidth</span></a></span>]{picture</span><span style="color: #E02020; ">}}</span>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ccaption"><span style="color: #800000;">caption</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Caption about here</span><span style="color: #E02020; ">}</span>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Clabel"><span style="color: #800000;">label</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">fig:fig1</span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">figure</span></span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

[<img class="alignnone size-big wp-image-1157" title="amazing" src="http://210.75.224.29/wordpress/wp-content/uploads/2011/07/amazing-300x141.png" alt="" width="300" height="141" />][1]

9.A useful specification is just <0>, which causes the frame to have no slides at all. For example,  
\begin{frame}<handout:0> causes the frame to be suppressed in the handout version, but to be shown normally  
in all other versions.

&nbsp;

10.frame的其他选项

> [allowframebreaks] :  for automatic split of frames if the contents do not fit in a single slide.  [The other command \framebreak has similar functions and allows you to set the lines where the frame break][2]. Just add this command after the last line which will stays in this slide.
> 
> <pre>\documentclass{beamer} 
\begin{document} 
\begin{frame}[allowframebreaks]{Title} 
A\\ A\\ A\\ A\\ A\\ A \framebreak B\\ B\\ 
\framebreak 
B\\ B\\ \end{frame} \end{document}
</pre>
> 
> [containsverbatim} for using verbatim environment and \verb command
> 
> [squeeze] for squeezing vertical space.

11.beamer frame 使用todonotes   [[here][3]]

> \usepackage{todonotes}
> 
> \presetkeys{todonotes}{inline}{size=\tiny}{}
> 
> \todo{Your notes}

12.beamer frame 使用verbatim,listing，[参考][4]

> \begin{frame}[fragile]
> 
> \begin{verbatim} \end{verbatim}
> 
> \end{frame}

13.beamer中hyperlink添加颜色,[参考][5]

> \definecolor{links}{HTML}{2A1b81}
> 
> \hypersetup{colorlinks,linkcolor=,urlcolor=links}

14. \listfiles 列出使用到的包及其版本

15.设置幻灯片的边距[http://www.math.umbc.edu/~rouben/beamer/quickstart-Z-H-24.html#node\_sec\_24][6]

<pre>\setbeamersize{text margin left=6mm, text margin right=2mm}</pre>

16.幻灯片默认大小是5.04in x 3.78in，12.8016cm X 9.6012cm

17.设置角标，[http://www.math.umbc.edu/~rouben/beamer/quickstart-Z-H-17.html#node\_sec\_17][7]

<pre>\documentclass{beamer}
\usetheme{Madrid}
\usepackage[absolute,overlay]{textpos}
\newenvironment{reference}[2]{%
  \begin{textblock*}{\textwidth}(#1,#2)
      \footnotesize\it\bgroup\color{red!50!black}}{\egroup\end{textblock*}}
\begin{document}

\begin{frame}{Title}
   \begin{reference}{4mm}{85mm}
       V. Jikov, S. Kozlov and O. Olenik, Homogenization
       of differential operators and integral
       functionals, Springer, 1994.
   \end{reference} 

   This is a test.
\end{frame}
</pre>

\end{document}

18.

 [1]: http://210.75.224.29/wordpress/wp-content/uploads/2011/07/amazing.png
 [2]: http://tex.stackexchange.com/questions/13380/explicit-frame-break-with-beamer-class
 [3]: http://tex.stackexchange.com/questions/12328/how-can-i-use-todonotes-with-beamer
 [4]: http://heather.cs.ucdavis.edu/~matloff/beamer.html
 [5]: http://tes.stackexchange.com/questions/13423/how-to-color-fhef--links-in-beamer
 [6]: http://www.math.umbc.edu/~rouben/beamer/quickstart-Z-H-24.html#node_sec_24
 [7]: http://www.math.umbc.edu/~rouben/beamer/quickstart-Z-H-17.html#node_sec_17