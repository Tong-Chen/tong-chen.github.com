---
title: 采用beamer混编beamer和article
author: 悟道
layout: post
permalink: /?p=1905
categories:
  - tex
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.宏转换，参考<http://tex.stackexchange.com/questions/39362/changing-standard-output-presentation-page-size-into-a4-size>

<div class="wp_codebox">
  <table>
    <tr id="p1905153">
      <td class="code" id="p1905code153">
        <pre class="latex" style="font-family:monospace;"><span style="color: #800000; font-weight: normal;">\newif</span><span style="color: #800000; font-weight: normal;">\ifmybeamer</span>
<span style="color: #2C922C; font-style: italic;">%\mybeamertrue  #when commented out, article output. else beamer output</span>
<span style="color: #800000; font-weight: normal;">\ifmybeamer</span>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">Madrid</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">beamer</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Celse"><span style="color: #800000;">else</span></a>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">article</span><span style="color: #E02020; ">}</span>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">beamerarticle</span><span style="color: #E02020; ">}</span>
&nbsp;
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cmakeatletter"><span style="color: #800000;">makeatletter</span></a>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdef"><span style="color: #800000;">def</span></a><span style="color: #800000; font-weight: normal;">\frametitle</span><span style="color: #E02020; ">{</span><span style="color: #2C922C; font-style: italic;">%</span>
        <span style="color: #E00000; font-weight: normal;">\@ifnextchar</span>&lt;<span style="color: #2C922C; font-style: italic;">%</span>
            <span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E00000; font-weight: normal;">\@frametitle</span>@lt</span><span style="color: #E02020; ">}</span><span style="color: #2C922C; font-style: italic;">%</span>
            <span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E00000; font-weight: normal;">\@frametitle</span>@lt&lt;&gt;</span><span style="color: #E02020; ">}</span><span style="color: #2C922C; font-style: italic;">%</span>
    <span style="color: #E02020; ">}</span>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdef"><span style="color: #800000;">def</span></a><span style="color: #E00000; font-weight: normal;">\@frametitle</span>@lt&lt;#1&gt;#2<span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}</span>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cmakeatother"><span style="color: #800000;">makeatother</span></a>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cfi"><span style="color: #800000;">fi</span></a>
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cauthor"><span style="color: #800000;">author</span></a>{Me</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctitle"><span style="color: #800000;">title</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Beamer Tricks</span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}</span>
   <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cmaketitle"><span style="color: #800000;">maketitle</span></a>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}</span><span style="color: #2C922C; font-style: italic;">%</span>
   <span style="color: #800000; font-weight: normal;">\frametitle</span>&lt;notes&gt;<span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Hi</span><span style="color: #E02020; ">}</span>
   Hello
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

2.多文件，参考<http://mathoverflow.net/questions/5893/beamer-printout>

<div class="wp_codebox">
  <table>
    <tr id="p1905154">
      <td class="code" id="p1905code154">
        <pre class="latex" style="font-family:monospace;">It's possible to change the type of the output (between beamer, handout, trans, or article) without modifying the file. The trick is to put the main document in one file, say geometry.tex but without the documentclass declaration. Then you create a new file for each type with just the documentclass declaration. For example, geometry.beamer.tex could contain:
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">12pt,t,xcolor=dvipsnames,ignorenonframetext</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">beamer</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cinput"><span style="color: #800000;">input</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">geometry.tex</span><span style="color: #E02020; ">}</span>
&nbsp;
whilst geometry.handout.tex might contain
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">[</span>12pt,xcolor=dvipsname,ignorenonframetext,handout,<span style="color: #2C922C; font-style: italic;">%</span>
 notes=only<span style="color: #2C922C; font-style: italic;">%</span>
<span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">beamer</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cinput"><span style="color: #800000;">input</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">geometry.tex</span><span style="color: #E02020; ">}</span>
&nbsp;
and geometry.article.tex might be
&nbsp;
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">a4paper,10pt</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">article</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">envcountsect</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">beamerarticle</span><span style="color: #E02020; ">}</span>
<span style="color: #800000; font-weight: normal;">\setjobnamebeamerversion</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">geometry.beamer</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cinput"><span style="color: #800000;">input</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">geometry.tex</span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>