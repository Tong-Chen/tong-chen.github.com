---
title: 美女教授带你从统计学视角看转录组分析
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---


### 引言

分子生物学的中心法则自1958年由Francis Crick提出到今年正好60周年，它描述了“DNA制造RNA，RNA制造蛋白质”的遗传信息的标准流程 [1]。十年前，第二代RNA测序技术(RNA-seq)的诞生及其迅速发展使得研究者可以在对RNA序列没有任何先验信息的情况下高通量地对全转录组进行测序 [2]。现如今第二代RNA测序技术已经成为了研究基因和RNA表达最常用的手段之一，它的广泛应用极大地促进了生物和医学领域的各类研究，包括对基因表达与调控，RNA可变剪切以及蛋白质翻译等多项生物过程的了解 [3]。具体见[生信老司机以中心法则为主线讲解组学技术的应用和生信分析心得](https://mp.weixin.qq.com/s/mlBLxXLabSU6FflOFXrzrw)。

为了回答各种生物问题，十年来不同领域的研究者已为第二代RNA-seq数据分析提出了超过2000种计算与分析方法 ([39个转录组分析工具，120种组合评估(转录组分析工具哪家强-导读版)](http://mp.weixin.qq.com/s/NUEi6oRFL7B3f1FpCD4Xug))。近日，加州大学洛杉矶分校（UCLA）的李婧翌（Jingyi Jessica Li）教授和她的学生李维（Wei Vivian Li）第一次从统计建模与分析的角度对第二代RNA测序数据的计算方法进行了总结和讨论，发表在最新一期的**Quantitative Biology**期刊中（Modeling and analysis of RNA-seq data：a review from a statistical perspective）[4](点击文末“阅读原文”下载英文版全文)。该综述文章从四个层面（样本，基因，转录本，和外显子选择）对RNA-seq数据的分析方法进行了总结，旨在归纳看似不同的方法背后共通的统计假设和模型。生信宝典之前的总结在 [转录组分析的正确姿势](https://mp.weixin.qq.com/s/h3wEMUoRNKMFVLDLDFXNoA)



![基因组浏览器、热图、定量、差异分析和可变剪接](http://www.ehbio.com/ehbio_resource/QBRNAseq_4level.png)

### 样本分析层面：样本相似性度量

作者首先从样本分析层面上讨论了如何利用RNA-seq数据对来自同种或者不同物种的多种细胞类型的样本进行比较，从而研究基因表达机制在物种进化过程中的分化和保守现象。这就需要用到样品间的相似性度量来检测`异常样品`，进行`样品聚类`、`样品分类`和`新细胞类型`分析。

`Pearson`和`Spearman`相关系数是最常用的计算相似性的度量，配合[热图](https://mp.weixin.qq.com/s/_9LKs6t6rcjzokF_0gneSA)展示。但这种通过相关性推测转录组相似性的方式容易受**持家基因**的影响，并且相关性测量依赖于表达值的精确计算，信噪比低时结果稳定性差。

作者提出了TROM (Transcriptome overlap measure)的计算方式，采用"`associated genes`"而不是全部基因计算相关性。`associated genes`是指那些在样品间归一化得到的`Z-score`的值高于系统检测的阈值的基因。`z-score`计算见[R语言 - 热图美化](http://mp.weixin.qq.com/s/lKrhvYrwn93esC6MA3bHWw)。作者也提供了R包`TROM`进行计算, 获得`associated genes`和进行`overlap test`，获得格式类似于相关性矩阵的TROM得分矩阵，用于后续分析。

另外还有其他度量方式，如偏相关系数 (`partial correlation coefficient`)指消除批次效应或其它影响因素后的相关性；

考虑到RNA-seq样品之间并不是线性相关的，信息论中的互信息(mutual information)可以计算非线性相关性。其它类似的还有条件互信息(conditional mutual information)。这些主要用在基因调控网路的构建上。具体见<https://rdrr.io/cran/synRNASeqNet/man/parMIEstimate.html>和<Gene Regulatory Network Inference from Single-Cell Data Using Multivariate Information Measures>。

直接降维的手段，如PCA、t-SNE和MDS, 见之前的文章：([一文看懂PCA主成分分析](https://mp.weixin.qq.com/s/ZKvQieq_6KX6l6LZyUz7jA), [还在用PCA降维？快学学大牛最爱的t-SNE算法吧,  附Python/R代码](https://mp.weixin.qq.com/s/alBfj3Y08qCnZoz5JwVdaw))。 

### 基因层面：基因表达动力学

其次，在基因分析层面上，作者着重讨论了两种最常见的基因表达数据分析：基因差异表达分析和基因共表达网络分析。

基因差异表达分析通过统计学的假设检验理论来研究哪些基因在不同条件下(比如实验组和对照组)存在差异表达。常用的数据标准化方法如`FPKM/RPKM/TPM`，是一种定量方式，一般可比，但也会有`protocol`特异的偏好。一般不用于差异基因检测。

![](http://www.ehbio.com/ehbio_resource/FPKM_TPM.png)

基于分布的标准化方式：如DESEq, DESeq2, TMM和quantile normalization等，基于不同样品基因表达水平分布相似的原则进行计算。具体计算如下（代码比文字易于理解）。

![](http://www.ehbio.com/ehbio_resource/distribution_normalization.png)

基于基因的标准化方式是使不同样品间非差异基因或持家基因的表达水平一直，如`PoissonSeq`。

基于最广泛使用的Negative Binomial模型概括了检验基因差异表达的6个核心步骤：估算基因表达和离散度，估算样品间差异统计量，推导H0下的统计量，计算每个基因的统计了，计算P-value，多重假设检验校正。操作见[DESeq2差异基因分析和批次效应移除](https://mp.weixin.qq.com/s/Vmhx_TGxNkQzkekf93Xl4w)。

基于log转换后的基因表达符合正太分布的模型，如`voom` (线性模型分析多因素设计，定量加权解释表达变化，经验贝叶斯估算)和`sleuth`(log转换的基因表达作为线性模型的响应变量，拆解为3个成分：样品间差异、生物自然噪音、推测噪音，通过bootsrap-test估计零假设和计算p-value)。

注意点：重复次数，FDR，没有方法是最优的，时间序列数据使用`maSigPro`或`multivariate empirical Bayes statistic (MB statistic)`。

**基因共表达网络分析**: 建立基因的共表达关系，推测未知基因的功能。常用的有WGCNA，检测共表达基因簇和模块。具体见[WGCNA分析，简单全面的最新教程](https://mp.weixin.qq.com/s/PMb2xwADvnMwaipyFXdtzQ)。


### 转录本分析层面： 重构和量化全长转录本

在转录本分析层面上，大部分研究的重心在于通过重建和量化全长转录本来研究可变剪切在细胞分化和疾病发展等过程中的作用。这两项任务（重建和量化）对于包括人在内的复杂生物体来说仍然非常困难，因为第二代测序技术一般产生的是不超过300个碱基（ bp）的短片段(reads),  但人体内全长转录本的平均长度在1700 bp左右，而短片段导致的信息损失只能依靠统计建模来推断和弥补。作者将现有的转录本量化方法分为两类：基于极大似然分析或基于回归分析。前者将转录本表达量作为参数建立混合概率模型(mixture model)，通过最大化似然函数来求解最优参数估计。后者将转录本表达量作为系数建立回归模型，通过数据拟合来求解最优系数估计。这里面涉及的软件有`Cufflinks`, `Stringtie`, `Salmon`,  `Kallisto`, `RSEM`等，其性能评估见[39个转录组分析工具，120种组合评估(转录组分析工具大比拼 （完整翻译版）)](http://mp.weixin.qq.com/s/xAaj-d5LRRj0SSMFJ7Yo9Q)。

### 外显子分析层面：计算单个外显子的PSI**

在外显子分析层面上，研究重心在于量化单个外显子在可变剪切的过程中存留在全长转录本中的可能性 (percentage spliced in,  PSI)，是一个较为可靠的可变剪接分析方式。常用工具有`MISO`和`rMATS`。基因组浏览器在此有重要的应用，可视化的reads分布模式对应研究不同可变剪接是必须的，从图谱看到差异，再设计工具寻找差异。

* [测序数据可视化 (一)](http://mp.weixin.qq.com/s/8EqULhLCyNttijO9bUm0BQ)
* [IGV基因组浏览器可视化高通量测序数据](http://mp.weixin.qq.com/s/vWQUNgVujCTdZgZZ2_AZfQ)
* [高通量数据分析必备-基因组浏览器使用介绍 - 1](https://mp.weixin.qq.com/s/_5zoRvjku5pb9qtwrvlWYw)
* [高通量数据分析必备-基因组浏览器使用介绍 - 2](https://mp.weixin.qq.com/s/uzyccMorR6XWqjMsMd3Oaw)
* [高通量数据分析必备-基因组浏览器使用介绍 - 3](https://mp.weixin.qq.com/s/qdKxBAU__nbq8Ua0rLCEow)


文章的最后作者对RNA-seq统计建模过程中仍然存在的难点进行了总结，并简要讨论了RNA-seq在RNA编辑和非编码RNA等相关问题中的应用。近年来兴起的单细胞RNA测序技术将转录组研究提高到单细胞精度，也给新数据的统计建模带来了新的机遇和挑战，可以参考`The Human Cell Atlas White Paper`了解更多。

### 附上两个完整的分析流程

![](http://www.ehbio.com/ehbio_resource/ref_salmon.png)

![](http://www.ehbio.com/ehbio_resource/ref_map1.png)



本文主要是帮助师姐推荐QB杂志，如对这篇文章原文有任何疑问欢迎联系QB微信号：13269084698，或直接在文末留言，QB将邀请作者为您解答。） 

参考文献

1.      Crick,  F.H.C. (1958). " On Protein Synthesis" . In F.K. Sanders. Symposia of the Society for Experimental Biology,  Number XII: The Biological Replication of Macromolecules. Cambridge University Press. pp. 138–163.
2.      Mortazavi,  A.,  Williams,  B.A.,  McCue. K.,  Schaeffer,  L.,  and Wold,  B. (2008). " Mapping and quantifying mammalian transcriptomes by RNA-Seq" . Nature Methods. 5 (7): 621–8.
3.      Ozsolak,  F. and Milos,  P.M. (2011). " RNA sequencing: advances,  challenges and opportunities" . Nature Review Genetics. 12 (2): 87–98.
4.      Li,  W.V. and Li,  J.J. (2018). “Modeling and analysis of RNA-seq data: a review from a statistical perspective”. Quantitative Biology. 6 (3): 195–209.

