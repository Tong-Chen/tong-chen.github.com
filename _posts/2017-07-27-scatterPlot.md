---
title: R 学习 - 散点图
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

## 散点图

散点图在生物信息分析中是应用比较广的一个图，常见的差异基因火山图、功能富集分析泡泡图、相关性分析散点图、抖动图、PCA样品分类图等。凡是想展示分布状态的都可以用散点图。

### 横纵轴都为数字的散点图解析

绘制散点图的输入一般都是规规矩矩的矩阵，可以让不同的列分别代表X轴、Y轴、点的大小、颜色、形状、名称等。

#### 输入数据格式 (使用火山图的输入数据为例)

火山图需要的数据格式如下

* id: 不是必须的，但一般的软件输出结果中都会包含，表示基因名字。
* log2FoldChange: 差异倍数的对数，一般的差异分析输出结果中也会给出对数处理的值, 因此程序没有提供这一步的计算操作。
* padj: 多重假设检验矫正过的差异显著性P值；一般的差异分析输出结果为原始值，程序提供一个参数对其求取负对数。
* significant: 可选列，标记哪些基因是上调、下调、无差异；若无此列或未在参数中指定此列，默认程序会根据`padj`列和`log2FoldChange`列根据给定的阈值自动计算差异基因，并作出不同颜色的标记。
* label: 可选列，一般用于在图中标记出感兴趣的基因的名字。非`-`行的字符串都会标记在图上。

```r
volcano = "id;log2FoldChange;padj;significant;label
E00007;4.28238;0;EHBIO_UP;A
E00008;-1.1036;0.476466843393901;Unchanged;-
E00009;-0.274368;1;Unchanged;-
E00010;4.62347;7.37606076333335e-103;EHBIO_UP;-
E00012;0.973987;0.482982440163204;Unchanged;-
E00017;-1.30205;0.000555693857439792;Baodian_UP;B
E00024;0.617636;2.78047837287061e-13;Unchanged;-
E00033;1.48669;2.56000581595275e-60;EHBIO_UP;-
E00034;-0.783716;0.00341521725291801;Unchanged;-
E00036;2.01592;6.03136656016401e-06;EHBIO_UP;C
E00040;-1.89657;4.73663890849056e-21;Baodian_UP;-
E00041;-0.268168;0.563429434558031;Unchanged;-
E00042;0.0861048;0.367700939634328;Unchanged;-
E00043;-1.19328;1.42673872027352e-153;Baodian_UP;-
E00044;-0.887981;2.43067804654905e-26;Unchanged;-
E00047;-0.610941;5.51696648645932e-57;Unchanged;-"

# 数据的读取之前的R语言统计和绘图系列都已解释过，不再赘述
# 文末也有链接可直达之前的文章，新学者建议从头开始
volcanoData <- read.table(text=volcano, sep=";", header=T, quote="", check.names=F)
head(volcanoData)
```

		  id log2FoldChange          padj significant label
	1 E00007       4.282380  0.000000e+00    EHBIO_UP     A
	2 E00008      -1.103600  4.764668e-01   Unchanged     -
	3 E00009      -0.274368  1.000000e+00   Unchanged     -
	4 E00010       4.623470 7.376061e-103    EHBIO_UP     -
	5 E00012       0.973987  4.829824e-01   Unchanged     -
	6 E00017      -1.302050  5.556939e-04  Baodian_UP     B

绘制散点图，只需要指定X轴和Y轴，再加上`geom_point`即可。

```r
library(ggplot2)
p <- ggplot(volcanoData, aes(x=log2FoldChange, y=padj))
p <- p + geom_point()
# 前面是给p不断添加图层的过程
# 单输入一个p是真正作图
# 前面有人说，上面都输完了，怎么没出图
# 就因为差了一个p
p
```

说好的火山图的例子，但怎么也看不出喷发的态势。

![]({{ site.img_url }}/splot/scatterplot1.png)

对数据坐下预处理，差异大的基因`padj`小，先对其求取负对数，所谓负负得正，差异大的基因就会处于图的上方了。

```r
# 从示例数据中看到，最小的padj值为0，求取负对数为正无穷。
# 实际上padj值小到一个点对我们来讲就是个数
# 所以可以给所有小于1e-6的padj都让其等于1e-6，再小也没意义
# 
volcanoData[volcanoData$padj<1e-6, "padj"] <- 1e-6
volcanoData$padj <- (-1)* log10(volcanoData$padj)
```

数据中基因的上调倍数远高于下调倍数，使得出来的图是偏的，这次画图时调整下X轴的区间使图对称。

```r
p <- ggplot(volcanoData,  aes(x=log2FoldChange,  y=padj)) +
     geom_point() +
	 xlim(-4.7, 4.7)
p
```

![]({{ site.img_url }}/splot/scatterplot2.png)

有点意思了，数据太少不明显，下一步加上颜色看看。

