---
title: Latex表格添加脚注
author: 悟道
layout: post
permalink: /?p=981
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

Latex表格可以添加两种形式的脚注：

一个是类似于正文的脚注，利用\footnotemark和\footnotetext  
另一个是表格内脚注，需要包threeparttable

具体用法和效果图：

<div class="wp_codebox">
  <table>
    <tr id="p981106">
      <td class="code" id="p981code106">
        <pre class="latex" style="font-family:monospace;"><span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cdocumentclass"><span style="color: #800000;">documentclass</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">article</span><span style="color: #E02020; ">}</span>
<span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Cusepackage"><span style="color: #800000;">usepackage</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">threeparttable</span><span style="color: #E02020; ">}</span>
&nbsp;
&nbsp;
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #2C922C; font-style: italic;">%A table with footnotes appearing at the bottom of the page:</span>
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">table</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ccentering"><span style="color: #800000;">centering</span></a>
  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tabular</span></span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">llll</span><span style="color: #E02020; ">}</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
  column 1 <span style="color: #E02020; ">&</span> column 2 <span style="color: #E02020; ">&</span> column 3<span style="color: #800000; font-weight: normal;">\footnotemark</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">1</span><span style="color: #E02020; ">]</span> <span style="color: #E02020; ">&</span> column 4<span style="color: #800000; font-weight: normal;">\footnotemark</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">2</span><span style="color: #E02020; ">]</span> <span style="color: #E02020; ">\\</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
  row 1 <span style="color: #E02020; ">&</span> data 1 <span style="color: #E02020; ">&</span> data 2 <span style="color: #E02020; ">&</span> data 3 <span style="color: #E02020; ">\\</span>
  row 2 <span style="color: #E02020; ">&</span> data 1 <span style="color: #E02020; ">&</span> data 2 <span style="color: #E02020; ">&</span> data 3 <span style="color: #E02020; ">\\</span>
  row 3 <span style="color: #E02020; ">&</span> data 1 <span style="color: #E02020; ">&</span> data 2 <span style="color: #E02020; ">&</span> data 3 <span style="color: #E02020; ">\\</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tabular</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ccaption"><span style="color: #800000;">caption</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Table with footnotes at the bottom of the page</span><span style="color: #E02020; ">}</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Clabel"><span style="color: #800000;">label</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">tab:test1</span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">table</span></span><span style="color: #E02020; ">}</span>
<span style="color: #800000; font-weight: normal;">\footnotetext</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">1</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">table footnote 1</span><span style="color: #E02020; ">}</span>
<span style="color: #800000; font-weight: normal;">\footnotetext</span><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">2</span><span style="color: #E02020; ">]{</span><span style="color: #2020C0; font-weight: normal;">table footnote 2</span><span style="color: #E02020; ">}</span>
&nbsp;
&nbsp;
&nbsp;
<span style="color: #2C922C; font-style: italic;">%A table with footnotes appearing at the bottom of the table:</span>
<span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">table</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ccentering"><span style="color: #800000;">centering</span></a>
  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">threeparttable</span></span><span style="color: #E02020; ">}[</span><span style="color: #C08020; font-weight: normal;">b</span><span style="color: #E02020; ">]</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Ccaption"><span style="color: #800000;">caption</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">Table with footnotes after the table</span><span style="color: #E02020; ">}</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Clabel"><span style="color: #800000;">label</span></a><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">tab:test2</span><span style="color: #E02020; ">}</span>
  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tabular</span></span><span style="color: #E02020; ">}{</span><span style="color: #2020C0; font-weight: normal;">llll</span><span style="color: #E02020; ">}</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
  column 1 <span style="color: #E02020; ">&</span> column 2 <span style="color: #E02020; ">&</span> column 3<span style="color: #800000; font-weight: normal;">\tnote</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">1</span><span style="color: #E02020; ">}</span> <span style="color: #E02020; ">&</span> column 4<span style="color: #800000; font-weight: normal;">\tnote</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;">2</span><span style="color: #E02020; ">}</span> <span style="color: #E02020; ">\\</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
  row 1 <span style="color: #E02020; ">&</span> data 1 <span style="color: #E02020; ">&</span> data 2 <span style="color: #E02020; ">&</span> data 3 <span style="color: #E02020; ">\\</span>
  row 2 <span style="color: #E02020; ">&</span> data 1 <span style="color: #E02020; ">&</span> data 2 <span style="color: #E02020; ">&</span> data 3 <span style="color: #E02020; ">\\</span>
  row 3 <span style="color: #E02020; ">&</span> data 1 <span style="color: #E02020; ">&</span> data 2 <span style="color: #E02020; ">&</span> data 3 <span style="color: #E02020; ">\\</span>
  <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Chline"><span style="color: #800000;">hline</span></a>
  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tabular</span></span><span style="color: #E02020; ">}</span>
  <span style="color: #C00000; font-weight: normal;">\begin</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tablenotes</span></span><span style="color: #E02020; ">}</span>
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Citem"><span style="color: #800000;">item</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">1</span><span style="color: #E02020; ">]</span> tablefootnote 1
    <span style="color: #E02020; ">\</span><a href="http://www.golatex.de/wiki/index.php?title=%5Citem"><span style="color: #800000;">item</span></a><span style="color: #E02020; ">[</span><span style="color: #C08020; font-weight: normal;">2</span><span style="color: #E02020; ">]</span> tablefootnote 2
  <span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">tablenotes</span></span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">threeparttable</span></span><span style="color: #E02020; ">}</span>
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">table</span></span><span style="color: #E02020; ">}</span>
&nbsp;
<span style="color: #C00000; font-weight: normal;">\end</span><span style="color: #E02020; ">{</span><span style="color: #2020C0; font-weight: normal;"><span style="color: #0000D0; font-weight: normal;">document</span></span><span style="color: #E02020; ">}</span></pre>
      </td>
    </tr>
  </table>
</div>

<img alt="" src="http://210.75.224.29/wordpress/wp-content/uploads/2011/06/table_footnote.png" class="alignnone" width="392" height="382" />

参考：<http://www.latex-community.org/forum/viewtopic.php?f=45&#038;t=4353>