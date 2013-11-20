---
title: gnuplot配合python画多线图
author: 悟道
layout: post
permalink: /?p=2161
categories:
  - gnuplot
  - python
tags:
  - gnuplot
  - python
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<div class="wp_codebox">
  <table>
    <tr id="p2161162">
      <td class="code" id="p2161code162">
        <pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
<span style="color: #808080; font-style: italic;"># -*- coding: utf-8 -*-</span>
<span style="color: #808080; font-style: italic;">#from __future__ import division, with_statement</span>
<span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
Copyright 2010, 闄堝悓 (chentong_biology@163.com).  
Please see the license file for legal information.
===========================================================
'</span><span style="color: #483d8b;">''</span>
__author__ = <span style="color: #483d8b;">'chentong & ct586[9]'</span>
__author_email__ = <span style="color: #483d8b;">'chentong_biology@163.com'</span>
<span style="color: #808080; font-style: italic;">#=========================================================</span>
<span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
<span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">os</span>
&nbsp;
<span style="color: #ff7700;font-weight:bold;">def</span> main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">"Output an eps and pdf graph file with the <span style="color: #000099; font-weight: bold;">\</span>
filename given as prefix."</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
File Format:(with a header line, startswith a '</span><span style="color: #808080; font-style: italic;">#'. This is necessary</span>
<span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: #ff7700;font-weight:bold;">is</span> used to annotate the first line <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #ff7700;font-weight:bold;">as</span> data.<span style="color: black;">&#41;</span>
<span style="color: #808080; font-style: italic;">#sample iso1    iso2    iso3    iso4</span>
sample1 <span style="color: #ff4500;">0.345</span>   <span style="color: #ff4500;">0.35</span>    <span style="color: #ff4500;">0.43</span>    <span style="color: #ff4500;">0.89</span>
sample2 <span style="color: #ff4500;">1.234</span>   <span style="color: #ff4500;">9.23</span>    <span style="color: #ff4500;">20.1</span>    <span style="color: #ff4500;"></span>
sample3 <span style="color: #ff4500;">5.02</span>    <span style="color: #ff4500;">3.42</span>    <span style="color: #ff4500;">0.33</span>    <span style="color: #ff4500;">0.01</span>
sample4 <span style="color: #ff4500;">5.60</span>    <span style="color: #ff4500;">0.01</span>    <span style="color: #ff4500;">0.03</span>    <span style="color: #ff4500;">4.3</span>
<span style="color: #808080; font-style: italic;">#######################</span>
Note: sample column <span style="color: #ff7700;font-weight:bold;">is</span> the x-axis label
sample row <span style="color: #ff7700;font-weight:bold;">is</span> the legend
The column number <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> allowed to be larger than <span style="color: #ff4500;">37</span>.
    <span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
    if len(sys.argv) &lt; 2 :
        print &gt;&gt;sys.stderr, '</span>Using python <span style="color: #66cc66;">%</span>s filename \
legend<span style="color: black;">&#91;</span>default <span style="color: #ff7700;font-weight:bold;">with</span> legend, which <span style="color: #ff7700;font-weight:bold;">is</span> your itms <span style="color: #ff7700;font-weight:bold;">in</span> your first line, \
<span style="color: #ff7700;font-weight:bold;">if</span> there are many items, it would be better to tun it off by supply\
a <span style="color: #ff4500;"></span> here.<span style="color: black;">&#93;</span> xtics<span style="color: black;">&#91;</span>default text xtics, <span style="color: #ff7700;font-weight:bold;">if</span> number supply a <span style="color: #ff4500;"></span><span style="color: black;">&#93;</span> \
preaditionallines<span style="color: black;">&#91;</span><span style="color: #66cc66;">;</span> seperate multiple lines<span style="color: black;">&#93;</span> postaditionallines \
xlabel ylabel title <span style="color: black;">&#91;</span>lines <span style="color: #ff7700;font-weight:bold;">or</span> linespoints<span style="color: black;">&#93;</span><span style="color: #483d8b;">' % sys.argv[0]
        sys.exit(0)
    #---------------------------------
    lenpara = len(sys.argv)
    legendornot = 1
    if lenpara &gt;= 3:
        legendornot = int(sys.argv[2])
    #-------------------------------
    xticsornot = 1 #text xtics
    xticsvalue = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 4:
        xticsornot = int(sys.argv[3])
        xticsvalue = '</span><span style="color: #ff4500;">1</span>:<span style="color: #483d8b;">'
    #-------------------------------
    pregnu = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 5:
        pregnu = sys.argv[4]       
    #-------------------------------
    postgnu = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 6:
        postgnu = sys.argv[5]       
    #-------------------------------
    xlabel = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 7:
        xlabel = sys.argv[6]
    #-------------------------------
    ylabel = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 8:
        ylabel = sys.argv[7]
    #-------------------------------
    title = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 9:
        title = sys.argv[8]
    #-------------------------------
    style = '</span>lines<span style="color: #483d8b;">'
    if lenpara &gt;=10:
        style = sys.argv[9]
    #-------------------------------
    lsDict = {2:'</span> ls <span style="color: #ff4500;">1</span><span style="color: #483d8b;">', 3:'</span> ls <span style="color: #ff4500;">2</span><span style="color: #483d8b;">', 4:'</span> ls <span style="color: #ff4500;">3</span><span style="color: #483d8b;">', 5:'</span> ls <span style="color: #ff4500;">4</span><span style="color: #483d8b;">', 
            6:'</span> ls <span style="color: #ff4500;">5</span><span style="color: #483d8b;">', 7:'</span> ls <span style="color: #ff4500;">6</span><span style="color: #483d8b;">', 8:'</span> ls <span style="color: #ff4500;">7</span><span style="color: #483d8b;">', 9:'</span> ls <span style="color: #ff4500;">8</span><span style="color: #483d8b;">',
            10:'</span> ls <span style="color: #ff4500;">9</span><span style="color: #483d8b;">', 11:'</span> ls <span style="color: #ff4500;">10</span><span style="color: #483d8b;">', 12:'</span> ls <span style="color: #ff4500;">11</span><span style="color: #483d8b;">', 13:'</span> ls <span style="color: #ff4500;">12</span><span style="color: #483d8b;">',
            14:'</span> ls <span style="color: #ff4500;">13</span><span style="color: #483d8b;">', 15:'</span> ls <span style="color: #ff4500;">14</span><span style="color: #483d8b;">', 16:'</span> ls <span style="color: #ff4500;">15</span><span style="color: #483d8b;">', 17:'</span> ls <span style="color: #ff4500;">16</span><span style="color: #483d8b;">',
            18:'</span> ls <span style="color: #ff4500;">17</span><span style="color: #483d8b;">', 19:'</span> ls <span style="color: #ff4500;">18</span><span style="color: #483d8b;">', 20:'</span> ls <span style="color: #ff4500;">19</span><span style="color: #483d8b;">', 21:'</span> ls <span style="color: #ff4500;">20</span><span style="color: #483d8b;">',
            22:'</span> ls <span style="color: #ff4500;">21</span><span style="color: #483d8b;">', 23:'</span> ls <span style="color: #ff4500;">22</span><span style="color: #483d8b;">', 24:'</span> ls <span style="color: #ff4500;">23</span><span style="color: #483d8b;">', 25:'</span> ls <span style="color: #ff4500;">24</span><span style="color: #483d8b;">',
            26:'</span> ls <span style="color: #ff4500;">25</span><span style="color: #483d8b;">', 27:'</span> ls <span style="color: #ff4500;">26</span><span style="color: #483d8b;">', 28:'</span> ls <span style="color: #ff4500;">27</span><span style="color: #483d8b;">', 29:'</span> ls <span style="color: #ff4500;">28</span><span style="color: #483d8b;">',
            30:'</span> ls <span style="color: #ff4500;">29</span><span style="color: #483d8b;">', 31:'</span> ls <span style="color: #ff4500;">30</span><span style="color: #483d8b;">', 32:'</span> ls <span style="color: #ff4500;">31</span><span style="color: #483d8b;">', 33:'</span> ls <span style="color: #ff4500;">32</span><span style="color: #483d8b;">',
            34:'</span> ls <span style="color: #ff4500;">33</span><span style="color: #483d8b;">', 35:'</span> ls <span style="color: #ff4500;">34</span><span style="color: #483d8b;">', 36:'</span> ls <span style="color: #ff4500;">35</span><span style="color: #483d8b;">', 37:'</span> ls <span style="color: #ff4500;">36</span><span style="color: #483d8b;">'
            }
    #-----------------------------
    sample = []
    header = 1
    for line in open(sys.argv[1]):
        if header:
            header = 0
            lineL = line.strip().split()
            plot = '</span>plot <span style="color: #483d8b;">' + '</span>\<span style="color: #483d8b;">''</span> + <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span> '</span>  
            pos = <span style="color: #ff4500;">1</span>
            <span style="color: #ff7700;font-weight:bold;">for</span> item <span style="color: #ff7700;font-weight:bold;">in</span> lineL<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span>:<span style="color: black;">&#93;</span>:
                pos += <span style="color: #ff4500;">1</span>
                <span style="color: #ff7700;font-weight:bold;">if</span> pos == <span style="color: #ff4500;">2</span>:
                    plot += <span style="color: #483d8b;">'using '</span> + xticsvalue + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>pos<span style="color: black;">&#41;</span> + \
                        <span style="color: #483d8b;">' title '</span> + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> +\
                        item + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> + <span style="color: #483d8b;">' with '</span> + style + lsDict<span style="color: black;">&#91;</span>pos<span style="color: black;">&#93;</span>
                <span style="color: #ff7700;font-weight:bold;">else</span>:
                    plot += <span style="color: #483d8b;">',<span style="color: #000099; font-weight: bold;">\'</span><span style="color: #000099; font-weight: bold;">\'</span> using '</span> + xticsvalue + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>pos<span style="color: black;">&#41;</span> + <span style="color: #483d8b;">' title '</span> + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> +\
                        item + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> + <span style="color: #483d8b;">' with '</span> + style + lsDict<span style="color: black;">&#91;</span>pos<span style="color: black;">&#93;</span>
        <span style="color: #808080; font-style: italic;">#---------------------------------------</span>
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            tmp = line.<span style="color: black;">split</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"<span style="color: #000099; font-weight: bold;">\t</span>"</span>,<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span>
            sample.<span style="color: black;">append</span><span style="color: black;">&#40;</span>tmp<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">#--------------------------------------------</span>
    xtics = <span style="color: #483d8b;">'set xtics ('</span>
    i48 = -<span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> item <span style="color: #ff7700;font-weight:bold;">in</span> sample:
        i48 += <span style="color: #ff4500;">1</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> item == <span style="color: #483d8b;">'-'</span>:
            <span style="color: #ff7700;font-weight:bold;">continue</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> i48 == <span style="color: #ff4500;"></span>:
            xtics += <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> + item + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span> '</span> + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>i48<span style="color: black;">&#41;</span> 
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            xtics += <span style="color: #483d8b;">',<span style="color: #000099; font-weight: bold;">\'</span>'</span> + item + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span> '</span> + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>i48<span style="color: black;">&#41;</span> 
    xtics += <span style="color: #483d8b;">')'</span>
    <span style="color: #808080; font-style: italic;">#------------------------------</span>
    <span style="color: #008000;">xrange</span>=<span style="color: #483d8b;">'set xrange [-0.5:'</span> + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>i48+<span style="color: #ff4500;">0.5</span><span style="color: black;">&#41;</span> + <span style="color: #483d8b;">']'</span>
    <span style="color: #808080; font-style: italic;">#------------------------------</span>
    fileout = <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'.plt'</span>
    fh = <span style="color: #008000;">open</span><span style="color: black;">&#40;</span>fileout , <span style="color: #483d8b;">'w'</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'set term postscript eps color'</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">"set output <span style="color: #000099; font-weight: bold;">\'</span>"</span> + <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'.eps<span style="color: #000099; font-weight: bold;">\'</span>'</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
set style line 1 lt 1 linecolor rgb "red"  lw 3
set style line 2 lt 1 linecolor rgb "orange"  lw 3
set style line 3 lt 1 linecolor rgb "#000000"  lw 3
set style line 4 lt 1 linecolor rgb "green"  lw 3
set style line 5 lt 1 linecolor rgb "cyan"  lw 3
set style line 6 lt 1 linecolor rgb "blue"  lw 3
set style line 7 lt 1 linecolor rgb "violet"  lw 3
set style line 8 lt 1 linecolor rgb "olive"  lw 3
set style line 9 lt 1 linecolor rgb "purple"  lw 3
set style line 10 lt 2 linecolor rgb "red"  lw 3
set style line 11 lt 2 linecolor rgb "orange"  lw 3
set style line 12 lt 2 linecolor rgb "#000000"  lw 3
set style line 13 lt 2 linecolor rgb "green"  lw 3
set style line 14 lt 2 linecolor rgb "cyan"  lw 3
set style line 15 lt 2 linecolor rgb "blue"  lw 3
set style line 16 lt 2 linecolor rgb "violet"  lw 3
set style line 17 lt 2 linecolor rgb "olive"  lw 3
set style line 18 lt 2 linecolor rgb "purple"  lw 3
set style line 19 lt 3 linecolor rgb "red"  lw 3
set style line 20 lt 3 linecolor rgb "orange"  lw 3
set style line 21 lt 3 linecolor rgb "#000000"  lw 3
set style line 22 lt 3 linecolor rgb "green"  lw 3
set style line 23 lt 3 linecolor rgb "cyan"  lw 3
set style line 24 lt 3 linecolor rgb "blue"  lw 3
set style line 25 lt 3 linecolor rgb "violet"  lw 3
set style line 26 lt 3 linecolor rgb "olive"  lw 3
set style line 27 lt 3 linecolor rgb "purple"  lw 3
set style line 28 lt 3 linecolor rgb "red"  lw 3
set style line 29 lt 3 linecolor rgb "orange"  lw 3
set style line 30 lt 3 linecolor rgb "#000000"  lw 3
set style line 31 lt 3 linecolor rgb "green"  lw 3
set style line 32 lt 3 linecolor rgb "cyan"  lw 3
set style line 33 lt 3 linecolor rgb "blue"  lw 3
set style line 34 lt 3 linecolor rgb "violet"  lw 3
set style line 35 lt 3 linecolor rgb "olive"  lw 3
set style line 36 lt 3 linecolor rgb "purple"  lw 3
&nbsp;
'</span><span style="color: #483d8b;">''</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #ff7700;font-weight:bold;">not</span> legendornot:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">"set nokey"</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> xticsornot:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #008000;">xrange</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, xtics
    <span style="color: #ff7700;font-weight:bold;">if</span> pregnu:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, pregnu
    <span style="color: #808080; font-style: italic;">#----------------------------</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> xlabel:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'set xlabel <span style="color: #000099; font-weight: bold;">\"</span>%s<span style="color: #000099; font-weight: bold;">\"</span>'</span> <span style="color: #66cc66;">%</span> xlabel 
    <span style="color: #ff7700;font-weight:bold;">if</span> ylabel:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'set ylabel <span style="color: #000099; font-weight: bold;">\"</span>%s<span style="color: #000099; font-weight: bold;">\"</span>'</span> <span style="color: #66cc66;">%</span> ylabel 
    <span style="color: #ff7700;font-weight:bold;">if</span> title:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'set title <span style="color: #000099; font-weight: bold;">\"</span>%s<span style="color: #000099; font-weight: bold;">\"</span>'</span> <span style="color: #66cc66;">%</span> title 
    <span style="color: #808080; font-style: italic;">#-----------------------------</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, plot
    <span style="color: #ff7700;font-weight:bold;">if</span> postgnu:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, postgnu
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'exit'</span>
    fh.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    cmd1 = <span style="color: #483d8b;">'gnuplot '</span> + fileout
    cmd2 = <span style="color: #483d8b;">'convert -density 300 -flatten '</span> + <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'.eps '</span> +\
        <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'.png'</span>
    <span style="color: #dc143c;">os</span>.<span style="color: black;">system</span><span style="color: black;">&#40;</span>cmd1<span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">os</span>.<span style="color: black;">system</span><span style="color: black;">&#40;</span>cmd2<span style="color: black;">&#41;</span>
<span style="color: #ff7700;font-weight:bold;">if</span> __name__ == <span style="color: #483d8b;">'__main__'</span>:
    main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
Plot lines with errorbars

<div class="wp_codebox">
  <table>
    <tr id="p2161163">
      <td class="code" id="p2161code163">
        <pre class="python" style="font-family:monospace;">&nbsp;
<span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
<span style="color: #808080; font-style: italic;"># -*- coding: utf-8 -*-</span>
<span style="color: #808080; font-style: italic;">#from __future__ import division, with_statement</span>
<span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
Copyright 2010, 陈同 (chentong_biology@163.com).  
Please see the license file for legal information.
===========================================================
'</span><span style="color: #483d8b;">''</span>
__author__ = <span style="color: #483d8b;">'chentong & ct586[9]'</span>
__author_email__ = <span style="color: #483d8b;">'chentong_biology@163.com'</span>
<span style="color: #808080; font-style: italic;">#=========================================================</span>
<span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
<span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">os</span>
&nbsp;
<span style="color: #ff7700;font-weight:bold;">def</span> main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">2</span> :
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">"Output an eps and pdf graph file with the <span style="color: #000099; font-weight: bold;">\</span>
    filename given as prefix."</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
    File Format:(with a header line, startswith a '</span><span style="color: #808080; font-style: italic;">#'. This is necessary</span>
    <span style="color: #ff7700;font-weight:bold;">and</span> <span style="color: #ff7700;font-weight:bold;">is</span> used to annotate the first line <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #ff7700;font-weight:bold;">as</span> data.<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">#sample iso1   ylow yhigh   iso2    ylow    yhigh</span>
    sample1 <span style="color: #ff4500;">0.345</span>   <span style="color: #ff4500;">0.1</span> <span style="color: #ff4500;">0.55</span>    <span style="color: #ff4500;">0.35</span>    <span style="color: #ff4500;">0.43</span>    <span style="color: #ff4500;">0.89</span>
    sample2 <span style="color: #ff4500;">1.234</span>   <span style="color: #ff4500;">1.0</span> <span style="color: #ff4500;">1.3</span> <span style="color: #ff4500;">9.23</span>    <span style="color: #ff4500;">20.1</span>    <span style="color: #ff4500;"></span>
    sample3 <span style="color: #ff4500;">5.02</span>    <span style="color: #ff4500;">5</span>   <span style="color: #ff4500;">6</span>   <span style="color: #ff4500;">3.42</span>    <span style="color: #ff4500;">0.33</span>    <span style="color: #ff4500;">0.01</span>
    sample4 <span style="color: #ff4500;">5.60</span>    <span style="color: #ff4500;">5.5</span> <span style="color: #ff4500;">6.2</span> <span style="color: #ff4500;">0.01</span>    <span style="color: #ff4500;">0.03</span>    <span style="color: #ff4500;">4.3</span>
    <span style="color: #808080; font-style: italic;">#######################</span>
    Note: sample column <span style="color: #ff7700;font-weight:bold;">is</span> the x-axis label
    sample row <span style="color: #ff7700;font-weight:bold;">is</span> the legend
    The column number <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> allowed to be larger than <span style="color: #ff4500;">37</span>.
    <span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
        print &gt;&gt;sys.stderr, '</span>Using python <span style="color: #66cc66;">%</span>s filename \
legend<span style="color: black;">&#91;</span>default <span style="color: #ff7700;font-weight:bold;">with</span> legend, which <span style="color: #ff7700;font-weight:bold;">is</span> your itms <span style="color: #ff7700;font-weight:bold;">in</span> your first line, \
<span style="color: #ff7700;font-weight:bold;">if</span> there are many items, it would be better to tun it off by supply\
a <span style="color: #ff4500;"></span> here.<span style="color: black;">&#93;</span> xtics<span style="color: black;">&#91;</span>default <span style="color: #ff4500;">1</span> means text xtics , <span style="color: #ff7700;font-weight:bold;">if</span> number supply a <span style="color: #ff4500;"></span><span style="color: black;">&#93;</span> \
preaditionallines<span style="color: black;">&#91;</span><span style="color: #66cc66;">;</span> seperate multiple lines<span style="color: black;">&#93;</span> postaditionallines \
xlabel ylabel title <span style="color: black;">&#91;</span>lines <span style="color: #ff7700;font-weight:bold;">or</span> linespoints<span style="color: black;">&#93;</span><span style="color: #483d8b;">' % sys.argv[0]
        sys.exit(0)
    #---------------------------------
    lenpara = len(sys.argv)
    legendornot = 1
    if lenpara &gt;= 3:
        legendornot = int(sys.argv[2])
    #-------------------------------
    xticsornot = 1 #text xtics
    xticsvalue = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 4:
        xticsornot = int(sys.argv[3])
        xticsvalue = '</span><span style="color: #ff4500;">1</span>:<span style="color: #483d8b;">'
    #-------------------------------
    pregnu = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 5:
        pregnu = sys.argv[4]       
    #-------------------------------
    postgnu = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 6:
        postgnu = sys.argv[5]       
    #-------------------------------
    xlabel = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 7:
        xlabel = sys.argv[6]
    #-------------------------------
    ylabel = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 8:
        ylabel = sys.argv[7]
    #-------------------------------
    title = '</span><span style="color: #483d8b;">'
    if lenpara &gt;= 9:
        title = sys.argv[8]
    #-------------------------------
    style = '</span>lines<span style="color: #483d8b;">'
    if lenpara &gt;=10:
        style = sys.argv[9]
    #-------------------------------
    lsDict = {2:'</span> ls <span style="color: #ff4500;">1</span><span style="color: #483d8b;">', 3:'</span> ls <span style="color: #ff4500;">2</span><span style="color: #483d8b;">', 4:'</span> ls <span style="color: #ff4500;">3</span><span style="color: #483d8b;">', 5:'</span> ls <span style="color: #ff4500;">4</span><span style="color: #483d8b;">', 
            6:'</span> ls <span style="color: #ff4500;">5</span><span style="color: #483d8b;">', 7:'</span> ls <span style="color: #ff4500;">6</span><span style="color: #483d8b;">', 8:'</span> ls <span style="color: #ff4500;">7</span><span style="color: #483d8b;">', 9:'</span> ls <span style="color: #ff4500;">8</span><span style="color: #483d8b;">',
            10:'</span> ls <span style="color: #ff4500;">9</span><span style="color: #483d8b;">', 11:'</span> ls <span style="color: #ff4500;">10</span><span style="color: #483d8b;">', 12:'</span> ls <span style="color: #ff4500;">11</span><span style="color: #483d8b;">', 13:'</span> ls <span style="color: #ff4500;">12</span><span style="color: #483d8b;">',
            14:'</span> ls <span style="color: #ff4500;">13</span><span style="color: #483d8b;">', 15:'</span> ls <span style="color: #ff4500;">14</span><span style="color: #483d8b;">', 16:'</span> ls <span style="color: #ff4500;">15</span><span style="color: #483d8b;">', 17:'</span> ls <span style="color: #ff4500;">16</span><span style="color: #483d8b;">',
            18:'</span> ls <span style="color: #ff4500;">17</span><span style="color: #483d8b;">', 19:'</span> ls <span style="color: #ff4500;">18</span><span style="color: #483d8b;">', 20:'</span> ls <span style="color: #ff4500;">19</span><span style="color: #483d8b;">', 21:'</span> ls <span style="color: #ff4500;">20</span><span style="color: #483d8b;">',
            22:'</span> ls <span style="color: #ff4500;">21</span><span style="color: #483d8b;">', 23:'</span> ls <span style="color: #ff4500;">22</span><span style="color: #483d8b;">', 24:'</span> ls <span style="color: #ff4500;">23</span><span style="color: #483d8b;">', 25:'</span> ls <span style="color: #ff4500;">24</span><span style="color: #483d8b;">',
            26:'</span> ls <span style="color: #ff4500;">25</span><span style="color: #483d8b;">', 27:'</span> ls <span style="color: #ff4500;">26</span><span style="color: #483d8b;">', 28:'</span> ls <span style="color: #ff4500;">27</span><span style="color: #483d8b;">', 29:'</span> ls <span style="color: #ff4500;">28</span><span style="color: #483d8b;">',
            30:'</span> ls <span style="color: #ff4500;">29</span><span style="color: #483d8b;">', 31:'</span> ls <span style="color: #ff4500;">30</span><span style="color: #483d8b;">', 32:'</span> ls <span style="color: #ff4500;">31</span><span style="color: #483d8b;">', 33:'</span> ls <span style="color: #ff4500;">32</span><span style="color: #483d8b;">',
            34:'</span> ls <span style="color: #ff4500;">33</span><span style="color: #483d8b;">', 35:'</span> ls <span style="color: #ff4500;">34</span><span style="color: #483d8b;">', 36:'</span> ls <span style="color: #ff4500;">35</span><span style="color: #483d8b;">', 37:'</span> ls <span style="color: #ff4500;">36</span><span style="color: #483d8b;">'
            }
    #-----------------------------
    sample = []
    header = 1
    for line in open(sys.argv[1]):
        if header:
            header = 0
            lineL = line.strip().split("<span style="color: #000099; font-weight: bold;">\t</span>")
            plot = '</span>plot <span style="color: #483d8b;">' + '</span>\<span style="color: #483d8b;">''</span> + <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span> '</span>  
            pos = <span style="color: #ff4500;">1</span>
            lenLineL = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>lineL<span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span>, lenLineL, <span style="color: #ff4500;">3</span><span style="color: black;">&#41;</span>:
                item = lineL<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span>
                pos += <span style="color: #ff4500;">1</span>
                errorbar = <span style="color: #483d8b;">':'</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span><span style="color: black;">&#40;</span><span style="color: #008000;">str</span><span style="color: black;">&#40;</span>pos<span style="color: black;">&#41;</span>,<span style="color: #008000;">str</span><span style="color: black;">&#40;</span>pos+<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>,<span style="color: #008000;">str</span><span style="color: black;">&#40;</span>pos+<span style="color: #ff4500;">2</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
                <span style="color: #ff7700;font-weight:bold;">if</span> pos == <span style="color: #ff4500;">2</span>:
                    plot += <span style="color: #483d8b;">'using '</span> + xticsvalue + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>pos<span style="color: black;">&#41;</span> + \
                        <span style="color: #483d8b;">' title '</span> + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> +\
                        item + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> + <span style="color: #483d8b;">' with '</span> + style + lsDict<span style="color: black;">&#91;</span>pos<span style="color: black;">&#93;</span>
                    plot += <span style="color: #483d8b;">',<span style="color: #000099; font-weight: bold;">\'</span><span style="color: #000099; font-weight: bold;">\'</span> using '</span> + xticsvalue + errorbar + \
                        <span style="color: #483d8b;">' with errorbar notitle'</span>  + lsDict<span style="color: black;">&#91;</span>pos<span style="color: black;">&#93;</span>
                <span style="color: #ff7700;font-weight:bold;">else</span>:
                    plot += <span style="color: #483d8b;">',<span style="color: #000099; font-weight: bold;">\'</span><span style="color: #000099; font-weight: bold;">\'</span> using '</span> + xticsvalue + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>pos<span style="color: black;">&#41;</span> + <span style="color: #483d8b;">' title '</span> + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> +\
                        item + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> + <span style="color: #483d8b;">' with '</span> + style + lsDict<span style="color: black;">&#91;</span>pos<span style="color: black;">&#93;</span>
                    plot += <span style="color: #483d8b;">',<span style="color: #000099; font-weight: bold;">\'</span><span style="color: #000099; font-weight: bold;">\'</span> using '</span> + xticsvalue + errorbar + \
                        <span style="color: #483d8b;">' with errorbar notitle'</span>  + lsDict<span style="color: black;">&#91;</span>pos<span style="color: black;">&#93;</span>
        <span style="color: #808080; font-style: italic;">#---------------------------------------</span>
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            tmp = line.<span style="color: black;">split</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"<span style="color: #000099; font-weight: bold;">\t</span>"</span>,<span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span>
            sample.<span style="color: black;">append</span><span style="color: black;">&#40;</span>tmp<span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">#--------------------------------------------</span>
    xtics = <span style="color: #483d8b;">'set xtics ('</span>
    i48 = -<span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> item <span style="color: #ff7700;font-weight:bold;">in</span> sample:
        i48 += <span style="color: #ff4500;">1</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> item == <span style="color: #483d8b;">'-'</span>:
            <span style="color: #ff7700;font-weight:bold;">continue</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> i48 == <span style="color: #ff4500;"></span>:
            xtics += <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span>'</span> + item + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span> '</span> + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>i48<span style="color: black;">&#41;</span> 
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            xtics += <span style="color: #483d8b;">',<span style="color: #000099; font-weight: bold;">\'</span>'</span> + item + <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\'</span> '</span> + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>i48<span style="color: black;">&#41;</span> 
    xtics += <span style="color: #483d8b;">')'</span>
    <span style="color: #808080; font-style: italic;">#------------------------------</span>
    <span style="color: #008000;">xrange</span>=<span style="color: #483d8b;">'set xrange [-0.5:'</span> + <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>i48+<span style="color: #ff4500;">0.5</span><span style="color: black;">&#41;</span> + <span style="color: #483d8b;">']'</span>
    <span style="color: #808080; font-style: italic;">#------------------------------</span>
    fileout = <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'.plt'</span>
    fh = <span style="color: #008000;">open</span><span style="color: black;">&#40;</span>fileout , <span style="color: #483d8b;">'w'</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'set term postscript eps color'</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">"set output <span style="color: #000099; font-weight: bold;">\'</span>"</span> + <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'.eps<span style="color: #000099; font-weight: bold;">\'</span>'</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
set style line 1 lt 1 linecolor rgb "red"  lw 3
set style line 2 lt 1 linecolor rgb "orange"  lw 3
set style line 3 lt 1 linecolor rgb "#000000"  lw 3
set style line 4 lt 1 linecolor rgb "green"  lw 3
set style line 5 lt 1 linecolor rgb "cyan"  lw 3
set style line 6 lt 1 linecolor rgb "blue"  lw 3
set style line 7 lt 1 linecolor rgb "violet"  lw 3
set style line 8 lt 1 linecolor rgb "olive"  lw 3
set style line 9 lt 1 linecolor rgb "purple"  lw 3
set style line 10 lt 2 linecolor rgb "red"  lw 3
set style line 11 lt 2 linecolor rgb "orange"  lw 3
set style line 12 lt 2 linecolor rgb "#000000"  lw 3
set style line 13 lt 2 linecolor rgb "green"  lw 3
set style line 14 lt 2 linecolor rgb "cyan"  lw 3
set style line 15 lt 2 linecolor rgb "blue"  lw 3
set style line 16 lt 2 linecolor rgb "violet"  lw 3
set style line 17 lt 2 linecolor rgb "olive"  lw 3
set style line 18 lt 2 linecolor rgb "purple"  lw 3
set style line 19 lt 3 linecolor rgb "red"  lw 3
set style line 20 lt 3 linecolor rgb "orange"  lw 3
set style line 21 lt 3 linecolor rgb "#000000"  lw 3
set style line 22 lt 3 linecolor rgb "green"  lw 3
set style line 23 lt 3 linecolor rgb "cyan"  lw 3
set style line 24 lt 3 linecolor rgb "blue"  lw 3
set style line 25 lt 3 linecolor rgb "violet"  lw 3
set style line 26 lt 3 linecolor rgb "olive"  lw 3
set style line 27 lt 3 linecolor rgb "purple"  lw 3
set style line 28 lt 3 linecolor rgb "red"  lw 3
set style line 29 lt 3 linecolor rgb "orange"  lw 3
set style line 30 lt 3 linecolor rgb "#000000"  lw 3
set style line 31 lt 3 linecolor rgb "green"  lw 3
set style line 32 lt 3 linecolor rgb "cyan"  lw 3
set style line 33 lt 3 linecolor rgb "blue"  lw 3
set style line 34 lt 3 linecolor rgb "violet"  lw 3
set style line 35 lt 3 linecolor rgb "olive"  lw 3
set style line 36 lt 3 linecolor rgb "purple"  lw 3
&nbsp;
'</span><span style="color: #483d8b;">''</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #ff7700;font-weight:bold;">not</span> legendornot:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">"set nokey"</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> xticsornot:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #008000;">xrange</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, xtics
    <span style="color: #ff7700;font-weight:bold;">if</span> pregnu:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, pregnu
    <span style="color: #808080; font-style: italic;">#----------------------------</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> xlabel:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'set xlabel <span style="color: #000099; font-weight: bold;">\"</span>%s<span style="color: #000099; font-weight: bold;">\"</span>'</span> <span style="color: #66cc66;">%</span> xlabel 
    <span style="color: #ff7700;font-weight:bold;">if</span> ylabel:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'set ylabel <span style="color: #000099; font-weight: bold;">\"</span>%s<span style="color: #000099; font-weight: bold;">\"</span>'</span> <span style="color: #66cc66;">%</span> ylabel 
    <span style="color: #ff7700;font-weight:bold;">if</span> title:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'set title <span style="color: #000099; font-weight: bold;">\"</span>%s<span style="color: #000099; font-weight: bold;">\"</span>'</span> <span style="color: #66cc66;">%</span> title 
    <span style="color: #808080; font-style: italic;">#-----------------------------</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, plot
    <span style="color: #ff7700;font-weight:bold;">if</span> postgnu:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, postgnu
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>fh, <span style="color: #483d8b;">'exit'</span>
    fh.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    cmd1 = <span style="color: #483d8b;">'gnuplot '</span> + fileout
    cmd2 = <span style="color: #483d8b;">'convert -density 300 -flatten '</span> + <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'.eps '</span> +\
        <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span> + <span style="color: #483d8b;">'.png'</span>
    <span style="color: #dc143c;">os</span>.<span style="color: black;">system</span><span style="color: black;">&#40;</span>cmd1<span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">os</span>.<span style="color: black;">system</span><span style="color: black;">&#40;</span>cmd2<span style="color: black;">&#41;</span>
<span style="color: #ff7700;font-weight:bold;">if</span> __name__ == <span style="color: #483d8b;">'__main__'</span>:
    main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-