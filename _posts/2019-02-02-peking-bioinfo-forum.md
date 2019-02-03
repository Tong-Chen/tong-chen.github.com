---
title: 北京大学生物信息平台"单细胞分析、染色质分析"公益讨论班
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

北京大学生物信息平台在2018年的暑假和秋季组织了两期关于**单细胞分析、染色质分析**的研讨班，报告人来自于邓兴旺老师组、李程老师组、汤富酬老师组、谢晓亮老师组、张学工老师组、张泽民老师组。内容涉及单细胞分析的基本生物学问题、聚类、可视化、细胞图谱、发育图谱和多组学分析，染色质可及性、三维结构等。授权生信宝典发表出来，让更多朋友可以参与。

视频和PPT在<https://space.bilibili.com/16813275/#/>和<http://202.205.131.32/forum/upload/forum.php?mod=viewthread&tid=324&extra=page%3D1>，后台回复 **北京大学生物信息平台**获取可点击的链接。


## 秋季讨论班内容

*描述为本人根据PPT和自己的理解所注，有不当处为本人而非演讲人责任，具体可听视频学习。*

I. 单细胞分析模块

1. 单细胞分析的生物学问题：The biology of single-cell genomics ，9月17日，主讲人：王龙腾（李程组）<https://share.weiyun.com/5LgmWyO>，（没有回放视频）

   龙腾一定是《[工作细胞](https://mp.weixin.qq.com/s/MhQ34l0pgqCxJnEu1ozcwg)》的忠实粉丝，从这个萌化了的日本动漫入手引出人约有**37兆2千亿**细胞。之前一直有个说法人体内的细菌比人的细胞多，在2006年的cell文章对此作了详细阐述，人体内细菌数目与人的细胞数目在同一数量级，但质量小的太多。一个**70 kg**的成年人，细胞重量在**46 kg**，细菌重量只有**0.2 kg**。有点发散了，后面展开讲受精卵卵裂形成`ICM`、胚胎干细胞、多能性干细胞、各个谱系进一步分化，以此作为铺垫既包含细胞之间的共性(可被常规bulk测序捕获)，又展示细胞类型的丰富 (很多类型未知、谱系追踪不成熟)和异质性(表达、染色体空间结构不完全一致)，这就引出了单细胞测序的优势，进行细胞分型、发育谱系构建、移植前遗传筛选等基础和临床的应用。展望一下，超高分辨率成像也许可以所见既所得的解决这个["被高中生物骗了这么多年，原来人体内细胞的DNA是有不同的？"](https://mp.weixin.qq.com/s/ELpachAsALTwJMPFjM1rrA)的问题。另外一个没提到的问题，单细胞测序细胞量大，尤其是来源于不同的个体或取样跨度时间长时，一定注意批次效应的影响，李程老师的`ComBat`是GEO数据分析批次校正的常用工具。

2. scRNA-seq data visualization and clustering，10月8日，主讲人：陈文昌 邹子恒（清华大学张学工组）链接：<https://share.weiyun.com/5TgOgDM>，（视频地址：<https://www.bilibili.com/video/av33441560>）

   文昌兄主要讲述了单细胞分析常用的降维算法`tSNE`的原理和应用。[PCA的线性降维](https://mp.weixin.qq.com/s/4R14xJkQVPtaufaoXOcPIw)我们比较熟悉了，把线性相关的变量转换为线性无关的向量。其操作方式是对原始矩阵的协方差矩阵进行对角化处理获得新变量的协方差矩阵即实现了线性降维。线性降维算法的一个主要问题是它们集中将不相似的数据点放置在较低维度区域时，数据点相距甚远。 但是为了在低维、非线性流型上表示高维数据，我们也需要把相似的数据点靠近在一起展示，这并不是线性降维算法所能做的。tSNE把点的高维空间的距离转换成点的相似度的概率，维持高维空间和低维空间中一对点之间的条件概率差值总和最小。同时使用t-分布的长尾性解决高维数据映射到低维时的重叠问题。t-SNE算法定义了数据的局部和全局结构之间的软边界，既可以使点在局部分散，又在全局聚集，同时照顾近距离和远距离的点。其性能优于任何非线性降维算法。具体实现见[在用PCA降维？快学学大牛最爱的t-SNE算法吧,  附Python/R代码](https://mp.weixin.qq.com/s/alBfj3Y08qCnZoz5JwVdaw)。

   聚类算法有[K-means](https://mp.weixin.qq.com/s/ST2SAmfKOptpJOHS8podmQ) (相似的[SOM自组织特征图聚类](https://mp.weixin.qq.com/s/fTSYs_vS_ofi71b-jNpbGA))、`SC3 (一致聚类)`,  `Seurat (图聚类)`、迭代聚类如层级聚类等。聚类的难点还在于其稳定性和聚类数目的确定，`silhouette index`是一个度量指标。
   

   ![](http://www.ehbio.com/ehbio_resource/tSNE_peking.png)

3. 单细胞分析与细胞图谱绘制，10月15日，主讲人：石强（李程组）, 链接：<https://share.weiyun.com/5kljVnj>

   以骨关节炎文章为例，展示了单细胞转录组的分析过程。从PCA结果看，细胞整体分型不明显，而且两个主成分的贡献率之和不足14%。但细胞在`PC2`维度与骨关节炎的各个阶段有些吻合，随后选择与`PC2`正贡献和负贡献的基因进行可视化展示 (一维的效果看上去优于二维)。随后是`tSNE`分型和`Pseudospace`发育轨迹分析、Marker鉴定等。可视化主要以[热图](https://mp.weixin.qq.com/s/_9LKs6t6rcjzokF_0gneSA)、[散点图](https://mp.weixin.qq.com/s/c2nwATMwyU_9FgLprqmQ5A)、[箱线图](https://mp.weixin.qq.com/s/Zvmht0kOyOf02P8jQNjaOw)为主。功能分析主要是[GSEA](https://mp.weixin.qq.com/s/3Nd3urhfRGkw-F0LGZrlZQ)。

   ![](http://www.ehbio.com/ehbio_resource/PC2_peking.png)

4. 单细胞分析与发育，10月29日，主讲人：李莉（汤富酬组），链接：链接：<https://share.weiyun.com/5p7I1Nd>

   Cell stem Cell 文章<Single-Cell RNA-Seq Analysis Maps Development of Human Germline Cells and Gonadal Niche Interactions>的一作讲坛。单细胞的分析都是套路分析，关键在于样品获取、实验的稳定性和结果的生物意义解读。本文主要围绕胚胎生殖细胞发育过程讲述单细胞转录组、甲基化组和染色质可及性的分子调控。落脚点是[调控网络](https://mp.weixin.qq.com/s/1LNae0pG0w_Q-rRxhI96Pg)和[信号通路](https://mp.weixin.qq.com/s/jI6Gz1JKxnGB9jDRSFjd0g)。

5. 单细胞多组学，11月5日，主讲人：张倩（李程组），链接：<https://share.weiyun.com/5p7I1Nd>
	
    同一个细胞，不同的调控层面。单细胞多组学有`sci-CAR`同时检测基因表达和染色质可及性，`scNMT-seq`同时检测染色质可及性、DNA甲基化和基因表达，`connect-seq`谱系追踪和转录组，在神经研究中应用较多。近来看到一篇追踪iPS重编程的工作，很有意思，回头解读下。这个视频重点在单细胞`ATAC-seq`技术的原理、应用和分析，有一部分`Cicero`的[R代码实战](https://mp.weixin.qq.com/s/EZ8R4v4f_jU3aaUP-1p1MQ)。`10X`官网有不少视频，是了解单细胞技术的好的素材。[基因组浏览器](https://mp.weixin.qq.com/s/qdKxBAU__nbq8Ua0rLCEow)是展示多组学信号的合适工具。

II. 染色质分析模块

1. 3D genome and its disorganization in diseases，11月19日，主讲人：李瑞风（李程组）链接：<https://share.weiyun.com/5p7I1Nd>

   通常人类细胞核大小为`6 um`，内有抻开后长度为`3.0 m`的`46`条染色体的`3亿`碱基对。想象一下你如何能把`3米`的绳子放在`6 um`的细胞核中，更别说DNA上还有组蛋白的结合。染色体在细胞核内高度压缩缠绕，各自占有自己的一部分空间称为`chromosome territories`。早期通过`FISH`技术鉴定，现在有`Hi-C`、`ChIA-PET`、`OCEAN-C` (李程老师组2018年发表，可同时检测TAD，compartment和开放染色质区域)等。3D基因组的3个层面：`Compartment` (A: 开放的活性区域，B致密的沉默区域， 10 Mb尺度)，`TAD` (拓扑结构域，1 Mb尺度，不同物种和细胞系之间相对保守，与常见组蛋白修饰、CTCF结合关联较好)，`Loops` (300 kb尺度，介导[enhancer-promoter](https://mp.weixin.qq.com/s/2wSNDuz9CtC1ym1QvWHcPg)互作等, 细胞系之间变化较大)。

   后面是一作讲坛，结合李程老师组Nature communication发表的关于多发性骨肉瘤的3D结构失调展示TAD与CNV的关系。3D基因组应用的一个例子还是趾的发育，这是增强子功能的经典案例，也是Cell和媒体的常客。	

   ![](http://www.ehbio.com/ehbio_resource/3Dgenome_peking.png)

2. ATAC-seq，分析流程与案例，11月26日，主讲人：孙林华（邓兴旺 钱伟强组）链接：<https://share.weiyun.com/5p7I1Nd>

   ATAC-seq全称`Assay for Transposase-Accessible chromatin`用于检测开放的染色质区域，其基本操作是用`Transposase Tn5`切割DNA并在切点处连上接头序列，供下游分离扩增测序。实验难度低于ChIP系列的富集测序，结果具有广谱性，既可以展示核小体定位(测序片段中间部分)，也可以研究开放染色质区域(测序片段结点部分)。配合[转录因子结合Motif分析](https://mp.weixin.qq.com/s/ZUlVq6IVEqZb0KTPCFCkiw)可在一定程度起到替代ChIP-seq的作用，尤其是抗体缺失的情况下。

   这个报告讲述了ATAC-seq的原理、可用的生信分析工具、在动植物分子调控研究中的应用。ATAC-seq基本分析与[ChIP类似](https://mp.weixin.qq.com/s/nldZ1_wiCmCtLO3MWJuQ8Q)，只是根据关注的重点确定参数的选择。
   
   ![](http://www.ehbio.com/ehbio_resource/ATAC_peking.png)

3. Introduction to Hi-C experiment and data analysis，12月3日，主讲人：李梦帆（李程组）链接：<https://share.weiyun.com/5p7I1Nd>
	
   Hi-C实验和分析的系统介绍，比较详细，可以作为学习的起点。测序成本的下降，给Hi-C提供了很好的契机，测序一次浪费一半以上的`reads`，背后都是钱啊。

   ![](http://www.ehbio.com/ehbio_resource/HiC_peking.png)

4. 基于成像的染色质分析，12月10日，主讲人：侯英萍（李程组）链接：<https://share.weiyun.com/5p7I1Nd> 

   基于FISH (Fluoresence in situ hybridization)的原位DNA结构鉴定和RNA表达的原位细胞类型鉴定。配合超高分辨率显微镜加精巧的实验设计，也可以一定程度的实现高通量的所见即所得。`MERFISH`是著名华人学者庄小威教授2015年开发的大规模RNA成像技术，根据不同细胞类型表达基因的不同在原位器官鉴定细胞类型的空间分布。

   ![](http://www.ehbio.com/ehbio_resource/merfish_peking.png)

5. 染色质分析与多组学整合，12月17日，主讲人：刘玉婷（李程组） 链接：<https://share.weiyun.com/5p7I1Nd>      

   多组学整合分析本质是把不同组学鉴定出来的元件根据特征细分、分类后做图谱、做交集。其研究要么起始于文献，要么起始于对数据的观察，这里面还是基因组浏览器的作用不可忽视。观察到基本模式后，就是去写程序检测基本模式是否具有普遍性和显著性，这部分没有成熟的工具，工具组合可以提供一些帮助，最主要的是自己学些[编程](https://mp.weixin.qq.com/s/xoLBg0pI9seEksa0hMXi0A)了。(回复**生信宝典福利第一波**获取我们自写的Python、Linux、R学习教程)

6. 染色质分析中的新概念、新方法和新工具，12月24日，主讲人：贾璐萌（李程组）链接：<https://share.weiyun.com/5p7I1Nd>
  
   一作解读，`OCCAN-C`, 李程老师组2018年发表，可同时检测TAD，compartment和开放染色质区域。

III. 网上资源：

* 单细胞分析课程：<http://hemberg-lab.github.io/scRNA.seq.course/index.html> (你也可以用[bookdown](https://mp.weixin.qq.com/s/u8WfC4xQ562Uekhs4WVBoQ)整理出这样漂亮的教程)
* 单细胞分析软件集成：<https://github.com/seandavi/awesome-single-cell>
* 染色质与三维基因组分析课程：<https://github.com/hms-dbmi/3d-genome-processing-tutorial>, <https://github.com/hms-dbmi/hic-data-analysis-bootcamp>
* 染色质分析相关软件：<https://github.com/dekkerlab>，<https://github.com/theaidenlab/juicer>，<https://github.com/nservant/HiC-Pro>，<https://bioconductor.org/packages/release/bioc/html/HiTC.html>




## 暑期讨论班内容

单细胞实验与分析（2018.6-8月，这部分没有配套视频）

1. An introduction to bulk and single-cell RNA-seq：2018年6月25日，主讲人:徐子晗（李程组) 链接：<https://share.weiyun.com/5dLF79v>
2. The advances in scRNA-seq techniques: 2018年7月2日，主讲人：李莉（汤富酬组） 链接：<https://share.weiyun.com/59ryjRX>
3. Pre-processing and variation of scRNA-seq data：2018年7月9日，主讲人：石强（李程组) 链接：<https://share.weiyun.com/5bGebsN> 介绍了基本单细胞分析流程和常用工具，主要讲述了噪音的来源和校正方法。
4. scRNA-seq data analysis: Imputation,  Cluster,  and differential expression: 2018年7月16日，主讲人：李子逸（张泽民组）链接：<https://share.weiyun.com/5dN7wuZ> 单细胞分析流程概述。
5. scRNA-seq data analysis: single cell trajectory：2018年7月23日，主讲人：张倩（李程组）链接：<https://share.weiyun.com/5uXwz15>
6. From single-cell RNA-seq to transcription network：2018年7月30日，主讲人：李响（谢晓亮组）链接：<https://share.weiyun.com/5ys73Yp>。主要讲述了[WGCNA](https://mp.weixin.qq.com/s/PMb2xwADvnMwaipyFXdtzQ)的应用。
7. 定制单细胞扩增与泛组学测序：2018年8月13日，主讲人：宋立阳（谢晓亮组）链接：<https://share.weiyun.com/5TMLNAk> (单细胞扩增技术的比较)

