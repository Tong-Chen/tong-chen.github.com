---
title: Python 经典小程序
author: 悟道
layout: post
categories:
  - python
  - letter
tags:
  - python
---

##### 字典生成

{% highlight python %}
#--a file---------
chr1	1
chr2	2
#------end file----
dict([line.strip().split() for line in open(file)])
{% endhighlight %}

##### Global variable

> First `global variable_name` when using global variable in a function  

##### python判断是否到文件结束
{% highlight python %}
if line: # not end
		print 'Non-end'
if line.strip(): # not blank line
		print "Non-blank"
{% endhighlight %}

##### Python start local server
{% highlight python %}
#Will run an instant file server on port 8000 on the current directory
python -m SimpleHTTPServer - 
{% endhighlight %}

