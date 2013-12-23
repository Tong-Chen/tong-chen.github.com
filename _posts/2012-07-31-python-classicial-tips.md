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

##### 区分Python2和Python3的判断

{% highlight python %}
if False: # check if print statement works, SyntaxError if it doesn't
	print 'This program does not work under python 3, run it in python 2.5/2.6/2.7'
{% endhighlight %}

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

