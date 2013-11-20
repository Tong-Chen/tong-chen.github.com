---
title: Makefile使用小记
author: 悟道
layout: post
permalink: /?p=1595
categories:
  - make
tags:
  - makefile
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.列出目录内所有文件

<pre class="brush: bash; title: ; notranslate" title="">shell := /bin/bash

name=$(shell ls)</pre>

2.使用多变量定义为命令名字

<pre class="brush: bash; title: ; notranslate" title="">$(name):
    @echo $@</pre>

3.命令名字中不能出现函数

正确的：

<pre class="brush: bash; title: ; notranslate" title="">nameN=$(addsuffix .N, $(name))

$(nameN):
    @echo $@</pre>

错误的：

<pre class="brush: bash; title: ; notranslate" title="">$(addsuffix .N, $(name)):
    @echo $@</pre>

4.make在ubuntu中默认使用dash执行脚本命令，因此可能会出一些问题，可以自己制定使用的shell类型

<pre class="brush: bash; title: ; notranslate" title="">shell := /bin/bash

$(shell paste *.file)</pre>

5.自定义隐式命令

<pre class="brush: bash; title: ; notranslate" title="">%.protein:%.gene; 
    translate $&lt; &gt;$@</pre>

6.foreach的使用

<pre class="brush: bash; title: ; notranslate" title=""> $(foreach &lt;var&gt;;,&lt;list&gt;;,&lt;text&gt;;)

把参数&lt;list&gt;中的单词逐一取出放到参数&lt;var&gt;所指定的变量中，然后再执行&lt;text&gt;所包含的表达式。
每一次&lt;text&gt;会返回一个字符串，循环过程中，&lt;text&gt;的所返回的每个字符串会以空格分隔
最后当整个循环结束时，&lt;text&gt;所返回的每个字符串所组成的整个字符串（以空格分隔）将会是foreach函数的返回值。 
所以，&lt;var&gt;最好是一个变量名，&lt;list&gt;可以是一个表达式，而&lt;text&gt;中一般会使用&lt;var&gt;这个参数来依次枚举&lt;list&gt;中的单词。举个例子：
names := a b c d
files := $(foreach n,$(names),$(n).o)
上面的例子中，$(name)中的单词会被挨个取出，并存到变量“n”中，“$(n).o”每次根据“$(n)”计算出一个值，
这些值以空格分隔，最后作为foreach函数的返回，所以，$(files)的值是“a.o b.o c.o d.o”。</pre>

7.Make中增加判断语句，控制执行的命令

<pre class="brush: bash; title: ; notranslate" title="">ifeq ($(gcc),cc )  
    &lt;&gt; 
else 
    &lt;&gt; 
endif
ifdef $gcc 
    &lt;&gt; 
endif
ifndef $gcc 
    &lt;&gt;   
endif
</pre>

   
[ref][1]

8.在Makefile中使用重定向时要定义SHELL的类型

<pre class="brush: bash; title: ; notranslate" title="">SHELL := /bin/bash -e -o pipefail

diff &lt;(sort -u a) &lt;(sort -u b)
</pre>

9.

10.

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

1.参考资料

http://www.jfranken.de/homepages/johannes/vortraege/make.en.html【[make.en][2]】

 [1]: http://wiki.ubuntu.org.cn/%E8%B7%9F%E6%88%91%E4%B8%80%E8%B5%B7%E5%86%99Makefile:%E4%BD%BF%E7%94%A8%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD
 [2]: http://210.75.224.29/wordpress/wp-content/uploads/2012/04/make.en_.pdf