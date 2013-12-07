---
title: R语言学习记录-图形篇
author: 悟道
layout: post
categories:
  - R
  - letter
tags:
  - R
---

1.坐标轴坐标方向  
**las **represents the style of axis labels.  
(0=parallel, 1=all horizontal, 2=all perpendicular to axis, 3=all vertical)

{% highlight r %}
plot(x,y,las=1)
{% endhighlight %}

2.生成一些列的颜色

{% highlight r %}>cm.colors(10, alpha = 1)
[1] "#80FFFFFF" "#99FFFFFF" "#B2FFFFFF" "#CCFFFFFF" "#E6FFFFFF" "#FFE6FFFF"
[7] "#FFCCFFFF" "#FFB2FFFF" "#FF99FFFF" "#FF80FFFF"
>rainbow(n, s = 1, v = 1, start = 0, end = max(1, n - 1)/n, alpha = 1)
>heat.colors(n, alpha = 1)
>terrain.colors(n, alpha = 1)
>topo.colors(n, alpha = 1)
>cm.colors(n, alpha = 1)
{% endhighlight %}

3. 画颜色梯度条

{% highlight r %}library(RColorBrewer)

color.bar &lt;- function(lut, min, max=-min, nticks=11, ticks=seq(min, max, len=nticks), title='') 
{ 
    scale = (length(lut)-1)/(max-min) 
    dev.new(width=1.75, height=5) 
    plot(c(0,10), c(min,max), type='n', bty='n', xaxt='n', xlab='', yaxt='n',   ylab='', main=title) 
     axis(2, ticks, las=1) 
    for (i in 1:(length(lut)-1)) { 
        y = (i-1)/scale + min rect(0,y,10,y+1/scale, col=lut[i], border=NA) 
    } 
}

color.bar(colorRampPalette(c("light green", "yellow", "orange", "red"))(100), -1)
{% endhighlight %}

<http://stackoverflow.com/questions/9314658/colorbar-from-custom-colorramppalette></code>  
<http://www.colbyimaging.com/wiki/statistics/color-bars> </blockquote> 

4.多个图形置于一张图

{% highlight r %}par(mfrow=c(2,2))
{% endhighlight %}

5.Text and Symbol Size

<table width="85%">
  <tr>
    <td>
      <strong>option</strong>
    </td>
    
    <td>
      <strong>description</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      <strong>cex</strong>
    </td>
    
    <td>
      number indicating the amount by which plotting text and symbols should be scaled relative to the default. 1=default, 1.5 is 50% larger, 0.5 is 50% smaller, etc.
    </td>
  </tr>
  
  <tr>
    <td>
      <strong>cex.axis</strong>
    </td>
    
    <td>
      magnification of axis annotation relative to cex
    </td>
  </tr>
  
  <tr>
    <td>
      <strong>cex.lab</strong>
    </td>
    
    <td>
      magnification of x and y labels relative to cex
    </td>
  </tr>
  
  <tr>
    <td>
      <strong>cex.main</strong>
    </td>
    
    <td>
      magnification of titles relative to cex
    </td>
  </tr>
  
  <tr>
    <td>
      <strong>cex.sub</strong>
    </td>
    
    <td>
      magnification of subtitles relative to cex
    </td>
  </tr>
</table>

6.

7.

8.

9.

10.

11.

12.

13.

http://blog.revolutionanalytics.com/2009/01/10-tips-for-making-your-r-graphics-look-their-best.html
