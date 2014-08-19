---
title: latex两列
author: 悟道
layout: post
permalink: /?p=1921
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

Three different styles have to be distinguished when creating multiple columns in a Latex document. Either we want the whole document to have two columns, single pages or only part of a page. In order to do so, three different Latex commands are used…

**Whole document (using article to write a paper):**

The only thing you need to do is changing the first command of your Latex-file.

`\documentclass[11pt,twocolumn]{article}`

It will automatically create two columns in the entire document.

Note: if you are writing a paper, IEEE provides useful templates which can be used and adapted to your needs. You can download them from their “<a title="IEEE Latex paper template" href="http://www.ieee.org/web/publications/authors/transjnl/index.html" target="_blank">Author Digital Tool Box</a>“.

**Single pages:**

The command \twocolumn starts a new page having two columns. Accordingly, \onecolumn starts a new page with a single column assuming you are in a two column environment as described above. Both commans do not take any arguments.

The is a way to define the distance between the two columns, use

`\setlength{\columnsep}{distance}`

If you need a line to separate the columns, the following command will do the job:

`\setlength{\columnseprule}{thickness}`

**Part of a page:**

I have posted another article on that, just have a look [there][1]. \minipage can also be used for text, not only for figures and tables.

&nbsp;

http://texblog.org/2007/08/11/creating-two-columns-in-article-report-or-book/

 [1]: http://texblog.wordpress.com/2007/08/01/placing-figurestables-side-by-side-minipage/ "Placing figures/tables side-by-side"