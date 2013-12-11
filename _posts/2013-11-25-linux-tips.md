---
title: Collected tips for linux usage
layout: post
categories:
- linux
- letter
tags:
- linux
---

1. Check if an executable program is 32 bit or 64 bit.
{% highlight bash %}
file `which program-name`
{% endhighlight %}

2. Set the value for executable files or libs
{% highlight bash %}
# For executable
export PATH=${PATH}:/yourpath
# Shared libraries
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/yourpatj
{% endhighlight %}

