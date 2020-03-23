---
title: 无参转录组工具评估和流程展示
author: ct
layout: post
categories:
  - Bioinfo
tags:
  - Bioinfo
---

## 无参转录组分析工具评估

研究人和小鼠类似的基因组注释比较完善的物种，是比较舒服的。想用什么数据，就可以找到什么数据。不过更多的物种是没有基因组数据或基因组注释不完整的，这时想获得基因的序列，做差异基因的分析时，相比于花大价钱测基因组，测不同组织或处理条件下的转录组是一个物美价廉的选择。既可以获得基因序列，又可以获得表达水平。这时就需要用到转录组的重头组装分析。

前面的文章[39个转录组分析工具，120种组合评估，转录组分析不再纠结](http://mp.weixin.qq.com/s/NUEi6oRFL7B3f1FpCD4Xug)中，比较了39个常用转录组分析工具包括序列比对、序列拼装、基因表达定量和基因差异分析工具，评估出了最优的分析组合。

在同一篇Nature Communication文章中，还对无参转录组分析工具进行了评估，包括`Trinity`、`Oases`和`SOAPdenovo-Trans`。

![](http://blog.genesino.com/images/noref/smes-007.png)

不同的从头转录组组装技术性能比较。a.转录本长度的分布。不同的颜色块表示对转录本长度的分类。横轴为不同长度的转录本的数目统计。这个图用直方图可能更清晰。b. 转录本长度N10-N50值的分布。不同的从头转录组组装技术性能比较。a.转录本长度的分布。b. N10-N50值。c. 不同表达百分位数的ExN50值。与b图不同，c图是把用于评估拼装工具对低表达转录本和高表达转录本的敏感度。横轴表示样品的表达量分组，从左至右为top 10%，top 20%，...， top 90%, top 100% (全部基因)。纵轴为不同表达集合的基因的N50值。

评估结果表明：

* Trinity往往预测出更长的亚型、更多的基因和转录本，但许多转录本比较散。
* 在所有样品中，Oases获得了最高的N10-N50值，表明在检测长的亚型方面具有优势。
* SOAPdenovo-Trans在高表达基因的位置有一个峰 (较小的表达百分位数)，表明它可以更好地检测高表达转录本。
* Oases在图c的最右侧N50值较高，表明可以有效检测低表达基因。

## 无参转录组常见分析流程和结果解释

这些都是在转录本长度水平做的评估。在实际应用中，转录本拼装也不一定是越长越好，而是拼装的越完整越好，后续进行基因克隆时才会更方便。

根据我们的经验，一个完整的无参转录组分析需要包括下面几部分内容,测序质量评估，拼装质量评估，基因功能注释，表达定量，样品重复性评估，差异基因鉴定，功能富集分析，共表达基因筛选。

![](http://blog.genesino.com/images/noref/No_ref_TOC.png)

测序质量的评估具体见[NGS基础 - FASTQ格式解释和质量评估](http://mp.weixin.qq.com/s/tDMih7ISLJcL4F4sWBq3Vw)。

### 拼装质量

拼装质量评估包括前面提到的拼装长度的评估

![](http://blog.genesino.com/images/noref/unigene_len_distrib.png)

真核生物有`248`个极其保守的基因，评估拼装出的转录本对这些基因的覆盖状态，是评估拼装是否完整的一个方式。如下表所示，拼装的转录本包含了`91%`的完整的真核保守基因；如果考虑部分匹配，则覆盖了`99%`的真核保守基因。

![](http://blog.genesino.com/images/noref/noref_cegma.png)

拼装的基因与SwissProt数据库中已经注释的基因的匹配百分比。一般认为匹配度越高，越有可能拼装出的为全长序列。

![](http://blog.genesino.com/images/noref/gene_completeness.png)

拼装的基因编码框的完整性和编码的蛋白的完整性。预测编码的蛋白时不只考虑了完整读码框，还考虑到由于拼接的不完整导致只拼出部分编码序列，但根据同源比对，也可以翻译出蛋白。这样提高了能鉴定出的蛋白的比例。

![](http://blog.genesino.com/images/noref/protein_completeness.png)

### 基因功能注释

功能注释比较常见的是注释到`Gene Ontology`，从整体看拼装出的基因的功能分布。

![](http://blog.genesino.com/images/noref/unigene_GO_annotation.png)

注释到TrEMBL、Pfam、KEGG和SwissProt数据库的基因的数目

![](http://blog.genesino.com/images/noref/multiple_db_anno.png)

转录因子的家族注释

![](http://blog.genesino.com/images/noref/TF_family.png)

### 样品重复性评估和聚类

单个样品的重复性一般从比对reads数的比较，不同样品基因表达的线性比较 (MA-plot)，样品间Pearson相关系数的计算等。

![](http://blog.genesino.com/images/noref/Replicate.png)

样品整体的聚类，不同样品之间，同一样品不同重复之间的相关性比较。

![](http://blog.genesino.com/images/noref/sample_pearson_all.png)

主成分分析

![](http://blog.genesino.com/images/noref/noref_pca.png)

### 差异基因图谱

差异基因的鉴定一般使用`edgeR` (基于Count的差异基因鉴定工具的评估也在前文有过比较分析)，常用的表示方式是MA-plot和火山图。

![](http://blog.genesino.com/images/noref/de_ma_volcano.png)

另外一个就是样品特异的表达热图了。

![](http://blog.genesino.com/images/noref/matrix.10.pam.result.final.sort.xls.heatmapS.png)

### 功能富集分析

功能富集分析对于查看差异基因的功能分布，指导下一步的研究具有重要意义。

![](http://blog.genesino.com/images/noref/go_bubble_plot.png)

### 表达模式聚类分析

同样表达模式的基因可能参与到同样的功能通路里面，是预测未知基因功能的一个方式。在这个图除了展示相同变化模式(正相关)的基因，还选择了相反变化模式(负相关)的基因。这个也可以利用Cytoscape绘制正负相关网络图。

![](http://blog.genesino.com/images/noref/cluster.1.png)

### 图形绘制

上面提到的图形都可以通过往期的脚本进行绘制

* [R语言学习 - 入门环境Rstudio](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483869&amp;idx=1&amp;sn=039651fa8fa9746bee6c9139b60c268e&amp;chksm=ec0dc457db7a4d4101629f584bf291a38cea3609e3d4fc406255b2b96e6db7184462374714e0#rd"})
* [R语言学习 - 入门环境Rstudio](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483882&amp;idx=1&amp;sn=e16903b4b745a1ef51855be3824149f6&amp;chksm=ec0dc460db7a4d76a70bd4ca2d250f147225252ee963d3e577affaebeeb81dea1ff639d5e9aa#rd)
* [R语言学习 - 热图绘制 (heatmap)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483889&amp;idx=1&amp;sn=9c9970cb120ac1e976713aca558ac9bf&amp;chksm=ec0dc47bdb7a4d6d6441e36055aa075b03d5592862eae01c05761e5972b39a62cf2228b19787#rd)
* [R语言学习 - 基础概念和矩阵操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483891&amp;idx=1&amp;sn=40daf6435398c4d9a41f332e9bba4915&amp;chksm=ec0dc479db7a4d6fec413bfb90a4660eb035b440d2bbee998114f7af29e3b3338a8adf62540a#rd)
* [R语言学习 - 热图简化](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483921&amp;idx=1&amp;sn=8326bc566e945386cad27250a33a1bf6&amp;chksm=ec0dc79bdb7a4e8d28bb909994432dab9bf09346b6f64a35ec1e657cbb298f10ca20c6838ca7#rd)
* [R语言学习 - 热图美化](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483901&amp;idx=1&amp;sn=5770a863352acd8f8aec3e157131bef8&amp;chksm=ec0dc477db7a4d61e5ee49323529d5b406941f0b2ebb63a8a8e7f35b28b97ada059692671c5b#rd)
* [R语言学习 - 线图绘制](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483937&amp;idx=1&amp;sn=8368c9346ccce10121c8a7b574c12f88&amp;chksm=ec0dc7abdb7a4ebd859713b8740b53f148e3ebb5047776e9cf42f2306ab082b6b968568f2f23#rd)
* [R语言学习 - 线图一步法](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483947&amp;idx=1&amp;sn=7cf0252efff5433447507b977fcaff97&amp;chksm=ec0dc7a1db7a4eb77a269709bdf2c8ab51bcad89aa780ec0be171a333e1cb8f3cc27eff277a1#rd)
* [R语言学习 - 箱线图（小提琴图、抖动图、区域散点图）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483964&amp;idx=1&amp;sn=ee52ac37fb9a919f5c75c0abe2a49ad4&amp;chksm=ec0dc7b6db7a4ea0a51306347fc43265c41fda3eeaf4764ddc3795546371327579676cd74a38#rd)
* [R语言学习 - 箱线图一步法](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483971&amp;idx=1&amp;sn=1b40a1137ccb8b2fa1ab3eb1d0f05de9&amp;chksm=ec0dc7c9db7a4edf16ea4966b9acb7f23cd23bd6a2e59450ae11bdac899fa2fceb124264dcf4#rd)
* [R语言学习 - 火山图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483996&amp;idx=1&amp;sn=9a29d52e78e9acffeb0a78077a14f9f2&amp;chksm=ec0dc7d6db7a4ec0163259e81e4ded54875a5dd8adaafbc6975a86c71223d863627ba37801e5#rd)
* [R语言学习 - 富集分析泡泡图 （文末有彩蛋）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483978&amp;idx=1&amp;sn=e0c158c0e92375553036cc37f4987e40&amp;chksm=ec0dc7c0db7a4ed6ac593493b7d8b52f11f2feb92d24fa00d19527fbb6f95b24f7e313ef9440#rd")
* [R语言学习 - 散点图绘制](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484056&amp;idx=1&amp;sn=f9b2b4f7495b432e9294b7cbf42eaf33&amp;chksm=ec0dc712db7a4e04769d322558364b4b401b0a8153097c7252e83170e9201a31c2a7abbaf101#rd)
* [一文看懂PCA主成分分析](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484036&amp;idx=1&amp;sn=22ee356d0c9680d56dada1b777985ed2&amp;chksm=ec0dc70edb7a4e182a21475e9ddcde35b907c291549cc8c2e767be260af445ff5455aa358b04#rd)
* [富集分析DotPlot，可以服](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484063&amp;idx=1&amp;sn=f4e93d428e4910b4abbee9c0430cd170&amp;chksm=ec0dc715db7a4e0318b388ba2ab3d51677741421c42ada474a0ac6046a0699283014eae84b6f#rd)
* [R语言学习 - 韦恩图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484076&idx=1&sn=fa5af19a2a4db4b0c5c7f145bf93ca57&chksm=ec0dc726db7a4e30fe7a0492ed9ea8eb5fa1c34641b1442a2da003efde0546b30c48fde3f118#rd)
* [R语言学习 - 柱状图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484134&amp;idx=1&amp;sn=ffb41298eae74834af2f5dad05d37921&amp;chksm=ec0dc76cdb7a4e7a852ac0670532c12c690399f140a2335f640eaf01f7da26bc5480941686a9#rd)

### 寻求帮助

转录组拼装对计算资源的要求是比较大的，尤其是内存资源，一般内存的消耗与数据量是1:1的关系。即如果测序了200 G的数据，拼装需要200 G的内存。同一个物种的测序为了最大限度的拼装质量，一般采用混合拼装的方式。后续的分析也需要不断地调整。

现在社会的发展越来越强调专人专事，这么繁琐的事情就交给我们来做吧，质优价廉，在分析时间、速度和质量上都能最大化效益。

## 生信宝典，换个角度学生信

<http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484402&idx=1&sn=f214ec35ff71bc4577f884584e9c9732&chksm=ec0dc678db7a4f6e40c73a6656cd7479e4cffe603a7ed7a26ad5cca72a428c78bee152a2aaee#rd>



## 生信宝典，生物信息学习系列教程，转录组，宏基因组，外显子组，R作图，Python学习，Cytoscape视频教程

[http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg](http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg)

## 生信宝典，最好的生物信息培训课程，培训课程资料

[www.ehbio.com/Training](www.ehbio.com/Training)
