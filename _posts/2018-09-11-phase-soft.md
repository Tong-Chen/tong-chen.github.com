---
title: 引起相变的无序结构域（IDRs）怎么预测？跟踪热点，提升文章档次！
author: lld
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

蛋白研究过程中，一般认为氨基酸的序列决定了蛋白的结构，结构决定功能（一般指蛋白的三维结构）。然而，近50年的研究中，有一种没有特定三维结构的蛋白不断被研究人员发现，由于这类蛋白无法折叠成稳定的三维结构而称为固有无序蛋白(intrinsically disordered regions，IDRs)。这类蛋白虽然缺乏稳定结构且高度可变，但是研究却发现他们在生物体内行驶着重要的生物学功能。

尤其是最近**相变**频繁登上CNS主刊，越来越多认识到IDRs在**相变**中的重要作用。[2018 Cell系列相变最强综述，未来已来，你在哪？](https://mp.weixin.qq.com/s/32bCVOkYwKqDufdpmFp0pg)


1. 相位分离在多种细胞过程中起作用，包括形成经典的无膜细胞器、信号复合物、细胞骨架和许多其他超分子组装。
 
2. 相位分离的概念为理解序列简并（低复杂性）和蛋白质无序区域的功能提供了新的研究方向。
 
3. 越来越多的证据表明，相变和无膜细胞器的失调在蛋白聚集相关的人类疾病中发挥关键作用。
 
4. 理解蛋白质相位分离背后的物理原理和分子互作机制可促进新型生物材料的研发。


IDRs的存在，使得蛋白更容易形成液滴状，诱发相变生成和调控的发生。还在做经典生物调控的你，如果能关联下**相变**，可能既能更好的解释细胞中的调控作用（毕竟细胞不是我们平常见到的溶液，其极度粘稠的特性诱发不同的调控规则），又可以跟踪热点，提升下文章档次。

### 相变IDRs预测

我们推荐一款工具，**MetaDisorder**（http://iimcb.genesilico.pl/metadisorder/），一个整合了多种meta-method方法的蛋白无序预测平台，操作简单，**只需2步**，就可以预测研究的目标蛋白是否有可能参与相变，再决定是否进行后期的验证。

其使用方式如下图：

![](http://www.ehbio.com/ehbio_resource/IDRs/metadisorder.png)

按照格式要求输入氨基酸序列后，点击`submit`，跳转结果页面，点击`Graphicial format`查看图形可视化的结果，点击`Simple text format` 查看文本化的结果。

![](http://www.ehbio.com/ehbio_resource/IDRs/metadisorder3.png)

可视化结果仅展示了4种MetaDisorder相关的结果，关于其它多种预测算法的结果点击`右侧灰色图例`显示。

![](http://www.ehbio.com/ehbio_resource/IDRs/metadisorder2.png)

MetaDisorder由于用到的方法多，运行会比较慢。如果特别着急，也可以使用下面的在线分析工具`DISOPRED`（http://bioinf.cs.ucl.ac.uk/psipred/?disopred=1），这是综合评估单款最优的预测工具。

用户可以在线提交蛋白质序列，执行特定的预测，并可通过邮件接收预测结果。这样可以很方便地得到一个蛋白质序列的非结构区域信息，能够为蛋白质特征分析提供更多的信息。工具的使用方法在`Help & Tutorials`页面有详细的图文介绍。


![](http://www.ehbio.com/ehbio_resource/IDRs/help.png)


除了在线分析平台，DISOPRED也有软件版，供大批量蛋白结构的预测（软件下载地址：http://bioinfadmin.cs.ucl.ac.uk/downloads/DISOPRED/）。一般下载使用最新版`DISOPRED3.16.tar.gz`。

![](http://www.ehbio.com/ehbio_resource/IDRs/disopred_software.png)

如果你的目标蛋白正好有这么一段IDRs，可以试试检测是否有**相变**的存在。如果对相变不熟，还是先建议阅读 [2018 Cell系列相变最强综述，未来已来，你在哪？](https://mp.weixin.qq.com/s/32bCVOkYwKqDufdpmFp0pg)。

关于IDRs，如果还想了解更多，请继续阅读。

### IDRs的研究历史

随着IDRs不断被发现，人们对其功能有了深入了解。IDRs在调节转录、翻译、细胞信号转导、蛋白质磷酸化、小分子存储，以及对大的多蛋白复合体(如细菌鞭毛及核糖体)自组装的调控等各方面都发挥着重要作用。

如我们熟知的DNA结合转录因子(TF)，其激活结构域(activation domain, AD)中便包含了固有无序化的低复杂序列结构域，在真核生物基因转录阶段起着至关重要的作用。在真核生物中，大约有三分之一的蛋白已被鉴定包括长度超过30个残基的无序区域，且有75%的哺乳动物信号蛋白存在无序区域。

同时IDRs也是许多**疾病**相关的位点，由于在编码无序区发生的染色体异位依然能保证折叠结构域的完整性，从而会产生功能异常的融合蛋白，引发疾病。

可见IDRs是真核生物蛋白质组中的重要组成部分，并在生命体的生长发育各个阶段起到重要的调控作用。对这类蛋白质的结构、功能、进化特征的认识和蛋白无序区域的预测，有助于我们更深层次地理解无序蛋白质的功能及其参与重要生理病理过程的分子机制。

如果预测到这些IDRs的存在，那么就可以对感兴趣的突变和相互作用进行建模，以了解它们如何影响蛋白质结构和相变发生，并确定哪些结构域可能适合于进一步实验调查。


![](http://www.ehbio.com/ehbio_resource/IDRs/Number.png)

<center>1990-2014年，PubMed中关于固有无序/非折叠蛋白报道的数量</center>
<center>（在PubMed中可通过输入`intrinsically disordered`, `intrinsically unstructured`, `natively unfolded`, `intrinsically unfolded and intrinsically flexible`等进行搜索）</center>

### IDRs预测方法


由于固有无序蛋白结构的不稳定性，很难通过实验手段使他们纯化结晶以得到可靠的实验数据，尤其是大规模地进行无序蛋白质结构测定更是十分困难。因此，各种IDRs预测软件快速发展起来，并通过每两年举办一次的蛋白质结构预测比赛(critical assessment of structure prediction，CASP)来评估各种预测软件的准确率。从CASP5开始加入了对无序蛋白质的预测，目前已经举行到CASP12(2016年)，CASP13（2018年）比赛正在进行中（有兴趣的小伙伴可查看官网了解比赛：http://predictioncenter.org/casp13/index.cgi）

<center>表1 部分固有无序蛋白预测工具展示</center>


![](http://www.ehbio.com/ehbio_resource/IDRs/list1.png)

![](http://www.ehbio.com/ehbio_resource/IDRs/list2.png)

这些预测方法可分为四大类：

**1. Sequence based**

依赖人工神经网络 (artificial neural networks，ANNs)、支持向量机(support vector machines，SVMs)等机器学习方法开发的算法。

例如1997年Romero等开发的第一个无序区域预测的工具`PONDR VL-XT`，它是基于`PDB`数据库中67个无序区域 (1340个残基)和一些有序区域(16 543个残基)建立的一种“双层前馈式神经网络”，首次表明单纯从氨基酸序列可以预测无序区域。

之后利用计算技术开发了一系列的算法，如`PONDR VL3`、`DISOPRED2`、`POODLE-L`等。

第一类算法的缺点是不能很好地揭示潜在的序列性质。

**2. clustering**

该方法通过使用蛋白一级序列生成三级结构模型，并将模型彼此叠加以鉴别蛋白高度可变区域。这个方法建立在理论上，认为序列的位置在多个模型中应该是保持一定的秩序规则，然而变化的残基可能是无序的。`intFOLD`和`DISOclust`便是基于此方法的预测工具。

由于聚类方法不依赖于训练数据集，因此这种方法可能不太能显示关于无序区域长度的偏差。

**3. template based**

与聚类方法类似，基于蛋白的一级序列与已知的同源物做比对。如`PrDOS`就是基于此方法的预测工具，同时也可以基于氨基酸序列做预测。这个方法认为，蛋白内在无序区域在蛋蛋白家族中应该是保守的，通过结合氨基酸序列的预测和同源比对的方法，`ProDOS`也可划分到第四种预测方式`meta-predictor`中。

**4. meta-predictor approaches**

基于参考多个无序预测工具的结果对蛋白做进一步预测。使用该方法的一个例子是`metaPRDOS`，该工具整合了八种不同单独预测方法的结果。`meta-predictor`可以提高预测的准确性，因其预测结果比较可靠而常将结果作为数据库填充的来源。如`MobiDB`数据库，利用多种无序预测手段的结果，整合了来自`PDB`和`DisProt`的无序蛋白质。`MobiDB`数据库中的每种蛋白，是基于**10种**无序预测方法的结果和`NMR / X`射线数据来挑选的。


### 预测工具性能评估

为了测试各工具之间的效果差异，Jennifer D. Atkins 等人用已知结构的心肌肌肉LIM蛋白（**MLP**）进行检验。已知MLP的中心区域含长的无序区域，且`N`-末端和`C`-末端都含有一定程度的无序区域。

![](http://www.ehbio.com/ehbio_resource/IDRs/MLP.png)

PDB条目2o10（残基7-66）和2o13（残基119-176）仅解析了具有部分接头序列的LIM结构域。2o10中残基1-6、72-83和2o13中的残基179-187也可能是接头序列，而残基109-112,136,137,143,156,163和183-184在2o13内未被发现。这表明这七个残基加上位于66位之后的残基可能是无序区域而没有被解析到。此外，66和119之间以及176-194之间的区域可能包含无序区域。基于此已知条件，将MLP提交给各预测工具，下表便是各个预测工具的预测结果。

<center>表2 利用不同预测软件心肌肌肉LIM蛋白(MLP)无序区预测结果的比较</center>

![](http://www.ehbio.com/ehbio_resource/IDRs/table2.png)

从上表中其实很难确定到底哪个工具预测最准确，因为所有的预测结果都不一样，甚至有些软件的预测结果与其他结果相差甚远。这体现了独个工具分析的局限性，也说明我们需要同时使用多个工具来尽可能清楚地解析给定序列中无序区域存在的可能性。

有研究者用其他已知结构的蛋白质做过类似的比较，得到了相似的效果，即不同的预测工具间结果存在不同程度的差异。基于前人的研究经验得出，`DISOPRED`似乎是比较可靠的预测方法，其**预测最接近已知的无序区域**。

我们不应单独使用某个预测软件，每个工具都有缺点和优点。尽管我们不能保证预测软件能100%地为我们提供正确的结果，但这些结果确实为我们提供了IDRs的较精准估计，从而使我们了解到一些无法通过实验得到的IDRs结构。

由上可知目前对IDRs的研究还存在诸多难题，由于结构不稳定而无法通过实验手段进行可靠的研究，就算有了众多的预测软件，但是也存在一定的局限性。机遇与挑战并存是生物研究中的常态，希望终有一天科学家们会揭开生物体内这些不同寻常的蛋白域的功能。如果有精力，开发这么一款软件和数据库也会对大家很有帮助。

### 参考文献

[1] 马冲, 杨冬, 姜颖等. 无序蛋白质的判定及其结构、功能和进化特征[J]. 生物化学与生物物理进展, 2015, 42(1): 16-24.
[2] Jennifer D. Atkins. Disorder Prediction Methods, Their Applicability to  Different Protein Targets and Their Usefulness for Guiding Experimental Studies [J]. Int. J. Mol. Sci. 2015, 16, 19040-19054.

