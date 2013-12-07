---
title: ggplot2 tips
layout: post
categories:
  - R
  - letter
tags:
  - ggplot2
  - R
---

##### -General usages 

[click here to see list of opts](https://github.com/hadley/ggplot2/wiki/+opts%28%29-List)

{% highlight r %}
1.theme_get() will show you the "hidden" options that you can use in theme()
2.?opts or ?themes
{% endhighlight %}


##### -Change font size and color for labels [link](http://stackoverflow.com/questions/3864535/how-can-i-add-a-subtitle-and-change-the-font-size-of-ggplot-plots-in-r)

{% highlight r %}
#chang axis size
theme(axis.text.x=element_text(size=X)) + theme(axis.text.y=element_text(size=X))
theme(axis.text.x=element_text(angle=90,hjust=1))

#Erase labels and ticks on x,y axis  
p + theme(axis.ticks=element\_blank(), axis.text.x=element\_blank(), \  
axis.text.y=element\_blank(),axis.ticks.x = element\_blank())  
{% endhighlight %}

##### -Title, xlab, ylab

{% highlight r %}
#wrap the title, you can use "\n" to move the remaining text to a new line:
#ggplot2 doesn't have "subtitle" functionality. 
#But you can use the \n term in any of the labels to drop down a line.
theme(title="text \n more text")
xlab(NULL) + ylab(NULL)
{% endhighlight %}

##### -Axis transform log [link](http://wiki.stdout.org/rcookbook/Graphs/Axes%20%28ggplot2%29/#axis-transformations-log-sqrt-etc)

{% highlight r %}
# A scatterplot with regular (linear) axis scaling
sp <- ggplot(dat, aes(xval, yval)) + geom_point()
sp

# log2 scaling of the y axis (with visually-equal spacing)
library(scales) # Need the scales package
sp + scale_y_continuous(trans=log2_trans())

# log2 coordinate transformation (with visually-diminishing spacing)
sp + coord_trans(y="log2")

#scale_y_log2() will do the transformation first and then calculate the geoms
#coord_trans() will do the opposite: calculate the geoms first, and the transform the axis.
#So you need coord_trans(ytrans = "log2") instead of scale_y_log2()
{% endhighlight %}

##### -operations for legends

{% highlight r %}
theme(legend.key.width=unit(1, "in"),
legend.text = theme_text(size=30),
legend.title=element_blank(), #no legend title
legend.key=element_blank(), #no border for legend
legend.position="none"  #"right","left","top"
legend.position=c(0.08,0.8) #0.08 means right away from y-axis, 0.8 means above from x-axis, relative to the size of picture
legend.direction = "vertical",
legend.justification = "center"
)
{% endhighlight %}

##### -Set the levl of legends

{% highlight r %}
foomelt$COG <- factor(foomelt$COG, levels = unique(as.character(foo[[1]])), ordered=T)
{% endhighlight %}

##### facets

{% highlight r %}
facet_wrap(~Size,  ncol=6,  scale='free')   #horizontally , six pics one row, each pic can have different axis ranges(scale='free').
Another solution for facets http://stackoverflow.com/questions/1532535/showing-multiple-axis-labels-using-ggplot2-with-facet-wrap-in-r
{% endhighlight %}

##### Add pearson coefficient [link](http://stackoverflow.com/questions/2050610/creating-a-facet-wrap-plot-with-ggplot2-with-different-annotations-in-each-plot)

{% highlight r %}
# Calculate correlation coefficient
with(mtcars,cor(wt, mpg, use = "everything", method = "pearson"))
[1] -0.8676594
#annotate the plot
+ geom_abline(intercept = 37, slope = -5) + 
geom_text(data = data.frame(), aes(4.5, 30, label = "Pearson-R = -.87"))
{% endhighlight %}

##### Remove grid line and use white background

{% highlight r %}
theme_bw()
theme(panel.grid.major = element_blank(), #theme_blank for old version
panel.grid.minor = element_blank())  #theme_blank for old version
{% endhighlight %}

##### [ggplot2 layout] (https://ggplot2-dev.googlegroups.com/attach/5aa16afece3d5bc6/theme0.html?gda=9XgBzEYAAABCncUW0npTUN_veVgl3inYi0oNsf4Sjxsz8g3AimkTHy2Q5nwgitdzQrQMmMK7aytx40jamwa1UURqDcgHarKEE-Ea7GxYMt0t6nY0uV5FIQ&view=1&part=4)

##### geom_boxplot

{% highlight r %}
1.Hidden outliers
geom_boxplot(outlier.colour='NA')
2.Adjust ylim
stats <- boxplot.stats(value)$stats
ylim_zoomin <- c(stats[1]/2,stats[5]*2)
p + coord_cartesian(ylim=ylim_zoomin)
{% endhighlight %}

##### manually set line type and lince color

{% highlight r %}
ggplot(mort3, aes(x = year, y = BCmort, col = State, linetype = State)) +
  geom_line(lwd = 1) +
  scale_linetype_manual(values = c(rep("solid", 10), rep("dashed", 6))) +
  scale_color_manual(values = c(brewer.pal(10, "Set3"), brewer.pal(6, "Set3"))) +
  opts(title = "BC mortality") +
  theme_bw()

scale_color_manual(values = c("red",'green','blue')
scale_color_manual(values = c(rgb(255/255,0/255,0/255),rgb(0/255,255/255,0/255),rgb(0/255,0/255,255/255))
[http://stackoverflow.com/questions/11344561/controlling-line-color-and-line-type-in-ggplot-legend]
{% endhighlight %}

##### manually set ytics and xtics

{% highlight r %}
scale_x_continuous(breaks=round(seq(min(dat$x), mx(dat$x), by=0.5),1))

sclale_y_continuous(breaks=c(8,16,100,128,512,1000))  #any number

{% endhighlight %}

##### color define

[color bars] (http://www.colbyimaging.com/wiki/statistics/color-bars)

[color plate](http://www.r-bloggers.com/define-intermediate-color-steps-for-colorramppalette/)

