---
title: Python profile
author: 悟道
layout: post
permalink: /?p=2997
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

1.Several ways for profiling Python programs

<pre class="brush: bash; title: ; notranslate" title="">#cProfile Here full path of program needed
python -m cProfile -s time mine.py &lt;args&gt;   
python -m cProfile -o output.file mine.py &lt;args&gt;

#Graphical visularizxation
sudo easy_install pycallgraph
pycallgraph mine.py args
pycallgraph -f svg -o pycallgraph.svg mine.py &lt;args&gt;
</pre>

2.

Ref to http://stackoverflow.com/questions/582336/how-can-you-profile-a-python-script