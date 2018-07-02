---
title: 基因组浏览器使用 (epgg)
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

基因组浏览器是高通量测序分析的一个重要的可视化工具。相比于最终提供的表格，基因组浏览器可以提供更多的信息，如直观展示突变位点、查看有无新转录本或新的可变剪接形式、查看peak的可信度、上下游基因、区域保守性、重复元件、蛋白结合motif等。

我们前面有[测序数据可视化](https://mp.weixin.qq.com/s/8EqULhLCyNttijO9bUm0BQ)列举了4个常用的高通量数据可视化工具，详细介绍了[IGV基因组浏览器可视化高通量测序数据](https://mp.weixin.qq.com/s/vWQUNgVujCTdZgZZ2_AZfQ)和[UCSC 基因组浏览器的安装使用](https://mp.weixin.qq.com/s/b7Cppdm-vMTgZfFVC3Q1lQ)。

最近几次将以华盛顿大学(DC)开发的EPGG基因组浏览器为主要工具，介绍下基因组浏览器的基本展示内容、各部分含义、使用方式等。

基因组浏览器都可以按照**位置**或**基因名字**搜索，可进行局部放大和缩小。虽然每个软件略有不同，但基本操作是通用的。点一点，拽一拽，就都能用了。初次接触一个软件，*多一点耐心，多一点操作*，其实没那么难。

![](http://www.ehbio.com/ehbio_resource/epgg_navigation.png)

基因信息展示包含基因的转录方向信息 (箭头)，基因结构信心 (CDS, UTR, intron)，基因功能描述信息等。方向信息对我们识别**转录起始位点**及**启动子**区域和启动子上的ChIP peak至关重要。

另外还有个功能，基因只在基因组占1%, 浏览起来不方便，**Juxtapose**模式可以只显示基因区，其它区域隐藏，这样截图或浏览起来都更方便。

![](http://www.ehbio.com/ehbio_resource/epgg_gene.png)

重复元件是我们做分析时需要关注的一个点，最近Cell文章发现 **LINE元件** (A LINE-1-Nucleolin Patnership Regulates Early Development and ESC Identity)是胚胎发育的关键。如果我们的数据能在某个重复元件上有特殊分布，也可能催生重要发现呢。

![](http://www.ehbio.com/ehbio_resource/epgg_rep.png)

数值Track是最常见的展示形式，常说的是“峰图”是一种，reads的分布有高有低，形成山峰状。封顶表示对应区域的表达、修饰或结合比较高。

除了峰形图，也可以展示热图、线图等。

数值Track支持的数据一般是**bigWig**格式，在不同浏览器之间通用。不同Track之间比较时需要先对数据做标准化，也需要设置同等大小的**Y轴**。数据可以进行一定程度的拟合，使得结果更清晰 (图中的Smooth window)。

![](http://www.ehbio.com/ehbio_resource/epgg_numerical_track.png)

这个线图常用于比较**富集样品和对照样品**，或比较不同样品之间的表达量高低等。把2个Track放到一起展示，高低立建。UCSC genome browser也有类似功能，而且展示效果更好，我们前面也已提过。

![](http://www.ehbio.com/ehbio_resource/epgg_linplot3.png)

epgg特有的甲基化数据展示，给定每个位点测序深度，CG甲基化比例，CHH，CHG甲基化比例等。还可以在线过滤，筛选不同支持reads数的甲基化位点，更有动态性。是甲基化分析的必备神器。

![](http://www.ehbio.com/ehbio_resource/epgg_methylc_track.png)

染色体的三维结构研究越能越多，用途也越来越大。关联SNP位点的功能，寻找enhancer的靶基因，基因组区域互作，都可以通过Hi-C数据提供更多支持信息。EPGG可以用互作热图或loop连线两种方式展示区域之间的互作。

互作热图的识别方式是：如果要看位点A和位点B之间是否有互作，只需在正负45度方向画一条线，查看线是否有交点和交点处颜色强弱即可判断。

还有圈图形式，从宏观展示某个位点与基因组其它区域的互作。

![](http://www.ehbio.com/ehbio_resource/epgg_long_range_hic.png)

SNP位点展示及连锁不平衡展示，这也是epgg的特有功能。可视化与Hi-C染色体互作类似。

![](http://www.ehbio.com/ehbio_resource/epgg_snp_ld.png)

下一步将讲一下EPGG的自带数据和分析功能，以更方便使用。


