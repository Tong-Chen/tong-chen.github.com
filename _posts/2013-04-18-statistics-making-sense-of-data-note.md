---
title: 'Statistics: Making Sense of Data &#8211;Note'
author: 悟道
layout: post
permalink: /?p=3101
categories:
  - sta
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.Trimmed means: remoce p% of data at both ends, n-2n\*p%. If n\*p% is not integer, sill 2n\*p% data removed. Besides, the two ends of remaining data will time the fraction part of n\*p%.

Trimmed mean involves trimming P percent observations from both ends.

E.g.: If you are asked to compute a 10% trimmed mean, P=10.

Given a bunch of observations, Xi:

1.  First find n = number of observations.
2.  Reorder them as &#8220;order statistics&#8221; Xi from the smallest to the largest.
3.  Find lower case p=P/100 = proportion trimmed.
4.  Compute np.

If np is an integer use k=np and trim k observations at both ends.

R = remaining observations = n−2k.

Trimmed mean = (1/R)(Xk+1+Xk+2+…+Xn−k).

**Example**: Find 10% trimmed mean of

2, 4, 6, 7, 11, 21, 81, 90, 105, 121

Here, n=10,p=0.10,k=np=1 which is an integer so trim exactly one observation at each end, since k=1. Thus trim off 2 and 121. We are left with R=n−2k=10−2=8observations.

10% trimmed mean= (1/8) * (4 + 6 + 7 + 11 + 21 + 81 + 90 + 105) = 40.625

If np has a fractional part present, trimmed mean is a bit more complicated. In the above example, if we wanted 15% trimmed mean, P=15,p=0.15,n=10,k=np=1.5. This has integer part 1 and fractional part 0.5 is present. R=n−2k=10−2∗1.5=10−3=7. Thus R=7observations are retained.

Addendum upon @whuber&#8217;s comment: To remain unbiased (after removing 2 and 121), it seems we must remove half of the 4 and half of the 105 for a trimmed mean of (4/2+6+7+11+21+81+90+105/2)/7=34.64

&nbsp;

2.