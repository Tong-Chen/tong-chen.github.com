---
title: 单细胞分群后，怎么找到Marker基因定义每一类群？
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

单细胞分析聚类得到各个分类群后，通常我们需要依赖**Marker gene**来定义每一个类群；

在使用`Monocle`进行发育轨迹分析或细胞聚类时，如果有**Marker gene**也可以更好的进行结果分析。

那么如何获取这些对应的**Marker gene**呢？

上次单细胞培训时，一位老师给推荐了`CellMarker`数据库，是哈尔滨医科大学 `Yun Xiao`老师等在2019年1月份发表于*核酸研究 (NAR)*数据库专刊的工作。

该团队通过梳理`100,000+`发表的文献，梳理出人的`158`个组织 (亚组织)的`467`个细胞类型的`13,605`个Marker基因，和鼠的`81`个组织 (亚组织)的`389`个细胞类型的`9, 148`个Marker基因。

![](http://www.ehbio.com/ehbio_resource/cell_marker_human.png)

Marker gene可以很方便的通过左侧层级树浏览查看, 支持该基因为Marker的文献越多，词云图中的字体就越大。来源于`单细胞测序`，`实验验证`, `综述文章`和`公司数据`的支持分别列出。点击`More details`可以查看更详细的名字、数据库外链、来源的文献或其他支持信息等。

![](http://www.ehbio.com/ehbio_resource/cell_marker_browse.png)

同时支持直接搜索组织、细胞系类型或癌症相关的Marker，或搜索一个基因是否为特定的Marker基因。搜索结果以散点图形式展示，点的大小表示横纵轴联合标记的细胞类型的Marker基因的多少。点越小，搜索的基因作为Marker的属性越特异。

![](http://www.ehbio.com/ehbio_resource/cell_marker_search.png)

所有数据都可以全部下载。更希望大家能**提交新的数据**到数据库以维持其数据的更新和构建更好的数据资源。

![](http://www.ehbio.com/ehbio_resource/cell_marker_download.png)

如果您也想做类似的数据库，欢迎与我们联系，已成功在NAR发表两篇数据库文章。



Ref:

* CellMarker: a manually curated resource of cell markers in human and mouse. Nucleic Acids Research. 2018. 

### 单细胞系列分析教程

* [收藏 北大生信平台" 单细胞分析、染色质分析" 视频和PPT分享](https://mp.weixin.qq.com/s/3FGXQlfx2UfbVtpW9kW11w)
* [Science: 小鼠肾脏单细胞转录组+突变分析揭示肾病潜在的细胞靶标](https://mp.weixin.qq.com/s/Qj1SUelmA8mAqmJ5DrlyFA)
* [10X单细胞测序分析软件:Cell ranger，从拆库到定量](https://mp.weixin.qq.com/s/qLqIA7Y3J9xf_tXlQj0FAw)
* [Hemberg-lab单细胞转录组数据分析（一）- 引言](https://mp.weixin.qq.com/s/18baLo2ecG-XiS5igmgV3g)
* [Hemberg-lab单细胞转录组数据分析（二）- 实验平台](https://mp.weixin.qq.com/s/2hN2LENp3bAeq4G8Lf4Ehw)
* [Hemberg-lab单细胞转录组数据分析（三）- 原始数据质控](https://mp.weixin.qq.com/s/uhhyYAjC4gxiQ2s_v_XGGA)
* [Hemberg-lab单细胞转录组数据分析（四）- 文库拆分和细胞鉴定](https://mp.weixin.qq.com/s/k2ZP6sDR0L7ZSDnimerQog)
* [Hemberg-lab单细胞转录组数据分析（五）- STAR, Kallisto定量](https://mp.weixin.qq.com/s/5B1GuPeRtRlYdke7CGtETg)
* [Hemberg-lab单细胞转录组数据分析（六）- 构建表达矩阵，UMI介绍](https://mp.weixin.qq.com/s/tlhCM1A7DmceluIkExgT1A)
* [Hemberg-lab单细胞转录组数据分析（七）- 导入10X和SmartSeq2数据Tabula Muris](https://mp.weixin.qq.com/s/oDji6BkV4ia9xViWRGoY5g)
* [Hemberg-lab单细胞转录组数据分析（八）- Scater包输入导入和存储](https://mp.weixin.qq.com/s/LpHqvdxR9C5kE-58BmKg7g)
* [Hemberg-lab单细胞转录组数据分析（九）- Scater包单细胞过滤](https://mp.weixin.qq.com/s/pGu2qZ9usy1kVqunX_x0-g)
* [Hemberg-lab单细胞转录组数据分析（十）- Scater基因评估和过滤](https://mp.weixin.qq.com/s/HHIFUqCUi1BNZk6SHxATig)
* [Hemberg-lab单细胞转录组数据分析（十一）- Scater单细胞表达谱PCA可视化](https://mp.weixin.qq.com/s/tDGbWN5GHcLrpVwQVkV-Dg)
* [Hemberg-lab单细胞转录组数据分析（十二）- Scater单细胞表达谱tSNE可视化](https://mp.weixin.qq.com/s/c1UOxQZUeyk6P5rhVSNaVA)
