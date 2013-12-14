---
title: Tips for Jekyll usage
layout: page
categories:
- jekyll
- letter
tags:
- jekyll
---

1. Run local jekyll serve
{% highlight bash %}
jekyll serve
jekyll serve --watch #Aumatically inspect the changes in your site and re-construct the site
jekyll serve --baseurl http://localhost:4000 #Specify url for all links locally to support debug 
{% endhighlight %}

2. Jekyll tag like highlight newver closed [Liquid exception: highlight tag was never closed][1]

{% highlight bash%}
#add the following line to _config.xml to let the excerpt 
#include the entire post before further process.
#Normally, an empty string will end excerpt immediately and problem solved.
#Also there is a bona fide that the build process will be slightly faster.
excerpt_separator: "" 
{% endhighlight %}





[1] http://blog.slaks.net/2013-08-09/jekyll-tag-was-never-closed
