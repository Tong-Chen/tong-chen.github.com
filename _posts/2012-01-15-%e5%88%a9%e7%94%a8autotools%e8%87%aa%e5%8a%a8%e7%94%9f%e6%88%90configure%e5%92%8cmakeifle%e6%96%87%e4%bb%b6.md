---
title: 利用autotools自动生成configure和Makeifle文件
author: 悟道
layout: post
permalink: /?p=1478
categories:
  - C
  - make
tags:
  - C
  - makefile
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.directory tree  
2.autoscan  
3.mv configure.scan configure.ac  
4.modify configure.ac [modification part the same as mij.oltrelinux.xom/devel/autoconf-automake]  
6.autoconf  
7.autoheader  
8.create Makefile.am  
9.aclocal  
10.automake &#8211;add-missing  
11.autoconf [this will update both configure and Makefile.in, so if you want to modify Makefile.in, make sure no more running of autoconf.]

&nbsp;

&nbsp;