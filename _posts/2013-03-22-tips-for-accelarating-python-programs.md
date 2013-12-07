---
title: Tips for accelarating python programs
author: 悟道
layout: post
categories:
  - python
  - article
tags:
  - python
---

1.Use **join** instead of **+** to concentrate strings.  
In python, **string** is unchangable. Each time you add a segment to existed string, it will re-create memeory to save new string. Thus, old string will be copy-paste for many times (No. of seg &#8211; 1).

2.Use local variable

<pre class="brush: python; title: ; notranslate" title="">#list = []
#for i in xrange(100):
#    list.append(i)
#
list = []
append = list.append
for i in xrange(100):
    append(i)
#or
list = [i for i in xrange(400)]

</pre>

3.Use array from stdlib array instead of list when dealing with homogeneous data (all same type). This would save some memory.

<pre class="brush: python; title: ; notranslate" title="">from array import array
list = array()
append = list.append
for i in xrange(100):
    append(i)
</pre>

4.
