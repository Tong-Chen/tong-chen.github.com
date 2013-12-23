---
title: Tips for Jekyll usage
layout: page
categories:
- jekyll
- letter
tags:
- jekyll
---

##### Run local jekyll serve

{% highlight bash %}
jekyll serve
#Aumatically inspect the changes in your site and re-construct the site.
#This parameter will not work well if you use jekyll portable server mentioned
#in HOW-To.
jekyll serve --watch
#First set <baseurl: http_address (no trailing slash)> in <_config.xml>
#Remember to use site.baseurl to represent site.url in all needed places.
#Then run following command and begin local test
jekyll serve --baseurl= 
{% endhighlight %}

##### Jekyll tag like highlight never closed [Liquid exception: highlight tag was never closed][1]

{% highlight bash%}
#add the following line to _config.xml to let the excerpt 
#include the entire post before further process.
#Normally, an empty string will end excerpt immediately and problem solved.
#Also there is a bona fide that the build process will be slightly faster.
excerpt_separator: "" 
{% endhighlight %}





[1] http://blog.slaks.net/2013-08-09/jekyll-tag-was-never-closed
