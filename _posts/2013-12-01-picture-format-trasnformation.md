---
title: Tips for transforming pictures
layout: post
categories:
- letter
- pic
tags:
- pic
---

#### 1. Convert svg file to png files

{% highlight bash %}
# -e is used to suppress gui
# -d to set dpi
for i in *.svg; do j=${i/svg/png}; inkscape -z -e $j -d 150 $i; done
{% endhighlight %}


