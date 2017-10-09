---
title: 为啥我的Python这么慢 (一)
author: ct
layout: post
categories:
  - Python
tags:
  - Python
  - Bioinfo
---


长假结束了，这不痛苦。痛苦的是长假结束了，发现写的基因组读取程序还没运行完？

在[Python系列教程](http://mp.weixin.qq.com/s/9BNrq8Lu7hjtO2BAKOIXOA)中，我们提到一个概念字符串是不可修改的。这一点可以通过`id`函数来判断确实是对的。但是这个概念会对我们写作程序有什么影响一直没有特别深的理解。

直到有一次，实验室一个朋友要读基因组数据，结果发现`3 G`的基因组读一晚上都没读完，就很诧异，看了下代码，这么写的。

基因组序列是`GRCh38.fa`，`FASTA`格式，序列行每行`70`个字符，共**44,284,892**行 (记住行数有多大)，示例如下。

```
>chr1
NNNNN...(60个N)...NNNNN
ACGTA...(60个Nt)...ACGTA
...
>chr2
NNNNN...(60个N)...NNNNN
ACGTA...(60个Nt)...ACGTA
...
```

读取程序如下(这里只选了读取基因组的部分，点击查看更多[FASTA的操作](http://mp.weixin.qq.com/s/UyohxmUILG_0smL3cd62xg))：

```python
aDict = {}
for line in open("GRCh38.fa"):
    if line[0] == '>':
        key = line[1:-1]
        aDict[key] = ''
    else:
        aDict[key]+=line.strip()
```

程序看上去没问题，获取`id`，读取一行**附加**在前一行后面，逻辑是对的。然后运行上程序，回去睡觉，满心欢喜期待第二天早上出来获得结果，结果啥也没出来，程序还停留在读取基因组序列步骤。

按我们服务器的性能，这不应该啊。就看代码是不是出问题了，怎么看逻辑都对。后来就想会不会是序列累加的问题，就换了一个写法。代码稍微长了些，先存入列表，再连接起来。

```python
Dict = {}
for line in open("GRCh38.fa"):
    if line[0] == '>':
        key = line[1:-1]
        aDict[key] = []
    else:
        aDict[key].append(line.strip())
#--------------------------------
for key, value in aDict.items():
    aDict[key] = ''.join(value)
```

使用`time`函数，查看下运行速度，不足1分钟。`time`及更多程序监测方法见[命令运行监测和软件安装](http://mp.weixin.qq.com/s/TNU7X2mhfVVffaJ7NRBuNA)。

```
time readFaJoin.py 

real	0m51.256s
user	0m40.729s
sys	0m10.425s
```

不比不知道，一比吓一跳；速度差了何止几千倍。

这时，我们重新理解下什么叫字符串不可修改。

使用`id`函数来确定字符串累加跟列表累加的不同。(不同电脑或不同时间允许的`id`不同，不看具体数字，只看`id`的变化)

```python
ehbio = "Sheng Xin Bao Dian"
id(ehbio)

## Output: 140405359946640

ehbio += ' very good'
ehbio

## Output: 'Sheng Xin Bao Dian very good'

id(ehbio)

## Output: 140405344262576
```

同样的变量名字，但不同的`id`。就是说python在对变量`ehbio`新增字符串时，是先开辟一份内存空间，把`ehbio`原有内容加新内容组成的字符串存入新的内存空间。而不是想象中的直接追加在已有字符串的后面。这样对4千万行数据的操作就是要做4千万次的内存空间开辟和字符串存储。这是一个特别耗时的步骤。

而如果是一个列表呢？

```python
aList = ['Sheng','Xin']

id(aList)

## Output: 140405344245520

aList.append("Bao")

id(aList)

## Output: 140405344245520

aList.extend(["Dian", "excellent"])

id(aList)

## Output: 140405344245520
```

而列表就不一样了，无论是使用`append`增加一个元素，还是使用`extend`增加一组元素，列表变量`aList`的`id`都没有变化。说明这是追加，不是新建。

`Python`使用中还有不少类似这样的需要注意的小细节，在后续会陆续推出。

而且我们生信宝典团队要开培训班了，涉及`Linux系统操作`、`Python编程`、`R Cytoscape作图`和`高通量数据分析`。如果您有需要我们解决的问题，还请后台留言，一并纳入培训班的授课。希望通过我们的努力，让培训发挥作用，不管是来学技术，来学理念，还是来解决你手头棘手的问题，希望都能有所收获。

具体日期静待公布。



