---
title: R boxplot outliers
author: 悟道
layout: post
permalink: /?p=2283
categories:
  - R
  - sta
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.The &#8220;dots&#8221; at the end of the boxplot represent outliers. There are a number of different rules for determining if a point is an outlier, but the method that R and ggplot use is the &#8220;1.5 rule&#8221;. If a data point is:

*   less than Q1 &#8211; 1.5*IQR
*   greater than Q3 + 1.5*IQR

then that point is classed as an &#8220;outlier&#8221;. The line goes to the first data point before the &#8220;1.5&#8243; cut-off. Note: IQR = Q3 &#8211; Q1

**Additional information**

*   See the <a href="http://en.wikipedia.org/wiki/Box_plot#Alternative_forms" rel="nofollow">wikipedia boxplot</a> page for alternative outlier rules.
*   There are actually a variety of ways of calculating quantiles. Have a look at \`?quantile for the description of the *nine* different methods.

http://stackoverflow.com/questions/4946964/in-ggplot2-what-do-the-end-of-the-boxplot-lines-represent/4947033#4947033

2.How to read boxplot?

http://stattrek.com/statistics/charts/boxplot.aspx

3.t-test and boxplot

http://ww2.coastal.edu/kingw/statistics/R-tutorials/index.html