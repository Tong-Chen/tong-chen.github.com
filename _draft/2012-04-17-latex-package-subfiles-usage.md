---
title: latex package subfiles usage
author: 悟道
layout: post
permalink: /?p=2013
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

The questions solved:

1.Main file and child file can have their own title, author, date information.

2.The content page do not appear in main file.

3.Natbib can be called in main file and child file separately except renamed. 

&#8212;&#8212;&#8212;&#8212;&#8211;The main file&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

<div class="wp_codebox">
  <table>
    <tr id="p2013157">
      <td class="code" id="p2013code157">
        <pre class="latex" style="font-family:monospace;"><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">a4paper, 12pt</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">article</span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">/home/CT/server/texmf/CtArticle</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">subfiles</span><span style="color: #E02020; ">}</span>
<span style="color: #2C922C; font-style: italic;">%\usepackage{standalone}</span>
<span style="color: #2C922C; font-style: italic;">%\graphicspath{{DNED/}}</span>
&nbsp;
<span style="color: #2C922C; font-style: italic;">%\newif\ifmultiple  %\multipletrue means called by main file</span>
<span style="color: #2C922C; font-style: italic;">%\multipletrue</span>
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Clet"><span style="color: #800000;">let</span></a><span style="color: #800000; font-weight: normal;">\ctbibliography</span><span style="color: #800000; font-weight: normal;">\bibliography</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Clet"><span style="color: #800000;">let</span></a><span style="color: #800000; font-weight: normal;">\ctbibliographystyle</span><span style="color: #800000; font-weight: normal;">\bibliographystyle</span>
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cauthor"><span style="color: #800000;">author</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #800000; font-weight: normal;">\href</span><span style="color: #E02020; ">{</span>mailto:chentong<span style="color: #800000; font-weight: normal;">\_</span>biology@163.com</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Chen Tong</span><span style="color: #E02020; ">}}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctitle"><span style="color: #800000;">title</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">main</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdate"><span style="color: #800000;">date</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">\<a href="http://www.golatex.de/wiki/index.php?title=%5Ctoday"><span style="color: #800000;">today</span></a></span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cmaketitle"><span style="color: #800000;">maketitle</span></a>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdef"><span style="color: #800000;">def</span></a><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cauthor"><span style="color: #800000;">author</span></a>#1<span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdef"><span style="color: #800000;">def</span></a><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctitle"><span style="color: #800000;">title</span></a>#1{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdef"><span style="color: #800000;">def</span></a><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdate"><span style="color: #800000;">date</span></a>#1{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdef"><span style="color: #800000;">def</span></a><span style="color: #800000; font-weight: normal;">\ctbibliographystyle</span>#1{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdef"><span style="color: #800000;">def</span></a><span style="color: #800000; font-weight: normal;">\ctbibliography</span>#1{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctableofcontents"><span style="color: #800000;">tableofcontents</span></a>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Clet"><span style="color: #800000;">let</span></a><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctableofcontents"><span style="color: #800000;">tableofcontents</span></a><span style="color: #800000; font-weight: normal;">\relax</span>
<span style="color: #800000; font-weight: normal;">\clearpage</span>
&nbsp;
&nbsp;
<span style="color: #800000; font-weight: normal;">\subfile</span>{child</span><span style="color: #E02020; ">}</span>
&nbsp;
&nbsp;
<span style="color: #800000; font-weight: normal;">\bibliographystyle</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">cell</span><span style="color: #E02020; ">}</span>    <span style="color: #2C922C; font-style: italic;">% (uses file ``plain.bst'')</span>
<span style="color: #800000; font-weight: normal;">\bibliography</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">all</span><span style="color: #E02020; ">}</span>            <span style="color: #2C922C; font-style: italic;">% expects file ``ref.bib''</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

&#8212;&#8212;-The child file&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

<div class="wp_codebox">
  <table>
    <tr id="p2013158">
      <td class="code" id="p2013code158">
        <pre class="latex" style="font-family:monospace;"><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">main.tex</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">subfiles</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cgraphicspath"><span style="color: #800000;">graphicspath</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">{mmp/</span><span style="color: #E02020; ">}}</span>
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cauthor"><span style="color: #800000;">author</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #800000; font-weight: normal;">\href</span><span style="color: #E02020; ">{</span>mailto:chentong<span style="color: #800000; font-weight: normal;">\_</span>biology@163.com</span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">Chen Tong</span><span style="color: #E02020; ">}}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctitle"><span style="color: #800000;">title</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">child</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdate"><span style="color: #800000;">date</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">\<a href="http://www.golatex.de/wiki/index.php?title=%5Ctoday"><span style="color: #800000;">today</span></a></span><span style="color: #E02020; ">}</span>
&nbsp;
&nbsp;
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cmaketitle"><span style="color: #800000;">maketitle</span></a>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctableofcontents"><span style="color: #800000;">tableofcontents</span></a>
<span style="color: #800000; font-weight: normal;">\clearpage</span>
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Csection"><span style="color: #800000;">section</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">ccc</span><span style="color: #E02020; ">}</span>
&nbsp;
&nbsp;
<span style="color: #800000; font-weight: normal;">\ctbibliographystyle</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">cell</span><span style="color: #E02020; ">}</span>    <span style="color: #2C922C; font-style: italic;">% (uses file ``plain.bst'')</span>
<span style="color: #800000; font-weight: normal;">\ctbibliography</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">child</span><span style="color: #E02020; ">}</span>             <span style="color: #2C922C; font-style: italic;">% expects file ``ref.bib''</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;End &#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;