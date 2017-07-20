---
title: R 学习 - 功能富集泡泡图
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---


## 功能富集泡泡图

功能富集分析用来展示某一组基因(一般是单个样品上调或下调的基因)倾向参与哪些功能调控通路，对从整体理解变化了的基因的功能和潜在的调控意义具有指导作用，也是文章发表中一个有意义的美图。通常会用柱状图、泡泡图和热图进行展示。热图的画法之前已经介绍过，这次介绍下富集分析泡泡图, 其展示的信息是最为全面的，也是比较抓人眼球的。

做基因功能富集分析、KEGG富集分析、GSEA分析首选`clusterProfiler` http://mp.weixin.qq.com/s/9M3lprc3rL6XII3ffpDHAw，Y叔的良心之作，数据集更新及时，结果准确，自带语义分析合并相似条目、出图漂亮。

但有时出来的结果还需要进行一些筛选处理然后重新绘图，本文就介绍下如何根据`clusterProfiler`的输出结果绘制富集分析图。本文虽主推`clusterProfiler`, 但绘图方法适用于所有富集分析的输出结果。

### 一步绘制富集分析图

假设有这么一个富集分析结果矩阵 (文件名为GOenrichement.xls) 存储了EHBIO样品和Baodian样品中各自上调的基因富集的通路。

* Description 为GO通路的描述，也可以是KEGG通路。
* GeneRatio 为对应通路差异基因占总差异基因的比例，本列可以用分数或小数表示，都可以处理。
* qvalue 表示对应通路富集的显著性程度，可以是log处理过的，也可以是原始的。
* Count 为对应通路差异基因数目。 
* Type 这个矩阵合并了EHBIO样品和Baodian样品中各自上调的基因富集的通路，用Type列做区分。如果只有一个样品可不要。
* 考虑到手机屏幕小能显示的字符有限，只保留了输出结果中用到的列，实际使用时，整个输出结果文件可以作为输入，不相关的列会忽略掉，不影响出图。

```
Description	GeneRatio	qvalue	Count	Type
ERBB signaling pathway	7/320	0.001836081	7	EHBIO_up
regulation of ERBB signaling pathway	5/320	0.003886659	5	EHBIO_up
negative regulation of cell cycle G1/S phase transition	4/320	0.016153254	4	EHBIO_up
Wnt signaling pathway	13/320	0.01680096	13	EHBIO_up
cell-cell signaling by wnt	13/320	0.0171473	13	EHBIO_up
negative regulation of cell cycle process	8/320	0.019453085	8	EHBIO_up
extrinsic apoptotic signaling pathway	9/320	0.024164034	9	EHBIO_up
positive regulation of extrinsic apoptotic signaling pathway	4/320	0.025708228	4	EHBIO_up
cell cycle G1/S phase transition	7/320	0.035797856	7	EHBIO_up
negative regulation of apoptotic signaling pathway	8/320	0.038684745	8	EHBIO_up
regulation of Notch signaling pathway	4/320	0.041592045	4	EHBIO_up
regulation of cell cycle G1/S phase transition	5/320	0.047407619	5	EHBIO_up
negative regulation of BMP signaling pathway	3/320	0.049460847	3	EHBIO_up
regulation of ERK1 and ERK2 cascade	14/342	0.000629602	14	Baodian_up
positive regulation of cell adhesion	17/342	0.000827275	17	Baodian_up
ERK1 and ERK2 cascade	14/342	0.001086508	14	Baodian_up
regulation of cell growth	17/342	0.002228511	17	Baodian_up
positive regulation of cytoskeleton organization	10/342	0.004406867	10	Baodian_up
regulation of cell-cell adhesion	15/342	0.005075219	15	Baodian_up
regulation of cytoskeleton organization	15/342	0.019685646	15	Baodian_up
negative regulation of Notch signaling pathway	3/342	0.020578211	3	Baodian_up
neuron apoptotic process	10/342	0.040284925	10	Baodian_up
```

绘图用到的脚本名字为`sp_enrichmentPlot.sh`, 首先看看它的使用方法和出图效果。

#### 单样品分开绘制

示例矩阵中包含两个样品上调基因的富集通路，现在先取出一个样品绘制。

* Linux命令不熟悉的去生信宝典文章集锦中查看Linux学习指南

```bash
grep -v 'Baodian_up' GOenrichement.xls >GOenrichement.ehbio.xls
```

```bash
# -f: 指定输入文件，格式如上面描述
# -o: 指定横轴的变量，单个样品一般选择GeneRatio或样品名字
# -T: 指定横轴变量的类似，是字符串还是数值
# -v: 指定Y轴显示的内容，一般为富集条目的描述
# -c: 指定用哪一列设置颜色展示，一般为qvalue或p.adjust
# -s: 指定用哪一列设置点的大小，一般为Count
# -l: 指定某一列进行对数操作，一般选qvalue列；如果已做过对数操作，则忽略
# -a: 设置图片输出高度
# -x, -y: 设置横轴和纵轴标题，注意多个单词需要引号括起来
sp_enrichmentPlot.sh -f GOenrichement.ehbio.xls -o GeneRatio -T numeric -v Description -c qvalue -s Count -l qvalue -a 12 -x "GeneRatio" -y "GO description"
```

![]({{ site.img_url }}/splot/enrichment2.png)

**如果不想展示GeneRatio也可以。**

```bash
# -o: 指定横轴的变量，单个样品一般选择GeneRatio或样品名字
# -T: 如果是样品名字，指定为字符串
sp_enrichmentPlot.sh -f GOenrichement.ehbio.xls -o Type -T string -v Description -c qvalue -s Count -l qvalue -a 12 -x "Sample" -y "GO description"
```

![]({{ site.img_url }}/splot/enrichment3.png)

#### 多样品合并绘制

```bash
# 多出来的参数是-S用来指定样品分组，不同类型的基因的富集分析用不同的形状表示
sp_enrichmentPlot.sh -f GOenrichement.xls -o GeneRatio -T numeric -v Description -c qvalue -s Count -l qvalue -a 12 -x "GeneRatio" -y "GO description" -S Type
```

![]({{ site.img_url }}/splot/enrichment4.png)

通过这张图解释下，富集分析的结果怎么解读。富集分析实际是查找哪些通路里面包含的差异基因占总差异基因的比例显著高于通路中总基因占所有已经注释的基因的比例。这一显著性通常用多重假设检验矫正过的`pvalue`(又称qvalue, FDR或p.adjust)来表示。在图中体现为点的颜色。从绿到红富集显著性逐渐增高。点的大小表示对应通路中包含的差异基因的数目。点的形状代表了不同类型的基因，如EHBIO中上调的基因和Baodian中上调的基因。横轴表示对应通路包含的差异基因占总的差异基因的比例, 本图中最高不过5%, 这个值越大说明通路被影响的越多。

**如果不想展示GeneRatio也可以。**


```bash
# 跟单个样品不显示GeneRatio的命令一样，不同的样品分列展示。
sp_enrichmentPlot.sh -f GOenrichement.xls -o GeneRatio -T numeric -v Description -c qvalue -s Count -l qvalue -a 12 -x "GeneRatio" -y "GO description" -S Type
```

![]({{ site.img_url }}/splot/enrichment5.png)



## Reference

* {{ site.url }}/2017/07/enrichmentPlot

