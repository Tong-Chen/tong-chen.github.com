---
title: WP-CodeBox
author: 悟道
excerpt: Wrap your code and syntax highlight.
layout: post
permalink: /?p=19
categories:
  - tool
tags:
  - tool
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

**[WP-CodeBox][1] **  
**Author: Eric.Wang**  
provides clean syntax highlighting and AJAX advanced features for embedding source code within pages or posts. It support wide range of popular languages highlighting with line numbers, code download, Copy to clipboard, collapse codebox,automatic keywords link to API manual and maintains formatting while copying snippets of code from the browser.

It&#8217;s provide simple background configuration for highlighter style/formatting customization. Since the plugin is developing, in the future it will support more options.(CSS option,Keywords display style,Auto Caps/Nocaps,Case Sensitivity etc. )  
Basic Usage

Wrap code blocks with  
*  
**<pre lang=&#8221;LANGUAGE&#8221; line=&#8221;1&#8243; file=&#8221;download.txt&#8221; colla=&#8221;-&#8221; >  
content  
</pre>**  
*  
Possible Parameters:

* lang=&#8221;LANGUAGE&#8221; &#8211; LANGUAGE is a GeSHi supported language syntax.  
* file=&#8221;download.txt&#8221; &#8211; The file will create a code downloading attribute.  
* line=&#8221;N&#8221; &#8211; The N is the starting line number.  
* colla=&#8221;+/-&#8221; &#8211; The +/- will expand/collapse the codebox.  
* line,file,colla is optional.

This is a test:

* * *

<div class="wp_codebox">
  <table>
    <tr id="p191">
      <td class="code" id="p19code1">
        <pre class="python" style="font-family:monospace;"> <span style="color: #ff7700;font-weight:bold;">def</span> compute_prefix_function<span style="color: black;">&#40;</span>p<span style="color: black;">&#41;</span>:
    m = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>p<span style="color: black;">&#41;</span>
    pi = <span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">*</span> m
    k = <span style="color: #ff4500;"></span>
    <span style="color: #ff7700;font-weight:bold;">for</span> q <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span>, m<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">while</span> k <span style="color: #66cc66;">&</span>gt<span style="color: #66cc66;">;</span> <span style="color: #ff4500;"></span> <span style="color: #ff7700;font-weight:bold;">and</span> p<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!</span>= p<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span>:
            k = pi<span style="color: black;">&#91;</span>k - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> p<span style="color: black;">&#91;</span>k<span style="color: black;">&#93;</span> == p<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span>:
            k = k + <span style="color: #ff4500;">1</span>
        pi<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span> = k
&nbsp;
    <span style="color: #ff7700;font-weight:bold;">return</span> pi
<span style="color: #ff7700;font-weight:bold;">def</span> kmp_matcher<span style="color: black;">&#40;</span>t, p<span style="color: black;">&#41;</span>:
    n = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>t<span style="color: black;">&#41;</span>
    m = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>p<span style="color: black;">&#41;</span>
    pi = compute_prefix_function<span style="color: black;">&#40;</span>p<span style="color: black;">&#41;</span>
    q = <span style="color: #ff4500;"></span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span>n<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">while</span> q <span style="color: #66cc66;">&</span>gt<span style="color: #66cc66;">;</span> <span style="color: #ff4500;"></span> <span style="color: #ff7700;font-weight:bold;">and</span> p<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span> <span style="color: #66cc66;">!</span>= t<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>:
            q = pi<span style="color: black;">&#91;</span>q - <span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> p<span style="color: black;">&#91;</span>q<span style="color: black;">&#93;</span> == t<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>:
            q = q + <span style="color: #ff4500;">1</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> q == m:
            q = <span style="color: #ff4500;"></span>
            <span style="color: #ff7700;font-weight:bold;">return</span> i - m + <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">return</span> -<span style="color: #ff4500;">1</span></pre>
      </td>
    </tr>
  </table>
</div>

 [1]: http://wordpress.org/extend/plugins/wp-codebox/