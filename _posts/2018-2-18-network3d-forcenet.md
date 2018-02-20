---
title: network3D 交互式网络生成
author: ct
layout: post
description:
modified:
categories: [Bioinformatics]
tags: [R]
---

networkD3是基于D3JS的R包交互式绘图工具，用于转换R语言生成的图为交互式网页嵌套图。目前支持网络图，桑基图，树枝图等。

关于网络图的绘制，我们之前有5篇文章，可点击查看。

* [Cytoscape教程1](http://mp.weixin.qq.com/s/m9uJm8GwSXb3xaRxtod08Q)
* [Cytoscape之操作界面介绍](http://mp.weixin.qq.com/s/ZSoW7-qWs3BuSB7bkDnfmA)
* [新出炉的Cytoscape视频教程](http://mp.weixin.qq.com/s/sKEy_Pn9qnWw4W-aXraA5g)
* [Cytoscape: MCODE增强包的网络模块化分析](http://mp.weixin.qq.com/s/jGHuP1ikCX0n3vKfS3VXPQ)
* [一文学会网络分析——Co-occurrence网络图在R中的实现](http://mp.weixin.qq.com/s/s-Si_s5pk7EF5gueqruBRQ)

也可以使用此文介绍的network3D绘制交互式网络图，输入数据与Cytoscape需要的数据格式一致。

运行下方脚本，可得到这个网络图。是关于我们培训现在开通报名的课程、开过的课程和即将要开的课程。

如果需要用自己的数据，也只需替换数据部分，其它部分都是写好的通用脚本。

![](http://www.ehbio.com/ehbio_resource/network_train.png)

```r
#install.packages("networkD3")
library("networkD3")

# 网络数据和节点属性数据以类似格式存入文本文件即可
# 网络文件有3列组成，第一列为
network <- "Src;Target;Value
Bioinfo;Biology;4
Bioinfo;Math;4
Bioinfo;Program;4
Bioinfo;NGS;4
Program;Linux;1
Program;Python;1
Program;R;1
NGS;RNAseq;1
NGS;ChIPseq;3
NGS;16Sseq;3
NGS;Metagenome;1
NGS;SingeCellSeq;3
NGS;DNAmethylseq;1
NGS;lncRNA;3
NGS;Exomeseq;1
NGS;TCGA;1
"

attribute <- "name;group;size
Bioinfo;Class;4
Biology;Class;4
Math;Class;4
Program;Class;4
NGS;Class;4
Linux;On;2
Python;Off;2
R;Off;2
RNAseq;Off;1
ChIPseq;On;1
16Sseq;On;1
Metagenome;On;1
SingeCellSeq;InPrepare;1
DNAmethylseq;InPrepare;1
lncRNA;InPrepare;1
Exomeseq;InPrepare;1
TCGA;InPrepare;1"

network <- read.table(text=network, sep=";", header=T, row.names=NULL, quote="", comment="")

network <- network[,1:3]
colnames(network) <- c("Src", "Target", "Value")

nodes <- unique(c(network$Src, network$Target))
factor_list <- sort(unique(c(levels(network$Src), levels(network$Target))))
num_list <- 0:(length(factor_list)-1)
levels(network$Src) <- num_list[factor_list %in% levels(network$Src)]
levels(network$Target) <- num_list[factor_list %in% levels(network$Target)]

attribute <- read.table(text=attribute, sep=";", header=T, row.names=NULL, quote="", comment="")
attribute <- attribute[match(factor_list, attribute$name),]
```

```
forceNetwork(Links = network, Nodes = attribute,
             width = 600, height=400,
            Source = "Src", Target = "Target",
            Value = "Value", NodeID = "name",
            Group = "group", opacity = 1, 
            legend = T, zoom = T, Nodesize = "size",
            bounded = T, opacityNoHover = 1, fontSize = 15)
```

桑基图

桑基图（Sankey diagram），即桑基能量分流图，也叫桑基能量平衡图。它是一种特定类型的流程图，图中延伸的分支的宽度对应数据流量的大小，通常应用于能源、材料成分、金融等数据的可视化分析。

也可以视为一种层级网络图，比如展示[上一篇文章中的生物信息课程网络图](http://mp.weixin.qq.com/s/rK5SolI0xGisvBCIcb448A)；也可以展示菌群随时间变化的趋势，如[3分和30分文章差距在哪里](https://mp.weixin.qq.com/s/USyg5hsmaimuEvkpPGx-kQ)文章所示哈扎人肠道菌群的季节变化规律。

下面将用2个例子，展示如何用常见网络图数据绘制桑基图。

*最简单桑基图*

第一列为`上游`，第二列为`下游`，第三列为联通值，值越大线越粗。如果您自己有数据，只需要替换输入部分，后面数据格式转换代码是通用的。

```
network <- "Src;Target;Value
Bioinfo;Biology;20
Bioinfo;Math;20
Bioinfo;Program;20
Bioinfo;NGS;20
Program;Linux;8
Program;Python;8
Program;R;6
NGS;RNAseq;1
NGS;ChIPseq;1
NGS;m16Sseq;1
NGS;Metagenome;1
NGS;SingeCellSeq;1
NGS;DNAmethylseq;1
NGS;lncRNA;1
NGS;Exomeseq;1
NGS;TCGA;1
"

network <- read.table(text=network, sep=";", header=T, row.names=NULL, quote="", comment="")

network <- network[,1:3]
colnames(network) <- c("Src", "Target", "Value")

# 转换原始数据点为0起始的一系列整数表示
factor_list <- sort(unique(c(levels(network$Src), levels(network$Target))))
num_list <- 0:(length(factor_list)-1)
levels(network$Src) <- num_list[factor_list %in% levels(network$Src)]
levels(network$Target) <- num_list[factor_list %in% levels(network$Target)]

network$Src <- as.numeric(as.character(network$Src))
network$Target <- as.numeric(as.character(network$Target))

attribute <- data.frame(name=c(factor_list))
```

**network**

> Src Target Value
> 1   1      2    20
> 2   1      8    20
> 3   1     11    20
> 4   1     10    20
> 5  11      6     8
> 6  11     12     8

**attribute**

> head(attribute[, 1])
> [1] 16Sseq       Bioinfo      Biology      ChIPseq      DNAmethylseq
> [6] Exomeseq

```
sankeyNetwork(Links = network, Nodes = attribute,
 Source = "Src", Target = "Target",
 Value = "Value", NodeID = "name",
 fontSize= 12, nodeWidth = 30)
```

![](http://www.ehbio.com/ehbio_resource/Sanky_train1.png)


*点线分组桑基图*

网络数据比上一步的桑基图多一列，指示线的属性；再提供一个节点分组信息文件，获得层次更鲜明的桑基图。

只需要修改对应的数据，后面格式转换的代码通用。

```
network <- "Src;Target;Value;Link_Grp
Bioinfo;Biology;20;Main
Bioinfo;Math;20;Main
Bioinfo;Program;20;Main
Bioinfo;NGS;20;Main
Program;Linux;8;Sub
Program;Python;8;Sub
Program;R;6;Sub
NGS;RNAseq;1;Sub
NGS;ChIPseq;1;Sub
NGS;16Sseq;1;Sub
NGS;Metagenome;1;Sub
NGS;SingeCellSeq;1;Sub
NGS;DNAmethylseq;1;Sub
NGS;lncRNA;1;Sub
NGS;Exomeseq;1;Sub
NGS;TCGA;1;Sub
"


network <- read.table(text=network, sep=";", header=T, row.names=NULL, quote="", comment="")

network <- network[,1:4]
colnames(network) <- c("Src", "Target", "Value", "Link_Grp")

factor_list <- sort(unique(c(levels(network$Src), levels(network$Target))))
num_list <- 0:(length(factor_list)-1)
levels(network$Src) <- num_list[factor_list %in% levels(network$Src)]
levels(network$Target) <- num_list[factor_list %in% levels(network$Target)]

network$Src <- as.numeric(as.character(network$Src))
network$Target <- as.numeric(as.character(network$Target))

# 只需要前两列
attribute <- "name;group;size
Bioinfo;Class;4
Biology;Class;4
Math;Class;4
Program;Class;4
NGS;Class;4
Linux;On;2
Python;Off;2
R;Off;2
RNAseq;Off;1
ChIPseq;On;1
16Sseq;On;1
Metagenome;On;1
SingeCellSeq;InPrepare;1
DNAmethylseq;InPrepare;1
lncRNA;InPrepare;1
Exomeseq;InPrepare;1
TCGA;InPrepare;1"

attribute <- read.table(text=attribute, sep=";", header=T, row.names=NULL, quote="", comment="")
attribute <- attribute[,1:2]
colnames(attribute) <- c("name", "group")
attribute <- attribute[match(factor_list, attribute$name),]

sankeyNetwork(Links = network, Nodes = attribute,
 Source = "Src", Target = "Target",
 Value = "Value", NodeID = "name",
 NodeGroup = "group", LinkGroup = "Link_Grp",
 fontSize= 14, nodeWidth = 30)
```

![](http://www.ehbio.com/ehbio_resource/Sanky_train2.png)

桑基图还有类似的称为冲击图 (alluvial diagram)的展示，具体可见[ggalluvial：冲击图展示组间变化、时间序列和复杂多属性alluvial diagram](http://mp.weixin.qq.com/s/dgxgi_3PdjW5g-fOPlAe4Q)。

说到交互式可视化，还有之前推出的：

* [R语言交互式可视化包CanvasXpress](http://mp.weixin.qq.com/s/EQ7-T66YlAYvqa33Y8z7YA)
* [视频教程：R语言recharts包绘制交互式图形](https://mp.weixin.qq.com/s/XOZD4ftYLPZjM2IVLYgUpA)

关于R绘图, 更多文章如下：

* [在R中赞扬下努力工作的你，奖励一份CheatShet](http://mp.weixin.qq.com/s/x3tWrQPriLRFXO8ZaD93EQ)
* [别人的电子书，你的电子书，都在bookdown](http://mp.weixin.qq.com/s/u8WfC4xQ562Uekhs4WVBoQ)
* [R语言 - 入门环境Rstudio](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483882&amp;idx=1&amp;sn=e16903b4b745a1ef51855be3824149f6&amp;chksm=ec0dc460db7a4d76a70bd4ca2d250f147225252ee963d3e577affaebeeb81dea1ff639d5e9aa#rd)
* [R语言 - 热图绘制 (heatmap)](http://mp.weixin.qq.com/s/mNSkf1rjWTCtE1pIOuI2rA)
* [R语言 - 基础概念和矩阵操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483891&amp;idx=1&amp;sn=40daf6435398c4d9a41f332e9bba4915&amp;chksm=ec0dc479db7a4d6fec413bfb90a4660eb035b440d2bbee998114f7af29e3b3338a8adf62540a#rd)
* [R语言 - 热图简化](https://mp.weixin.qq.com/s/_9LKs6t6rcjzokF_0gneSA)
* [R语言 - 热图美化](http://mp.weixin.qq.com/s/lKrhvYrwn93esC6MA3bHWw)
* [R语言 - 线图绘制](http://mp.weixin.qq.com/s/YB-9tE4ut9RN0yfS8qBhtQ)
* [R语言 - 线图一步法](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483947&amp;idx=1&amp;sn=7cf0252efff5433447507b977fcaff97&amp;chksm=ec0dc7a1db7a4eb77a269709bdf2c8ab51bcad89aa780ec0be171a333e1cb8f3cc27eff277a1#rd)
* [R语言 - 箱线图（小提琴图、抖动图、区域散点图）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483964&amp;idx=1&amp;sn=ee52ac37fb9a919f5c75c0abe2a49ad4&amp;chksm=ec0dc7b6db7a4ea0a51306347fc43265c41fda3eeaf4764ddc3795546371327579676cd74a38#rd)
* [R语言 - 箱线图一步法](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483971&amp;idx=1&amp;sn=1b40a1137ccb8b2fa1ab3eb1d0f05de9&amp;chksm=ec0dc7c9db7a4edf16ea4966b9acb7f23cd23bd6a2e59450ae11bdac899fa2fceb124264dcf4#rd)
* [R语言 - 火山图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483996&amp;idx=1&amp;sn=9a29d52e78e9acffeb0a78077a14f9f2&amp;chksm=ec0dc7d6db7a4ec0163259e81e4ded54875a5dd8adaafbc6975a86c71223d863627ba37801e5#rd)
* [R语言 - 富集分析泡泡图 （文末有彩蛋）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483978&amp;idx=1&amp;sn=e0c158c0e92375553036cc37f4987e40&amp;chksm=ec0dc7c0db7a4ed6ac593493b7d8b52f11f2feb92d24fa00d19527fbb6f95b24f7e313ef9440#rd)
* [R语言 - 散点图绘制](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484056&amp;idx=1&amp;sn=f9b2b4f7495b432e9294b7cbf42eaf33&amp;chksm=ec0dc712db7a4e04769d322558364b4b401b0a8153097c7252e83170e9201a31c2a7abbaf101#rd)
* [一文看懂PCA主成分分析](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484036&amp;idx=1&amp;sn=22ee356d0c9680d56dada1b777985ed2&amp;chksm=ec0dc70edb7a4e182a21475e9ddcde35b907c291549cc8c2e767be260af445ff5455aa358b04#rd)
* [富集分析DotPlot，可以服](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484063&amp;idx=1&amp;sn=f4e93d428e4910b4abbee9c0430cd170&amp;chksm=ec0dc715db7a4e0318b388ba2ab3d51677741421c42ada474a0ac6046a0699283014eae84b6f#rd)
* [R语言 - 韦恩图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484076&idx=1&sn=fa5af19a2a4db4b0c5c7f145bf93ca57&chksm=ec0dc726db7a4e30fe7a0492ed9ea8eb5fa1c34641b1442a2da003efde0546b30c48fde3f118#rd)
* [R语言 - 柱状图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484134&amp;idx=1&amp;sn=ffb41298eae74834af2f5dad05d37921&amp;chksm=ec0dc76cdb7a4e7a852ac0670532c12c690399f140a2335f640eaf01f7da26bc5480941686a9#rd)
* [R语言 - 图形设置中英字体](http://mp.weixin.qq.com/s/NAwyvtTS7t5rRU7KKBwHTA)
* [R语言 - 非参数法生存分析](http://mp.weixin.qq.com/s/_Dy9Yn8fc8I0rASGxH5x9A)
* [基因共表达聚类分析和可视化](http://mp.weixin.qq.com/s/ST2SAmfKOptpJOHS8podmQ)
* [R中1010个热图绘制方法](http://mp.weixin.qq.com/s/N7oLvJ1oPIImgybJVVSxXg)
* [还在用PCA降维？快学学大牛最爱的t-SNE算法吧, 附Python/R代码](http://mp.weixin.qq.com/s/alBfj3Y08qCnZoz5JwVdaw)
* [一个函数抓取代谢组学权威数据库HMDB的所有表格数据](http://mp.weixin.qq.com/s/rYjcsfHrbcAhaFpQI5Yc6g)
* [文章用图的修改和排版](https://mp.weixin.qq.com/s/IJNyhinakY0lSXgCN7b9ug)

点击**阅读原文**，了解更多培训信息。