```r
p <- ggplot(volcanoData,  aes(x=log2FoldChange,  y=padj)) +
     geom_point(color=significant) +
	 xlim(-4.7, 4.7)
p
```

利用现有的数据，基本上就是这个样子了。虽然还不太像，原理都已经都点到了。

![]({{ site.img_url }}/splot/scatterplot3.png)

盗取火山图绘制一文中的图来显示个真正的火山图吧。这样一步步绘制很麻烦，去看一步法吧。


### 横纵轴都为字符串的散点图展示

#### 输入数据格式如下

这个数据是前面讲到的FASTQC结果总结中的直观的查看所有样品测序碱基质量和GC含量的散点图的示例数据。

```r
fastqc<-"ID;GC_quality;Base_quality
ehbio_1_1;PASS;PASS
ehbio_1_2;PASS;PASS
ehbio_2_1;WARN;PASS
ehbio_2_2;WARN;PASS
Other_1_1;FAIL;FAIL
Other_1_2;FAIL;FAIL"

fastqc_data <- read.table(text=fastqc, sep=";", header=T)
# 就不查看了
```

```r
p <- ggplot(fastqc_data, aes(x=GC_quality, y=Base_quality)) + geom_point()
p
```

![]({{ site.img_url }}/splot/scatterplot4.png)

六个点少了只剩下了3个，重叠在一起了，而且也不知道哪个点代表什么样品。这时需要把点抖动下，用到一个包`ggbeeswarm`，抖动图的神器。

```r
library(ggbeeswarm)
p <- ggplot(fastqc_data, aes(x=GC_quality, y=Base_quality)) + geom_quasirandom()
# 使用geom_text增加点的标记
# label表示标记哪一列的数值
# position_quasirandom获取点偏移后的位置
# xjust调整对齐方式; hjust是水平的对齐方式，0为左，1为右，0.5居中，0-1之间可以取任意值。vjust是垂直对齐方式，0底对齐，1为顶对齐，0.5居中，0-1之间可以取任意值。
# check_overlap检查名字在图上是否重叠
p <- p + geom_text(aes(label=ID), position=position_quasirandom(),hjust=0, check_overlap=T)
p
```

![]({{ site.img_url }}/splot/scatterplot5.png)


### 一网打进散点图绘制

假如有一个输入数据如下所示(存储于文件scatterplot.xls中)

```
Samp	Gene1	Gene2	Color	Size	GC_quality	Base_quality
a	1	1	grp1	10	PASS	PASS
b	2	2	grp1	10	PASS	PASS
c	1	3	grp1	10	WARN	PASS
d	3	1	grp2	15	WARN	WARN
e	2	2	grp2	15	PASS	WARN
f	3	3	grp3	5	PASS	PASS
g	2	1	grp3	5	WARN	PASS
```

想绘制样品在这两个Gene为轴的空间的分布，并标记样品的属性，只需要运行如下命令

```bash
# -f: 指定输入文件，列数不限，顺序不限; 第一行为列名字，第一列无特殊要求，必选
# -X: 指定哪一列为X轴信息，必选
# -Y: 指定哪一列为Y轴信息，必选
# -c: 指定用哪一列标记颜色，可选
# -s: 指定哪一列标记大小，一般为数字列，可选
# -S: 指定哪一列标记形状，可选
# -L: 指定哪一列用来作为文本标记
# -w, -u: 指定图的长宽
sp_scatterplot2.sh -f scatterplot.xls -X Gene1 -Y Gene2 -c Color -s Size -S GC_quality -L Samp -w 10 -u 10
```

![]({{ site.img_url }}/splot/scatterplot6.png)

如果横纵轴为字符串，且有重复, 则需指定参数`-J TRUE`以错开重叠的点，具体如下

```bash
# -O: 指定X轴变量的顺序, 默认是字母顺序
# 其它列或其它属性的顺序也可以用相应的方式指示，具体看程序的帮助提示
# -c Gene1: 用特定基因的表达对点着色，单细胞分析图中常用
# -J TRUE: 见上
# -Z FALSE：默认使用geom_text_repel添加点的标记，及其智能，不会出现标签过多覆盖的情况
# 但对jitterplot，会有些冲突，所以在`-J TRUE`且出来的图中点的标签不符合预期时，设定
# 次参数为FALSE，使用geom_text标记点。

sp_scatterplot2.sh -f scatterplot.xls -X GC_quality -Y Base_quality -O "'WARN', 'PASS'" -c Gene1 -w 10 -u 10 -J TRUE -L Samp -Z FALSE
```

![]({{ site.img_url }}/splot/scatterplot7.png)

只有想不到，没有做不到，`sp_scatterplot2.sh`还可以完成更多你想做的散点图，而且只需调参数，无需改代码，简单可重用。

```diff
转发获取，不用再重复了
```

## Reference

* {{ site.url }}/2017/07/scatterPlot

## 生信宝典公众号, 几千人一起学生信

<https://mp.weixin.qq.com/s/c2nwATMwyU_9FgLprqmQ5A>

