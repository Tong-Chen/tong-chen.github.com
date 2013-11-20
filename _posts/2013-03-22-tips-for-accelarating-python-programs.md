---
title: Tips for accelarating python programs
author: 悟道
layout: post
permalink: /?p=3006
categories:
  - python
tags:
  - python
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.Use **join** instead of **+** to concentrate strings.  
In python, **string** is unchangable. Each time you add a segment to existed string, it will re-create memeory to save new string. Thus, old string will be copy-paste for many times (No. of seg &#8211; 1).

2.Use local variable

<pre class="brush: python; title: ; notranslate" title="">#list = []
#for i in xrange(100):
#    list.append(i)
#
list = []
append = list.append
for i in xrange(100):
    append(i)
#or
list = [i for i in xrange(400)]

</pre>

3.Use array from stdlib array instead of list when dealing with homogeneous data (all same type). This would save some memory.

<pre class="brush: python; title: ; notranslate" title="">from array import array
list = array()
append = list.append
for i in xrange(100):
    append(i)
</pre>

4.