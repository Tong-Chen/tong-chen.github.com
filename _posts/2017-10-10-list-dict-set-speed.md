---
title: 为啥我的Python这么慢 - 项查找 (二)
author: ct
layout: post
categories:
  - Python
tags:
  - Python
  - Bioinfo
---

上一篇[为啥我的Python这么慢, 字符串的加和和join](https://mp.weixin.qq.com/s/n5kkZfC8FGlzeBODarLHcw)被陈群主分享到`biopython-生信`QQ群时，乐平指出字典的写法存在问题，并给了一篇知乎的链接<https://zhuanlan.zhihu.com/p/28738634>指导如何高效字典操作。

根据那篇文章改了两处写法，如下：

```python
from collections import defaultdict

aDict = defaultdict(list)

for line in open("GRCh38.fa"):
    if line[0] == '>':
        key = line[1:-1]
    else:
        aDict[key].append(line.strip())
#----------------------------------------
for key, value in aDict.iteritems():
    aDict[key] = ''.join(value)
```

比之前提速接近`2s`。一个是使用了`defaultdict`初始化字典，另外一个是用`iteritems`遍历字典，节省近一半的内存。

`defaultdict`用在这效果不太明显，之前处理全基因组每个位点数据的频繁存取时，`defaultdict`在程序无论速度还是写法上都有很大提升。

```bash
time python readFaJoin2.py

real	0m49.114s
user	0m38.442s
sys	0m10.565s

```

字典本身还有更多高效用法，可以去参考知乎的那篇文章。这儿介绍的是妙用字典的哈希属性快速查找项。

在生信操作中，常常会在一个大矩阵中匹配已小部分基因或位点，提取关注的基因或位点的信息。最开始的写法是：

```python
targetL = ['a', 'n', 'c', 'd']
if item in targetL:
	other_operations
```

后来，随着数据量变大，发现这个速度并不快，于是换了下面的方式

```python
targetL = ['a', 'n', 'c', 'd']
targetD = dict.fromkeys(targetL, 0)

if item in targetD:
	other_operations
```

又可以愉快的查询了。

为什么呢？

这是因为：在`Pyhton`中列表的查询时间复杂度是`O(n)`(`n`是列表长度)；字典的查询负责度是`O(1)`(与字典长度无关)。

字典的查询复杂度为什么是`O(1)`呢？ Python中实现了一个`hash`函数，把字典的`key`转换为`哈希`值，组成连续地址的数字`哈希表`。字典的每次查询转换为了从数组特定位置取出一个元素，所以时间复杂度为`O(1)`。

后来发现`python`中`set`也是用`hash table`存储，所以上面的程序，可以更简化而不影响速度。

```python
targetS = set(['a', 'n', 'c', 'd'])

if item in targetS:
	other_operations
```

那么速度到底差多大，有没有直观一些的展示呢? 这是StackOverflow的一个简化例子, 百万倍速度差异。

```
ct@ehbio:~$ python -mtimeit -s 'd=range(10**7)' '5*10**6 in d'
```

10 loops, best of 3: `182 msec` per loop

```
ct@ehbio:~$ python -mtimeit -s 'd=dict.fromkeys(range(10**7))' '5*10**6 in d'
```

10000000 loops, best of 3: `0.16 usec` per loop

```
ct@ehbio:~$ python -mtimeit -s 'd=set(range(10**7))' '5*10**6 in d'
```

10000000 loops, best of 3: `0.164 usec` per loop

Ref:

* [速度测试例子 https://stackoverflow.com/questions/513882/python-list-vs-dict-for-look-up-table](https://stackoverflow.com/questions/513882/python-list-vs-dict-for-look-up-table)
* [python各数据结构时间复杂度 https://wiki.python.org/moin/TimeComplexity](https://wiki.python.org/moin/TimeComplexity)

