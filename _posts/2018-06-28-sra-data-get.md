---
title: NGS基础：测序原始数据下载
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

生物或医学中涉及高通量测序的论文，一般会将原始测序数据上传到公开的数据库，上传方式见[测序文章数据上传找哪里](http://mp.weixin.qq.com/s/aDINq43Xwas_l4-AdY7xXg)；并在文章末尾标明数据存储位置和登录号,如 *The data from this study was deposited in NCBI Sequence Read Archive under accession SRA: SRP114962.*。

NCBI的SRA (Sequence Read Archive) 数据库(http://www.ncbi.nlm.nih.gov/sra/) 是最常用的存储测序数据的数据库。目前SRA数据的组织方式分为下面4个层次：

1. Studies--研究课题；
2. Experiments--实验设计；
3. Runs--测序结果集；
4. Samples--样品信息。


进入SRA官网：https://www.ncbi.nlm.nih.gov/sra, Search框中输入SRA编号（`SRP114962`），获得如下图的界面：

![](http://www.ehbio.com/ehbio_resource/SRP114962.png)

点击第一个样品即可查看其详细信息。

![](http://www.ehbio.com/ehbio_resource/SRR5906250.png)

当样品比较多时，可以点击**Send results to Run selector**（图中画圈的位置）进入筛选页面。

![img](http://www.ehbio.com/ehbio_resource/runselector.png)

从图中可发现，测序平台是Illumina HiSeq 4000，5748个Runs，每个Run的名字、样本名、测序类型（全基因组/外显子组等）、tissue、treatment等。

![img](http://www.ehbio.com/ehbio_resource/runSelectorShow.png)

在如此多的Runs中，假设我们想获取其中两个病人的化疗前和化疗后的外显子组测序数据，观察其化疗前后究竟有哪些基因突变以及突变的频率怎么样。数据来自于文章 [肿瘤化疗无效是对预先存在的突变的选择还是诱发新突变，Cell给你答案](https://mp.weixin.qq.com/s/HhGotXHxd_9maKwrjiBEFA)。

5748个Runs，有116Page，怎么找呢？

![img](http://www.ehbio.com/ehbio_resource/runSelectorFilter.png)

在*Facets*下拉框中先勾选**Assay Type**，等待页面相应后勾选`wxs`，即全外显子组数据，等待页面相应。

在*Facets*下拉框中勾选**Sample name**，等待页面相应后勾选`ktn102`及`ktn102`两个病人的分别四个样本（四种treatment：pre、2cycleschemo、operative和blood），如图。等待页面相应。获得Run编号（蓝色框）：**SRR5908363、SRR5908362...**

然后使用NCBI提供的工具SRAToolkit下载。

SRA toolkit https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=software, 根据服务器操作系统类型下载对应的二进制编码包，下载解压放到[环境变量](https://mp.weixin.qq.com/s/poFpNHQgHDr0qr2wqfVNdw)即可使用。

使用NCBI提供的SRA-toolkit中的工具`fastq-dump`直接下载SRR文件，并转换为FASTQ格式，`--split-3`参数表示如果是双端测序就自动拆分，如果是单端不受影响。`--gzip`转换fastq为压缩文件，节省空间。

下载的数据集一般比较大，放入后台不中断下载 (`nohup cmd &`)。

```
nohup fastq-dump -v --split-3 --gzip SRR5908360 &
nohup fastq-dump -v --split-3 --gzip SRR5908361 &
nohup fastq-dump -v --split-3 --gzip SRR5908362 &
nohup fastq-dump -v --split-3 --gzip SRR5908363 &
nohup fastq-dump -v --split-3 --gzip SRR5906250 &
nohup fastq-dump -v --split-3 --gzip SRR5906251 &
nohup fastq-dump -v --split-3 --gzip SRR5906252 &
nohup fastq-dump -v --split-3 --gzip SRR5906253 &
```

注意：如果数据量很大可能需要下载1-2天。数据下载完会在`~/ncbi`下面存在缓存的sra文件，记得定时清空。

## Summary

按照上述步骤下载完毕后可看到很多个fastq.gz格式测序文件。


* [NGS基础 - FASTQ格式解释和质量评估](http://mp.weixin.qq.com/s/tDMih7ISLJcL4F4sWBq3Vw)
* [NGS基础 - 高通量测序原理](https://mp.weixin.qq.com/s/SS9YBSpgUoU9gI86u-0ATg)
* [NGS基础 - 参考基因组和基因注释文件](http://mp.weixin.qq.com/s/2OoXy4f1t0hE8OUqsAt1kw)
* [NGS基础 - GTF/GFF文件格式解读和转换](http://mp.weixin.qq.com/s/rZ26i19hiS5ZOqIoqkL1Wg)

