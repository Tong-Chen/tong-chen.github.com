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

为了回答各种生物问题，十年来不同领域的研究者已为第二代RNA-seq数据分析提出了超过2000种计算与分析方法 ([39个转录组分析工具，120种组合评估(转录组分析工具哪家强-导读版)](http://mp.weixin.qq.com/s/NUEi6oRFL7B3f1FpCD4Xug))。近日，加州大学洛杉矶分校（UCLA）的李婧翌（Jingyi Jessica Li）教授和她的学生李维（Wei Vivian Li）第一次从统计建模与分析的角度对第二代RNA测序数据的计算方法进行了总结和讨论，发表在最新一期的**Quantitative Biology**期刊中（Modeling and analysis of RNA-seq data：a review from a statistical perspective）[4](点击文末“阅读原文”下载英文版全文)。该综述文章从四个层面（样本，基因，转录本，和外显子选择）对RNA-seq数据的分析方法进行了总结，旨在归纳看似不同的方法背后共通的统计假设和模型。生信宝典之前的总结在 [转录组分析的正确姿势](https://mp.weixin.qq.com/s/h3wEMUoRNKMFVLDLDFXNoA)。



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

配合Cytoscape使用更佳：

* [Cytoscape教程1](http://mp.weixin.qq.com/s/m9uJm8GwSXb3xaRxtod08Q)
* [Cytoscape之操作界面介绍](http://mp.weixin.qq.com/s/ZSoW7-qWs3BuSB7bkDnfmA)
* [新出炉的Cytoscape视频教程](http://mp.weixin.qq.com/s/sKEy_Pn9qnWw4W-aXraA5g)
* [Cytoscape制作带bar图和pie图节点的网络图](https://mp.weixin.qq.com/s/AzCxP1AP04hsvKT7j_SpTw)

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

<mark>本文主要是帮助师姐推荐QB杂志，如对这篇文章原文有任何疑问欢迎联系QB微信号：13269084698，或直接在文末留言，QB将邀请作者为您解答。</mark>

### 附上两个完整的分析流程

![](http://www.ehbio.com/ehbio_resource/ref_salmon.png)

![](http://www.ehbio.com/ehbio_resource/ref_map1.png)

### 转录组分析培训班第4期

在广大粉丝的期待下，《生信宝典》联合《宏基因组》在**2018年11月16-18日北京鼓楼**推出《**转录组数据分析**》专题培训第四期，为大家提供一条走进生信大门的捷径、为同行提供一个转录组实战分析学习和交流的机会、助力学员真正理解分析原理和完成实战分析，独创四段式教学(3天集中授课+自行练习2周+再集中讲解答疑+上课视频回看反复练习)，**"教—练—答—用"四个环节统一协调，真正实现独立分析大数据**。

关于学习生物信息学分析的重要性，请阅读[《生物信息9天速成班—成为团队中不可或缺的人》](http://mp.weixin.qq.com/s/1nf7vwyvC3oemkTq_pu87A)。

本课程一共3天，每天6节课，共18节课，全部课程均理论与实战结合(只要课上讲的都是可以带你自己实现的分析)。从分析平台搭建、Linux和R基础、图表解读和实战、转录组设计、分析标准流程、差异基因分析、功能富集分析、及各类高级分析(差异剪接、WGCNA分析、通路图绘制等)，和CNS级图片修改排版。3天时间，老司机带您完成自学需要3个月甚至是1年的崎岖之路，助力您真正玩转转录组分析。

### 课程大纲

每节课1小时一个主题，理论结合实战，学懂原理，实战实操，全是老司机多年经验和代码的无私分享。下面是课程安排，如11代表第一天第一节课，26代表第二天第六节课，41为两周后的线上集中视频答疑。这次课程重点做了调整，**侧重后期高级分析**，弱化流程性分析。

编号 | 主题 | 简介
---|---|-
11|转录组概述|转录组设计、应用、批次效应等
12|转录组分析流程简介|基于/不基于比对的分析流程讲演
13|转录组流程配置|Linux下一键配置转录组分析工具集
14|Salmon定量实战|不基于比对直接定量基因和转录本的表达
15|STAR/HISAT2比对定量实战|比对定量和比对质量评估
16|转录组分析案例|转录组分析案例 
21|二代三代测序原理介绍|建库测序过程及注意事项
22|差异基因分析|DESeq2差异基因分析
23|富集分析|GO/GSEA富集分析
24|WGCNA分析|基因加权共表达网络分析
25|Cytoscape绘制网络图|Cytoscape绘制共表达网络和调控通路网络图
26|常见图表解读|常见图表解读和Illustrator制作CNS标准图版
31|基因表达资源数据库|在线查询多组织器官基因表达，癌症特意表达基因筛选
32|可变剪接分析|差异剪接分析
33|无参转录组组装和注释|无参转录组组装和注释
34|多组学分析示例讲解|多组学分析示例讲解
35|考试、圆桌论坛|自评学习效果、知识点回顾
41|答疑-线上|答疑、考试内容串讲

**教程内容简介如下：**

### 转录组的应用、设计和案例分享

![](http://www.ehbio.com/ehbio_resource/Transcriptome_product.jpg)

1. 转录组学研究技术介绍
2. 转录组学实验设计和测序原则、注意事项
3. [二代](https://mp.weixin.qq.com/s/SS9YBSpgUoU9gI86u-0ATg)、三代测序过程和原理解析
4. 转录组学文章案例分析
5. 在线基因表达资源数1据库

### 转录组分析流程实战

![](http://www.ehbio.com/ehbio_resource/Transcriptome_flow.png)

1. [转录组分析流程评估](https://mp.weixin.qq.com/s/NUEi6oRFL7B3f1FpCD4Xug)
2. [测序数据质量评估和清洗](https://mp.weixin.qq.com/s/tDMih7ISLJcL4F4sWBq3Vw)
2. 不基于比对的[差异基因分析](https://mp.weixin.qq.com/s/Vmhx_TGxNkQzkekf93Xl4w)
3. 基于比对的差异基因分析
4. 转录本组装和选择性剪接分析
5. [目标基因GSEA/GO富集分析](https://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg)

### 常见图表解读和图形编辑排版

在培训上，结合发表高水平文章，进一步讲解16种常用分析图的原理和使用范围，让你不仅读懂图，更知道如何应用于自己的研究，并亲自轻松完成绘图。

针对大家使用R语言绘图学习时间成本较高的问题，易生信团队针对常用16种图开发了[免费绘图网站](https://mp.weixin.qq.com/s/MnM_MyosBdEvKV0W018KeA)，一键出图，更可鼠标点选参数修改图形的个性样式。

成果发表是科研过程中不可缺的一部分，发表成果又少不了图形展示。文章图表排版是否整齐规范、协调一致、重点突出对一篇文章的发表也是有不少贡献的。之前推出的[文章发表图的修改和排版](https://mp.weixin.qq.com/s/IJNyhinakY0lSXgCN7b9ug)讲演了部分图形编辑和排版操作，本次培训也会实践从原始图形、到细节修饰再到排版发表的整个过程和注意事项。

### 转录组高级分析

![](http://www.ehbio.com/ehbio_resource/WGCNA_flow.png)

1. [WGCNA基因共表达分析](https://mp.weixin.qq.com/s/PMb2xwADvnMwaipyFXdtzQ)
2. WGCNA基因、表型关联分析
3. [Cytoscape 共表达网络](https://mp.weixin.qq.com/s/sKEy_Pn9qnWw4W-aXraA5g)绘制
4. 转录组常见图形在线绘制
5. [KEGG/Reactome通路图绘制](https://mp.weixin.qq.com/s/jI6Gz1JKxnGB9jDRSFjd0g)，表达映射
6. [基因互作的文献挖掘和数据库挖掘](https://mp.weixin.qq.com/s/1LNae0pG0w_Q-rRxhI96Pg)展示
7. 其它高级分析

### 生信基础知识

1. Linux/Windows下Rstudio和Linux命令的使用
2. Linux/Windows下转录组分析流程的搭建

生物学家必要掌握的[Shell](https://mp.weixin.qq.com/s/rXjQfyEX2FnuW9HTM_Uc8Q)和[R语言](https://mp.weixin.qq.com/s/EZ8R4v4f_jU3aaUP-1p1MQ)基础知识。

(如果基础薄弱，报名付款成功后，可免费**领取[基础程序课](https://ke.qq.com/course/289264)**，做好准备工作, [让程序成为我们的得力工具而不是学习新知识的绊脚石](http://mp.weixin.qq.com/s/u8AmzvO0-PIS33ficKOrUQ)。)

### 定制内容

如果您看到文章中有哪些图或分析工作需要重现，也请提出，一起讲述。

如果您有其它关注的问题，也请报名时提出，把这次课程变成您的**定制讲解**。

### 120分的转录组试题来测试下

* [120分的转录组试题（第一份答案）](https://mp.weixin.qq.com/s/lsaubsJofGRbCVnrhmTygw)
* [120分的转录组试题（第二份答案）](https://mp.weixin.qq.com/s/Vh2c-JegoaMr0Ws2gDuFhA)
* [120分的转录组试题（第三份答案）](https://mp.weixin.qq.com/s/BadU3ZVPAlxBn0_QehVnXQ)


### 往期精彩回顾

![image](http://bailab.genetics.ac.cn/markdown/train/1809/41.jpg)
![image](http://www.ehbio.com/Training/Public/assets/images/sandai.jpg)
![image](http://www.ehbio.com/ehbio_resource/%E4%BA%8C%E4%BB%A3%E4%B8%89%E4%BB%A3%E8%BD%AC%E5%BD%95%E7%BB%84%E6%B5%8B%E5%BA%8F_%E8%85%BE%E8%AE%AF%E8%AF%BE%E5%A0%82_%E8%AF%84%E4%BB%B7.png)


### 主讲教师


陈同，博士，2015毕业于中科院遗传与发育生物学研究所，生物信息专业博士，在Cell Stem Cell(IF=23.2，第一作者兼封面文章)，Nucleic Acids Research，Stem Cells and Development等高水平杂志以第一作者或主要作者发表文章，运营有数万人关注的[《生信宝典》](https://mp.weixin.qq.com/s/2b3_8Vvv7McqCkEfUszW3A)微信公众号，给你不一样的学习生信体验。 


刘永鑫，博士。2008年毕业于东北农大微生物学专业。2014年中科院遗传发育所获生物信息学博士学位，2016年博士后出站留所工作，任宏基因组学实验室工程师，目前主要研究方向为宏基因组学数据分析与可重复计算。发表论文10余篇，SCI收录7篇。2017年7月创办[“宏基因组”公众号](https://mp.weixin.qq.com/s/oa1M7FZ7f4PUtIsE5QZdMA)，目前分享宏基因组、扩增子原创文章185篇，关注人数2.3万人，累计阅读近300万次。

### 助教团队

十余名中国科学院、清华、北大博士(含在读)，轮值讲师和助教，辅助学员学习和矫正培训过程中不足的点。 

### 授课模式

本课程以讲解流程和实际操作为主，采用独创四段式教学，封装好的代码全部分享，随处可用：

- 第一阶段 3天集中授课；
- 第二阶段 自行练习2周；
- 第三阶段 在线直播答疑；
- 第四阶段 培训视频继续学习；
- 实现教-练-答-用四个环节的统一协调。

### 培训时间

2018-11-16 到 2018-11-18 (线下讲解实战)  
每天早9点到晚6点，半封闭式教学 (最后1小时为集中讨论时间，最后一天会稍微提前一些，多留出时间讨论，也方便老师乘车返回)  
报到时间：提前一天或者当天都可以


### 授课地点

北京市西城区鼓楼明德大厦 (北京市旧鼓楼大街47号院2号楼2010)。 

### 课程价格

1. 截止 2018-11-10  4199 元/人
2. 名额有限，每次课程报名满40人后自动关闭报名通道
3. 提供易汉博基因科技实习机会或工作机会

### 课程福利

1. 座位按报名并**缴费或预付款成功**顺序从前到后龙摆尾式排序 
2. 赠送程序基础课和对应课程往期视频课一份 (http://bioinfo.ke.qq.com)
3. 多人 (N，10>N>1) 组团报名并同时缴费，每人还可减免**N-1**百元 (最高500)
4. 赠送金士顿U盘一个（32G含培训数据和脚本）
5. 附推荐语分享对应的招生信息到朋友圈，截图发到train@ehbio.com 可获得**200元**生信宝典腾讯课堂课程优惠券（可拆分供多个课程使用）

**注意事项** *

1. 需自备笔记本电脑，推荐使用win10系统，4G以上内存(推荐8G)。课程实践根据需要会提供云计算平台
2. 培训班所有数据，文档为内部资料，仅供参阅，未经允许不得翻印外传登刊
3. 上课期间禁止录音，录像
4. 成功付款的学员，若临时有紧急事情不能到来的，可申请延期，更换后续培训班；也可申请退款
5. 若开课2周 (含) 前申请退款可退还85%费用；开课3个工作日 (含) 前申请退款退还70%的费用 (若已开发票需承担相应手续费)
6. 不可先延期再退款
更多课程的详细介绍，请扫描下方二维码。

![image](http://bailab.genetics.ac.cn/markdown/train/1809/easy_bio_qr.png)

![image](http://bailab.genetics.ac.cn/markdown/train/1809/201807.jpg)

复制以下链接
http://www.ehbio.com/Training/ 或
点击**阅读原文**跳转报名页，成为实验中不可或缺的人，赶快报名吧！


参考文献

1.      Crick,  F.H.C. (1958). " On Protein Synthesis" . In F.K. Sanders. Symposia of the Society for Experimental Biology,  Number XII: The Biological Replication of Macromolecules. Cambridge University Press. pp. 138–163.
2.      Mortazavi,  A.,  Williams,  B.A.,  McCue. K.,  Schaeffer,  L.,  and Wold,  B. (2008). " Mapping and quantifying mammalian transcriptomes by RNA-Seq" . Nature Methods. 5 (7): 621–8.
3.      Ozsolak,  F. and Milos,  P.M. (2011). " RNA sequencing: advances,  challenges and opportunities" . Nature Review Genetics. 12 (2): 87–98.
4.      Li,  W.V. and Li,  J.J. (2018). “Modeling and analysis of RNA-seq data: a review from a statistical perspective”. Quantitative Biology. 6 (3): 195–209.

