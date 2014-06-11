---
title: Record learning process of Python scientific computation
author: 悟道 [ct586(9)]
layout: post
categories:
  - python
  - letter
tags:
  - python
---

### Basic usage of Numpy (`import numpy as np`)

> Assume you have a file names 'test' containing the following lines.
> ---------File Begins at below-----------------------------
> Name    CTCF    DnaseI  EB
> A20     106.775 7.25444 2
> A18     56.07   14.4547 3
> A23     119.992 25.3157 9
> A15     124.967 117.176 9
> A27     76.4879 12.1073 11
> A28     84.4517 12.9363 11
> A13     162.313 48.6617 13
> A24     121.3   16.5198 16
> A10     20.1017 2.73259 20
> A25     75.369  31.2857 24
> ---------File ends at above-----------------------------

#### Load files using np.loadtxt()

{% highlight bash %}
# In default, np.loadtxt will split columns on white space and return a two dimensional array.
# Column number starts with 0, (1,2,3) indicates the 2nd,3nd and 4th column. 
two_dimensional_array = np.loadtxt('test', usecols=(1,2,3),skiprows=1)

{% endhighlight %}

