---
title: Errors and solutions in compiling softwares from sources
author: 悟道
layout: post
permalink: /?p=2388
categories:
  - C
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

## 1./usr/bin/ld: cannot find -lyaml-cpp

yaml-cpp indicates the function library name, the nomenclature formula is **lib+yaml-cpp+.so. (**This file usually located in a subdirectory named &#8216;lib&#8217;.** )**

The solution method is to install the deleted library or create a symbol link to already installed one but with different name.

However, usually this happens when the library is installed in non-standard path. For this occasion, LIBRARY\_PATH and LD\_LIBRARY_PATH need to be set.

<div>
  <p>
    <strong>LIBRARY_PATH</strong> is used by gcc <strong>before compilation</strong> to search for directories containing libraries that need to be linked to your program.
  </p>
  
  <p>
    <strong>LD_LIBRARY_PATH</strong> is used by your program to search for directories containing the libraries after it has been<strong> successfully compiled and linked</strong>.
  </p>
  
  <p>
    EDIT: As pointed below, your libraries can be static or shared. If it is static then the code is copied over into your program and you don&#8217;t need to search for the library after your program is compiled and linked. If your library is shared then it needs to be dynamically linked to your program and that&#8217;s when LD_LIBRARY_PATH comes into play.
  </p>
</div>

http://stackoverflow.com/questions/4250624/ld-library-path-vs-library-path

http://bbs.sciencenet.cn/home.php?mod=space&#038;uid=676535&#038;do=blog&#038;id=541444

## 2.error: gsl/gsl_cdf.h: No such file or directory

This happens when the program can not find the header file which needed by the codes.

Those files often locates in sub-directory names &#8216;include&#8217;.

One solution to non-standard path is hacking Makefile with &#8220;INCLUDE = -Iauthor-include **-I/home/me/soft/gsl/include**&#8220;.

The other solution is &#8220;cp -rf **/home/me/soft/gsl/include/* src_dir/**&#8220;.

Third solution is &#8220;export C\_INCLUDE\_PATH=${C\_INCLUDE\_PATH}:**/home/me/soft/gsl/include**&#8221;

[`C_INCLUDE_PATH` (for C header files) or `CPLUS_INCLUDE_PATH` (for C++ header files).]

http://stackoverflow.com/questions/558803/how-to-add-a-default-include-path-for-gcc-in-linux

3.

4.

5.

6.