---
title: Latex beamer frame
author: 悟道
layout: post
permalink: /?p=1504
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

<div class="wp_codebox">
  <table>
    <tr id="p1504146">
      <td class="code" id="p1504code146">
        <pre class="latex" style="font-family:monospace;"><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">/home/user/tex/CtBeamer</span><span style="color: #E02020; ">}</span>
<span style="color: #2C922C; font-style: italic;">%</span>
<span style="color: #2C922C; font-style: italic;">% The following info should normally be given in you main file:</span>
<span style="color: #2C922C; font-style: italic;">%</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ctitle"><span style="color: #800000;">title</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">miRNA</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">microRNA</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Csubtitle"><span style="color: #800000;">subtitle</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cauthor"><span style="color: #800000;">author</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">Chen Tong</span>]{Chen Tong</span><span style="color: #E02020; ">}</span>
<span style="color: #800000; font-weight: normal;">\institute</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">Wang's lab</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">Omics lab, IGDB, CAS</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdate"><span style="color: #800000;">date</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">\<a href="http://www.golatex.de/wiki/index.php?title=%5Ctoday"><span style="color: #800000;">today</span></a></span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Csubject"><span style="color: #800000;">subject</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">miRNA</span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #800000; font-weight: normal;">\frame</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">plain</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #800000; font-weight: normal;">\titlepage</span></span><span style="color: #E02020; ">}</span> <span style="color: #2C922C; font-style: italic;">%delete the navagation bar at first page</span>
&nbsp;
<span style="color: #2C922C; font-style: italic;">%\AtBeginSection[]</span>
<span style="color: #2C922C; font-style: italic;">%{</span>
<span style="color: #2C922C; font-style: italic;">%  \begin{frame}</span>
<span style="color: #2C922C; font-style: italic;">%	\frametitle{Outline}</span>
<span style="color: #2C922C; font-style: italic;">%	\tableofcontents[current]</span>
<span style="color: #2C922C; font-style: italic;">%  \end{frame}</span>
<span style="color: #2C922C; font-style: italic;">%}</span>
&nbsp;
<span style="color: #800000; font-weight: normal;">\part</span>
<span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Main Talk</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Csection"><span style="color: #800000;">section</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Introduction</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Csubsection"><span style="color: #800000;">subsection</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Discovery</span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}[</span><span style="color: #C08020; font-weight: normal;">allowframebreak</span><span style="color: #E02020; ">]</span>
  <span style="color: #800000; font-weight: normal;">\frametitle</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Title</span><span style="color: #E02020; ">}</span>
  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">exampleblock</span></span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">block title</span><span style="color: #E02020; ">}</span>
  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">enumerate</span></span><span style="color: #E02020; ">}</span>
	<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Citem"><span style="color: #800000;">item</span></a> item<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cfootnote"><span style="color: #800000;">footnote</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">foornote</span><span style="color: #E02020; ">}</span>
	  <span style="color: #800000; font-weight: normal;">\small</span>
	  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">itemize</span></span><span style="color: #E02020; ">}</span>
		<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Citem"><span style="color: #800000;">item</span></a> <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cemph"><span style="color: #800000;">emph</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">it</span><span style="color: #E02020; ">}</span>em
	  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">itemize</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">enumerate</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">exampleblock</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #800000; font-weight: normal;">\framebreak</span>
  <span style="color: #800000; font-weight: normal;">\todo</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Things recorded</span><span style="color: #E02020; ">}</span>
  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">columns</span></span><span style="color: #E02020; ">}[</span><span style="color: #C08020; font-weight: normal;">t</span><span style="color: #E02020; ">]</span>
	<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">column</span></span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">0.5\<a href="http://www.golatex.de/wiki/index.php?title=%5Ctextwidth"><span style="color: #800000;">textwidth</span></a></span><span style="color: #E02020; ">}</span>
	  Title
	  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">table</span></span><span style="color: #E02020; ">}</span><span style="color: #800000; font-weight: normal;">\footnotesize</span>
	  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tabular</span></span><span style="color: #E02020; ">}{</span><span style="color: #E02020; "><span style="color: #2020C0; font-weight: normal;">|c|l|r|</span></span><span style="color: #E02020; ">}</span>
	  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tabular</span></span><span style="color: #E02020; ">}</span>
	  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">table</span></span><span style="color: #E02020; ">}</span>
	<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">column</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">columns</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #800000; font-weight: normal;">\note</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Csection"><span style="color: #800000;">section</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Acknowledgement</span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}[</span><span style="color: #C08020; font-weight: normal;">c</span><span style="color: #E02020; ">]</span>
  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">figure</span></span><span style="color: #E02020; ">}</span>
	<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ccentering"><span style="color: #800000;">centering</span></a>
	<span style="color: #800000; font-weight: normal;">\Huge</span> Thank you!
  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">figure</span></span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">frame</span></span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

The package CtBeamer.sty can be found in <a href="http://210.75.224.29/wordpress/?p=1221" title="latex beamer header package" target="_blank">latex beamer header package</a>