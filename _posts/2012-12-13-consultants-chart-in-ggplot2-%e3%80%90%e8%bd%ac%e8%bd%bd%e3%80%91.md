---
title: Consultants’ Chart in ggplot2 【转载】
author: 悟道
layout: post
permalink: /?p=2681
categories:
  - R
tags:
  - ggplot2
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<div>
  <h1>
    Consultants’ Chart in ggplot2
  </h1>
  
  <div id="single-date">
    August 16, 2010
  </div>
</div>

<div>
  <div>
    tags: <a href="http://learnr.wordpress.com/tag/chart/" rel="tag">chart</a>, <a href="http://learnr.wordpress.com/tag/excel/" rel="tag">excel</a>, <a href="http://learnr.wordpress.com/tag/ggplot2/" rel="tag">ggplot2</a>, <a href="http://learnr.wordpress.com/tag/polar/" rel="tag">polar</a>, <a href="http://learnr.wordpress.com/tag/r/" rel="tag">R</a>, <a href="http://learnr.wordpress.com/tag/rose/" rel="tag">rose</a>
  </div>
  
  <div>
  </div>
</div>

<div>
  <p>
    Excel Charts Blog <a href="http://www.excelcharts.com/blog/the-consultants-chart-revisited/">posted</a> a video tutorial of how to create a circumplex or rose or dougnut chart in Excel. Apparently this type of chart is very popular in the consulting industry, hence the “Consultants’ Chart”.
  </p>
  
  <p>
    <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/12/consulting.gif"><img class="aligncenter size-thumbnail wp-image-2682" title="consulting" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/12/consulting-150x150.gif" alt="" width="150" height="150" /></a>
  </p>
  
  <div>
  </div>
  
  <p>
    It is very easy to make this chart in Excel 2010, but it involves countless number of clicks and formulas to format both the source data and the chart itself.
  </p>
  
  <p>
    In <a href="http://had.co.nz/ggplot2">ggplot2</a> the same can be achieved with around 10 lines of code, as can be seen below.
  </p>
  
  <p>
    &nbsp;
  </p>
  
  <hr />
  
  <h2>
    <a name="_set_up_dummy_dataframe"></a>Set up dummy dataframe
  </h2>
  
  <table width="100%" border="0" bgcolor="#e8e8e8">
    <tr>
      <td>
        <pre>&gt; set.seed(9876)
&gt; DF &lt;- data.frame(variable = 1:10, value = sample(10,
+     replace = TRUE))
&gt; DF
   variable value
1         1     9
2         2     4
3         3     2
4         4     6
5         5     5
6         6     3
7         7     5
8         8     7
9         9     6
10       10     2</pre>
      </td>
    </tr>
  </table>
  
  <hr />
  
  <h2>
    <a name="_prepare_the_charts"></a>Prepare the charts
  </h2>
  
  <table width="100%" border="0" bgcolor="#e8e8e8">
    <tr>
      <td>
        <pre>&gt; library(ggplot2)</pre>
      </td>
    </tr>
  </table>
  
  <p>
    Dougnut chart is essentially a bar chart using a polar coordinate system, so we start off with a simple bar chart. And to make life a bit more colourful will fill each slice with a different colour.
  </p>
  
  <table width="100%" border="0" bgcolor="#e8e8e8">
    <tr>
      <td>
        <pre>&gt; ggplot(DF, aes(factor(variable), value, fill = factor(variable))) +
+     geom_bar(width = 1)</pre>
      </td>
    </tr>
  </table>
  
  <div>
  </div>
  
  <p>
    <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/12/rose_circumplex_chart-005.png"><img class="aligncenter size-thumbnail wp-image-2683" title="rose_circumplex_chart-005" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/12/rose_circumplex_chart-005-150x150.png" alt="" width="150" height="150" /></a>
  </p>
  
  <p>
    Next the coordinate system is changed and some of the plot elements are removed for a cleaner look.
  </p>
  
  <table width="100%" border="0" bgcolor="#e8e8e8">
    <tr>
      <td>
        <pre>&gt; last_plot() + scale_y_continuous(breaks = 0:10) +
+     coord_polar() + labs(x = "", y = "") + opts(legend.position = "none",
+     axis.text.x = theme_blank(), axis.text.y = theme_blank(),
+     axis.ticks = theme_blank())</pre>
      </td>
    </tr>
  </table>
  
  <div>
    <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/12/rose_circumplex_chart-007.png"><img class="aligncenter size-thumbnail wp-image-2684" title="rose_circumplex_chart-007" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/12/rose_circumplex_chart-007-150x150.png" alt="" width="150" height="150" /></a>
  </div>
  
  <hr />
  
  <h2>
    <a name="_adding_gridlines"></a>Adding gridlines
  </h2>
  
  <p>
    <strong>Update 17 August 2010</strong>
  </p>
  
  <p>
    Several commentators asked how to draw gridlines on top of the slices as in the original example.
  </p>
  
  <p>
    Putting the gridlines/guides on top of the plot is accomplished by adding a new variable that is purely used for drawing the borders of each slice element. Essentially, it stacks the required number of slices with a white border on top of each other.
  </p>
  
  <table width="100%" border="0" bgcolor="#e8e8e8">
    <tr>
      <td>
        <pre>&gt; DF &lt;- ddply(DF, .(variable), transform, border = rep(1,
+     value))
&gt; head(DF, 10)
   variable value border
1         1     9      1
2         1     9      1
3         1     9      1
4         1     9      1
5         1     9      1
6         1     9      1
7         1     9      1
8         1     9      1
9         1     9      1
10        2     4      1</pre>
      </td>
    </tr>
  </table>
  
  <table width="100%" border="0" bgcolor="#e8e8e8">
    <tr>
      <td>
        <pre>&gt; ggplot(DF, aes(factor(variable))) + geom_bar(width = 1,
+     aes(y = value, fill = factor(variable))) +
+     geom_bar(aes(y = border, width = 1), position = "stack",
+         stat = "identity", fill = NA, colour = "white") +
+     scale_y_continuous(breaks = 0:10) + coord_polar() +
+     labs(x = "", y = "") + opts(legend.position = "none",
+     axis.text.x = theme_blank(), axis.text.y = theme_blank(),
+     axis.ticks = theme_blank())</pre>
      </td>
    </tr>
  </table>
  
  <div>
    <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/12/rose_circumplex_chart-010.png"><img class="aligncenter size-thumbnail wp-image-2687" title="rose_circumplex_chart-010" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/12/rose_circumplex_chart-010-150x150.png" alt="" width="150" height="150" /></a>
  </div>
  
  <div>
    转载：http://learnr.wordpress.com/2010/08/16/consultants-chart-in-ggplot2/#more-2445
  </div>
</div>