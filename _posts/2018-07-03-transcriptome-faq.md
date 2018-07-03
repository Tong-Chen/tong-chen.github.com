---
title: 120分的转录组试题和答案
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

这个答案之前出过三份，最近整理了一份文字版，方便观看，还请大家多多补充。

* [120分的转录组试题（第一份答案）](https://mp.weixin.qq.com/s/lsaubsJofGRbCVnrhmTygw)
* [120分的转录组试题（第二份答案）](https://mp.weixin.qq.com/s/Vh2c-JegoaMr0Ws2gDuFhA)
* [120分的转录组试题（第三份答案）](https://mp.weixin.qq.com/s/BadU3ZVPAlxBn0_QehVnXQ)

## 一、理论题目

### 1、说出至少5种高通量测序技术的应用，并简要描述其在科研中的用途？ (2分) (选答)

* de novo sequencing：获得该物种的参考序列，为后续研究奠定基础。

* 基因组重测序：进行全基因组重测序，在全基因组水平上扫描并检测突变位点，发现个体差异的分子基础。

* 转录组测序：基因表达定量，寻找差异基因；发现新的转录本、可变剪切、基因融合等。([转录组分析的正确姿势](https://mp.weixin.qq.com/s/h3wEMUoRNKMFVLDLDFXNoA))

* ChIP-Seq: 结合ChIP和高通量测序技术的优势，能够在全基因组范围内高效地研究目的蛋白的结合位点。([ChIP-seq基本分析流程](http://mp.weixin.qq.com/s/nldZ1_wiCmCtLO3MWJuQ8Q))

* DNA甲基化：基因组水平高精度的甲基化检测成为现实。甲基化DNA免疫共沉淀测序、甲基结合蛋白测序、亚硫酸氢盐测序。

* [测序发展史：150年的风雨历程](https://mp.weixin.qq.com/s/GReWY8yq7O_xVnajknrHZQ)也看一下。

### 2、转录组测序可以解决的问题有哪些？(2分)

* 可以从转录组水平整体评估外界条件引起的基因表达响应。

* 对于检测低丰度转录本和发现新转录本具有独特优势。

* 可以发现基因融合、可变剪切及结构变异。

### 3、转录组项目开展前需要考虑哪些问题？ (6分)

* 明确解决的生物学问题，选择合适的建库方法和测序方法。

* 设计合理的对照样品和生物学重复。

* 尽量一次性完成样本的处理和测序。不然就得处理[批次效应](https://mp.weixin.qq.com/s/Vmhx_TGxNkQzkekf93Xl4w)。

* 经济条件，样本获取难易成度，失败风险。

###	4、转录组测序同一样品不同重复之间相关性多少合适？分别叙述不同的需求可用reads数多少合适？ (3分)

* 相同基因型生物学重复Spearman系数>0.9；不同基因型生物学重复Spearman系数>0.8。

* 检测新转录本，可变剪切：  50-100 million可用reads.

* Long RNA-Seq library:   30 million aligned reads.

* RAMPAGE library:        30 million aligned reads.

* Small RNA-Seq library:  30 million aligned reads.

### 5、测序reads数和测序碱基数之间如何换算?(1分)

* Reads数=碱基数/读长；例子：如果读长150bp 碱基数4.5G，则对应的reads为30M。即：30million reads=4.5G/150bp

### 6、描述下常规转录组测序的过程，从样本准备到获取测序数据中经历的步骤？ (6分)

* 获取样本：培养细胞或从组织上进行解剖，必要时可以用流式细胞仪分离细胞，注意对照组和生物学重复。
* RNA提取：根据不同的提取试剂盒提total RNA，去除rRNA或富集mRNA，反转录为cDNA.
* 建库：将cDNA片段化(超声剪切或酶切)，末端修复+A，链接index接头，一般需要再进行5-8个循环的文库扩增，磁珠纯化进行片段筛选。
* 上机测序：把index不同的样品混合到一起，把双链文库变性成单链，与flowcell上的oligo互补结合，进行桥式扩增，形成cluster，进行边合成边测序 (SBS)。具体见[NGS基础 - 高通量测序原理](https://mp.weixin.qq.com/s/SS9YBSpgUoU9gI86u-0ATg)。
* 获取数据：按照接头拆分下机后的bcl格式文件并转为fastq格式文件。

### 7、描述下常规转录组分析的流程，列举每步可用的工具、每步分析的意义? (10分)

* [数据质控](http://mp.weixin.qq.com/s/tDMih7ISLJcL4F4sWBq3Vw)：质量评估用FastQC软件，质控cutadapt，Trimmomatic。意义：去除碱基质量低的reads和接头部分。
* 比对：[Tophat2/HISAT2/STAR](http://mp.weixin.qq.com/s/NUEi6oRFL7B3f1FpCD4Xug)。意义：确定每条reads来源于哪个基因，什么位置。
* 差异基因鉴定：[DEseq2](https://mp.weixin.qq.com/s/Vmhx_TGxNkQzkekf93Xl4w)。意义：比较标准化后的基因表达丰度，得到差异基因。
* GO富集分析：[GOEAST](https://mp.weixin.qq.com/s/l6j2encDfEQkt2UeNCMFhg)。 意义：寻找差异基因与哪些功能有关。
* 转录本拼装：String Tie；可变剪切：Rmats。意义：发现新的转录本和可变剪切形式。
* [通路可视化](http://mp.weixin.qq.com/s/C4EBufEtFF6bhBKrH8NXng)、[WGCNA共表达分析](https://mp.weixin.qq.com/s/PMb2xwADvnMwaipyFXdtzQ)等。

### 8、基因组和转录组测序序列比对使用的工具有什么不同？转录组reads比对回基因组时需要特殊地考虑什么？(4分)

* RNA测序并不能直接使用DNA测序常用的BWA、Bowtie等比对软件，这是由于真核生物内含子的存在，导致测到的reads有时并不与基因组序列完全一致，因此需要使用Tophat2/HISAT/STAR等专门为RNA测序设计的软件进行splice-map比对。

### 9、STAR为了提高比对率做了哪些容错机制? (4分)

* STAR具有最高比例的在基因组上有唯一比对位置的reads，尤其是对读长为300nt的样品也有最高的比对率。STAR只保留双端reads都比对到基因组的序列，但对低质量的比对(允许更多的错配碱基和soft-clip事件)容忍度高，这一点在长reads样品中的体现更为明显。

注：soft-clip事件即reads末端存在低质量碱基或接头导致比对不上的，STAR会自动尝试截去未比对部分，只保留比对上的部分。

### 10、StringTie和Cufflinks是做什么的？什么时候会用到？(2分)

* 转录本拼装， 研究新转录本，可变剪切时会用到。

### 11、Illumina测序时什么情况下会测到接头序列? (3分)

* 如果插入片段小于测序单端读长，会在尾部测到接头; 如果接头之间发生了自连，则整条或大部分是接头。

### 12、链特异文库是什么？可以解决什么问题？(3分)

* 建库时将mRNA链的方向信息保存到测序文库中。最常用的dUTP，首先利用随机引物合成RNA的一条cDNA链，在合成第二条链的时候用dUTP代替dTTP，加adaptor后用UDGase处理，将有U的第二条cDNA降解掉。

* 确定转录本来自正链还是负链，更准确的获得基因的结构以及基因表达信息，并且可以更好的发现新的转录本、反义转录本等。

### 13、Illumina测序时测序簇 (cluster)是如何生成的？生成测序簇的意义是什么？(2分) (选答)

* 单链文库与flowcell中的oligo结合，进行快速等温桥式扩增，在小范围内由同一条链克隆出来的很多条链聚集成簇（cluster）。
* 放大荧光信号，方便成像检测。

### 14、双端测序的左端和右端reads分别测序的什么，是否来源于同一片段? (2分)

左端和右端reads分别测的是同一条模板的两端的序列。左端和右端reads对应下图的read1和read2。

![img](photo/5.png)

## 二、实战题目

### 1、ct@ehbio:~/data$ 中 ct、ehbio、~/data、$ 各代表什么？ (1分)

* `ct`: 用户名。
* `ehbio`: 主机名。
* `~/data`: 当前所在路径为用户家目录的data下。
* `$`: 普通用户命令提示符。

### 2、写代码计算FASTQ序列中的reads数、碱基数? (1分)

* 计算reads数：

```
echo "`zcat trt_N061011_1.fq.gz | wc -l` / (4*1000000)" | bc -l

# wc -l: 计算行数
# bc -l: 计算器 (-l：浮点运算)
# 除以4：fastq文件每4行为一条reads
# 除以1000000：单位换算为million
```

* 计算碱基数：

```
zcat trt_N061011_1.fq.gz | awk '{if(FNR%4==0) base+=length}END{print base/10^9,"G";}'

# %：取除以4后的余数
# / 10^9：单位换算为G

```

### 3、写代码用Fastqc评估测序质量。并解释什么样的质量值是可以接受的？GC含量正常和异常的结果有什么不同? 导致GC含量异常的原因是什么？ (4分)

```
fastqc filename

#filename：通常为样品名.fq.gz
```

* Reads数和reads长度符合预期，碱基质量Q30>=75，GC含量45%-50%（特殊序列除外），接头序列越少越好，GC含量正常时曲线圆滑，有单个突出的峰，不正常会有多个突起，原因是样品本身碱基不平衡或引入了其他物种基因或引物二聚体。

* 具体见[NGS基础 - FASTQ格式解释和质量评估](http://mp.weixin.qq.com/s/tDMih7ISLJcL4F4sWBq3Vw)。

### 4、写代码去除双端测序reads低质量碱基和接头序列，并解释各个参数的含义？(3分)

```
trimmomatic.sh PE -phred33 input_forward.fq input_reverse.fq \
output_forward_paired.fq \ 
output_forward_unpaired.fq \
output_reverse_paired.fq \ 
output_reverse_unpaired.fq \
ILLUMINACLIP:adaptor-PE.fa:2:30:10 LEADING:20 TRAILING:20 MINLEN:36

# PE：双端测序
# -phred33：质量体系
# ILLUMINACLIP：接头类型，去除接头和引物序列
# LEADING:20 和 TRAILING：20：去除前后各20个低质量碱基
# MINLEN:36：去除小于36bp的reads
```

### 5、为什么一般只使用去除低质量碱基和接头后仍然成对的reads做后续分析? (2分)

* 为了结果更准确。

### 6、写代码完成基因组索引的构建，并解释基因组索引构建的意义是什么? (2分)

```
hisat2-build -p 2 GRCh38.fa GRCh38
```

* 提高比对速度。

### 7、解释环境变量是什么？设置环境变量的意义是什么？如何设置环境变量？(3分)

* 告诉系统在哪几个目录下有可执行程序，当输入可执行程序名字时系统会去这几个指定目录中查找对应文件是否存在并执行。设置环境变量是为了更方便调用可执行程序。（相当于windows中快捷方式）

```
export PATH=$PATH:绝对路径
```

### 8、写代码进行序列比对，并解释每个参数的含义? (2分)

```
hisat2 -x genome/GRCh38 -1 trt_N061011_1.fq.gz -2 trt_N061011_2.fq.gz -p 2 \
		--mm -S trt_N061011/trt_N061011.sam

#-p 4: 使用4个线程。
#-x：索引文件的名字。(若不在当前目录需包含路径)
#-1, -2：左端和右端序列。
#--mm: 多个hisat2共享内存中的hisat2基因组索引，减少内存使用
#-S: 输出文件
```

### 9、如何从比对结果中获取比对reads数和比对率？怎么判断比对率是否合适？ (2分)

* 从hisat2比对的输出可以看到reads数和比对率，可以重定向到某个文件方便以后查看。
* 比对率是否合适没有统一标准，一般比对率80%以上。或者未比对上的`reads`做一下`blast`，依然没有匹配，也可以说明都比对环节无问题。如果比对到其它物种，考虑存在污染。

### 10、解释STAR或HTSeq是如何计算基因的表达量(readscount)的，程序是根据注释文件中的哪些信息来计算某个基因的reads数的，如果一个基因有多个转录本怎么计算基因表达量 (3分)

```
htseq-count -f bam -r pos -a 10 -t exon -s no -i gene_id -m union \
trt_N061011/trt_N061011.sortP.bam genome/GRCh38.gtf \
>trt_N061011/trt_N061011.readsCount
```

* 程序是根据注释文件中`gene_name`和`exon`信息来判断reads归属。多个转录本会统一计算。


### 11、写代码转换BAM文件为样品间可比的bigWig文件，并说明bigWig文件的用途? (2分)

```
bam2wig.py -i trt_N061011/trt_N061011.sortP.bam -s genome/GRCh38.chromsize \
	-o trt_N061011/trt_N061011 -t 1000000000 -q 0
```

导入基因组浏览器进行数据可视化。[高通量数据分析必备|基因组浏览器使用介绍 - 1](https://mp.weixin.qq.com/s/_5zoRvjku5pb9qtwrvlWYw)。

### 12、写代码评估比对质量，包括评估基因5’-3’测序均一度评估、reads在基因组标志区域评估和饱和度评估，并解释每个参数的意义? (3分)

* 5'-3'测序覆盖均一性评估：

```
# RseQC软件
geneBody_coverage2.py -i trt_N061011/trt_N061011.bw -r genome/GRCh38.model.gtf.bed12 -o \
	trt_N061011/trt_N061011.geneBody_coverage

# -i：输入文件
# -r：输入参考文件
# -o:指定输出文件
```

* Reads在基因组标志区域评估：


```
Read_distribution.py -i trt_N061011/trt_N061011.sortP.bam -r genome/GRCh38.gtf.bed12 \
	>trt_N061011/trt_N061011.read_distrib.xls
```

* 测序饱和度评估：

```
RPKM_saturation.py -i trt_N061011/trt_N061011.sortP.bam -r genome/GRCh38.gtf.bed12 \
	-s 5 -q 0 -o trt_N061011/trt_N061011.RPKM_saturation
```

### 13、用RSEM计算基因表达TPM值，并解释TPM值、FPKM值、与DESeq2标准化后的值、原始reads count的区别? (4分)

* RPKM：Reads per Kilobase per Million.
* RPKM=（比对到某个基因上的reads数/比对到基因组上的总reads数）/基因长度（k）* 10^6
* FPKM意义与RPKM极为相近。二者区别仅在于Fragment与Read。PE测序中，通常一个Fragment产生两条reads。

![img](photo/TPM.png)

### 14、写R代码读入reads count文件、样品分组信息文件，并解释参数的含义?  (1分)

* 读入Reads count文件:

```
Data <- read.table("ehbio_trans.Count_matrix.xls", header=T, row.names=1, com='', quote='',check.names=F, sep="\t")
```

* 读入样品分组文件:

```
sample <- read.table("sampleFile", header=T, row.names=1, com='', quote='', check.names=F, sep="\t", colClasses="factor")
```


### 15、写代码产生DESeqDataSet数据集，并解释参数的含义?  (3分)

```
ddsFullCountTable <- DESeqDataSetFromMatrix(countData = data,colData = sample, design= ~ conditions)
dds <- DESeq(ddsFullCountTable)

#countData：表达矩阵
#cloData：样品分组信息
#design：实验设计信息
#conditions必须是cloData中的一列
```

### 16、解释函数DESeq运行时函数内部都做哪些数据处理和操作? (5分)

* 表达量的标准化，差异基因分析。

### 17、写代码从DESeqDataSet数据集获取标准化后的数据、标准化后取对数的数据，并解释用到的函数的作用? (3分)

* 标准化数据:

```
normalized_counts <- counts(dds, normalized=TRUE)
normalized_counts_mad <- apply(normalized_counts, 1, mad)
normalized_counts <- normalized_counts [order(normalized_counts_mad, decreasing=T), ]
```

* 数据输出:

```
write.table(normalized_counts,file="ehbio_trans.Count_matrix.xls.DESeq2.normalized.xls",quote=F, sep="\t", row.names=T, col.names=T)
```

* 取对数: 

```
rld <- rlog(dds, blind=FALSE)
rlogMat <- assay(rld)
rlogMat <- rlogMat[order(normalized_counts_mad, decreasing=T), ]
```

* 数据输出:

```
write.table(rlogMat,file="ehbio_trans.Count_matrix.xls.DESeq2.normalized.rlog.xls",quote=F, sep="\t", row.names=T, col.names=T)
```

### 18、写代码在DESeq中做主成分分析，并解释主成分分析的结果? (2分)

```
plotPCA(rld, intgroup=c("conditions"), ntop=5000)
```

* 每个点代表一个样品，点与点之间的距离越近，基因成分越相似。

### 19、写代码计算样品相关性并完成相关性热图绘制，解释下述哪种矩阵适合做相关性分析:原始readscount、标准化后的矩阵、标准化后对数处理的矩阵？(4分)

* 生成颜色：

```
hmcol <- colorRampPalette(brewer.pal(9, "GnBu"))(100)
```

* 计算相关性pearson correlation：

```
pearson_cor <- as.matrix(cor(rlogMat, method="pearson"))
```

* 层级聚类：

```
hc <- hcluster(t(rlogMat), method="pearson")
```

* 热图绘制：

```
pdf("ehbio_trans.Count_matrix.xls.DESeq2.normalized.rlog.pearson.pdf", pointsize=10)
heatmap.2(pearson_cor, Rowv=as.dendrogram(hc), symm=T, trace="none",
col=hmcol, margins=c(11,11), main="The pearson correlation of each
sample")
dev.off()
```

计算样品相关性用标准化后对数处理的矩阵。

### 20、写代码提取两组样品中的差异基因分析结果，并解释用到的函数和变量的意义? (3分)

```
sampleA = "untrt"
sampleB = "trt"
contrastV <- c("conditions", sampleA, sampleB)
res <- results(dds, contrast=contrastV)
baseA <- counts(dds, normalized=TRUE)[, colData(dds)$conditions == sampleA]
if (is.vector(baseA)){
  baseMeanA <- as.data.frame(baseA)
} else {
  baseMeanA <- as.data.frame(rowMeans(baseA))
}
colnames(baseMeanA) <- sampleA
baseB <- counts(dds, normalized=TRUE)[, colData(dds)$conditions == sampleB]
if (is.vector(baseB)){
  baseMeanB <- as.data.frame(baseB)
} else {
  baseMeanB <- as.data.frame(rowMeans(baseB))
}
colnames(baseMeanB) <- sampleB
res <- cbind(baseMeanA, baseMeanB, as.data.frame(res))
res <- cbind(ID=rownames(res), as.data.frame(res))
res$baseMean <- rowMeans(cbind(baseA, baseB))
res$padj[is.na(res$padj)] <- 1
res <- res[order(res$pvalue),]
comp314 <- paste(sampleA, "_vs_", sampleB, sep=".")
comp314 <- paste(sampleA, "_vs_", sampleB, sep=".")
file_base <- paste("ehbio_trans.Count_matrix.xls.DESeq2", comp314, sep=".")
file_base1 <- paste(file_base, "results.xls", sep=".")
write.table(as.data.frame(res), file=file_base1, sep="\t", quote=F, row.names=F)
```

使用函数和变量为了程序的方便和实用。

### 21、写代码绘制火山图，并解读火山图展示的信息是什么? (1分)

```
logCounts <- log2(res$baseMean+1)
logFC <- res$log2FoldChange
FDR <- res$padj
\#png(filename=paste(file_base, "Volcano.png", sep="."))
plot(logFC, -1*log10(FDR), col=ifelse(FDR<=0.01, "red", "black"),
xlab="logFC", ylab="-1*log1o(FDR)", main="Volcano plot", pch=".")
\#dev.off()
```

左右两边代表下调和上调的基因，每个点是一个基因，点越高差异越大。[R语言 - 火山图](https://mp.weixin.qq.com/s/dikXvlDhjmaPuZkCFyRXUg) 

### 22、写代码绘制差异基因热图，并解读此热图? (2分)

```
res_de_up_top20_id <- as.vector(head(res_de_up$ID,20))
res_de_dw_top20_id <- as.vector(head(res_de_dw$ID,20))
red_de_top20 <- c(res_de_up_top20_id, res_de_dw_top20_id)
red_de_top20
# 可以把矩阵存储，提交到www.ehbio.com/ImageGP 绘制火山图
# 或者使用我们的s-plot https://github.com/Tong-Chen/s-plot
red_de_top20_expr <- normalized_counts[rownames(normalized_counts) %in% red_de_top20,]
library(pheatmap)
pheatmap(red_de_top20_expr, cluster_row=T, scale="row", annotation_col=sample)
```

[R语言 - 热图简化](https://mp.weixin.qq.com/s/_9LKs6t6rcjzokF_0gneSA)

* 横轴为样品，纵轴为基因，红色表达量越高，蓝色表达量低。

### 23、绘制热图时什么时候做行聚类、什么时候做列聚类、按行标准化数据的意义是什么、结果怎么解读? (2)

* 样品之间差异比较做列聚类，基因之间差异比较做行聚类。

* 避免某个表达量异常高，影响中等表的量的显示。把真正的表达量隐藏，以便显示表达量的趋势。红色表的量高，蓝色表的量地；每行进行比较，发现每个基因在不同样品中的表达情况。

### 24、如何识别样品中是否有批次效应? (2分) (选答)

*在samplefile中添加一行批次列，从热图上看，差异基因应该是以分组信息聚类的，但如果以批次列聚类了，就说明存在批次效应。

### 25、描述GO富集分析的原理，并给出GO富集分析需要的数据的格式? (1分)

* 采用超几何检验判断选定的差异基因在GO的哪些通路富集。

* 根据挑选出的差异基因，计算这些差异基因同GO分类中某（几）个特定的分支的超几何分布关系，GO富集分析会对每个有差异基因存在的GO返回一个p-value，小的p值表示差异基因在该GO 中出现了富集。

* 数据格式：两列文件，第一列基因ID，第二列是样本差异。

### 26、描述GSEA富集分析的原理，并给出GSEA富集分析需要的数据的格式? (1分)

* 需要两个文件，参考文件：排序好已知功能注释后的基因集 分析的文件：自己做的表达矩阵。

* 用表达矩阵去与基因集比较，统计表达矩阵中的基因对应到基因集的位置是否集中。

### 27、GO富集分析结果的泡泡图怎么解释? (1分)

* 基因比例的比率。

* 越红越显著，点越大差异基因数目越多。

### 28、转录本拼装的意义是什么? 不同样品拼装结果最后需要merge在一起的意义是? (2分)
* 发现新的转录本，新的可变剪切形式，鉴定非编码RNA.

* 合并是为了新发现的方便。

### 29、DESeq2中是如何处理批次效应的? (2分) (选答)

* 用limma 包中的removeBatchEffect函数去除批次效应。把标准化后取对数后的矩阵和样品分组表（标轴必须有批次列）交给函数，函数会根据批次列进行去除，也可以在DESeq2计算表达量时加入design=~batch+conditions参数，会自动去除批次效应。

