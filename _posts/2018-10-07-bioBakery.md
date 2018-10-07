---
title: 哈佛大学宏基因组/16S分析流程 bioBakery
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---


bioBakery是NIH人类微生物组计划实施过程中开发的部分软件和使用教程的集合，主要由哈佛大学的Huttenhower实验室开发。提供了**16S**, **宏基因组**，**宏转录组**分析的全部流程，并可以生成结果报告。

其主要工具如下(可单独安装，也可打包安装)：

![](http://www.ehbio.com/ehbio_resource/microbial_community_profile.png)

![](http://www.ehbio.com/ehbio_resource/microbial_downstream.png)

![](http://www.ehbio.com/ehbio_resource/microbial_utility.png)

这都是宏基因组和16S分析常用工具，软件使用请看[宏基因组分析教程合集](https://mp.weixin.qq.com/s/F-c92FxvZA2CAX66nR5IFQ)。

### biobakery安装

下面4中安装方式，按需选择。

1. 使用`conda`一个个安装，[Conda安装方法](https://mp.weixin.qq.com/s/A4_j8ZbyprMr1TT_wgisQQ)。

2. 使用`Docker`安装，`docker run -it biobakery/workflows bash`。[Docker使用教程](https://mp.weixin.qq.com/s/HLHiWMLaWtB7SOJe_jP3mA)

3. 使用`Homebrew`或`Linuxbrew`安装，`brew install biobakery/biobakery/workflows`。

4. 使用`pip`安装(部分依赖包需要手动安装)，`pip install biobakery_workflows`。

### biobakery数据库安装

```
# To install the full shotgun databases:
biobakery_workflows_databases --install wmgx

# To install the full 16s databases:
biobakery_workflows_databases --install 16s
```

### 16S分析流程

![](http://www.ehbio.com/ehbio_resource/biobakery_16s_workflow.jpg)

```
# All input files are located in the folder input and all output files will be written to the folder output_data.

biobakery_workflows 16s --input input --output output_data
```

这个分析流程与我们的培训[扩增子有参无参和功能分析](https://mp.weixin.qq.com/s/w5zYuS54oHDVEDBsmpJQWQ)主体类似，而且我们在这个基础上做了比较多的拓展，可以获得更多定制分析结果。本课程也有配套视频在腾讯课堂<https://bioinfo.ke.qq.com/>, 欢迎观看。

### 16S DADA2分析流程

![](http://www.ehbio.com/ehbio_resource/biobakery_16s_dada2_workflow.jpg)

### 宏基因组流程

![](http://www.ehbio.com/ehbio_resource/biobakery_wms_workflow.jpg)

![](http://www.ehbio.com/ehbio_resource/biobakery_metagenoem_report.png)

新一期的宏基因组课程开始了，**2018年10月19-21日**, 相约北京鼓楼，一起讨论[宏基因组分析专题](https://mp.weixin.qq.com/s/1fN-urTTwZy6wiOenzSsqg)。内容涵盖这套流程，并且增加了无参宏基因组分析(bin)。

软件流程网址 <https://bitbucket.org/biobakery/biobakery/wiki/biobakery_workflows> (后台回复 **biobakery**获取可点击的链接)

### 扩增子三步曲

* [1图表解读-理解文章思路](http://mp.weixin.qq.com/s/oiVHO2S1JgYrKXPDU6fH2g)  
* [2分析流程-把握分析细节](http://mp.weixin.qq.com/s/KrYyy3jjzAL0rQzVfV6h4A)  
* [扩展1：视频教程-夯实分析思路](http://mp.weixin.qq.com/s/SxWl0qBJgg8ziZUFDmKvpQ)  
* [扩展2：QIIME2教程-了解分析趋势](http://mp.weixin.qq.com/s/wkn-91BVOSWZLRvlcaaEgg)  
* [3统计绘图-冲击高分文章](http://mp.weixin.qq.com/s/6tNePiaDsPPzEBZjiCXIRg)  
* [易生信-扩增子教程01-基本概念](https://mp.weixin.qq.com/s/PG_WQx3e_jegRgvVjtk9OA)
* [易生信-扩增子教程02-真菌引物选择](https://mp.weixin.qq.com/s/ouPqSH1kS8nX8QY0HsCj7g)
* [收藏-手把手带你重现菌群封面文章全部结果图表](https://mp.weixin.qq.com/s/J5vQB2e3LaXL88pO7vqSwg)

### 宏基因组教程

* [微生物组入门必读+宏基因组实操课程](http://mp.weixin.qq.com/s/sQyl5EctXFB95Oxg8YIasg)
* [扩增子图表解读-理解文章思路](http://mp.weixin.qq.com/s/oiVHO2S1JgYrKXPDU6fH2g)
* [扩增子分析流程-把握分析细节](http://mp.weixin.qq.com/s/KrYyy3jjzAL0rQzVfV6h4A)
* [扩增子统计绘图-冲击高分文章](http://mp.weixin.qq.com/s/6tNePiaDsPPzEBZjiCXIRg)
* [宏基因组分析教程](http://mp.weixin.qq.com/s/bcyvhFrNr6niqD13rQfZeg)
* [4500元的微生物组培训资料](http://mp.weixin.qq.com/s/li7SdZVaCEyFQF8h6MMh2A)
* [宏基因组分析教程合集](https://mp.weixin.qq.com/s/nzpU3JzxGE23FotB3sxcmw)
* [宏基因组分析教程合集和往期课程PPT分享](https://mp.weixin.qq.com/s/F-c92FxvZA2CAX66nR5IFQ)

### 宏基因组分析专题

* [1 背景知识-Shell入门与本地blast实战](http://mp.weixin.qq.com/s/jASOBPzpwYCL-fWNUJJp8g)
* [2 数据质控fastqc,   Trimmomatic,   MultiQC,   khmer](http://mp.weixin.qq.com/s/3O01eNMe79J_kUTaJjP6ag)
* [3 组装拼接MEGAHIT和评估quast](http://mp.weixin.qq.com/s/NMKX0iDuR_qOzmLXxC8MEQ)
* [4 基因注释Prokka](http://mp.weixin.qq.com/s/1TM61IrzrpVb5KhZ5A0kZQ)
* [5 基于Kmer比较数据集sourmash](https://mp.weixin.qq.com/s/Rmx-z1zxj7GF9ivJGWVvLg)
* [6 不比对快速估计基因丰度Salmon](http://mp.weixin.qq.com/s/2fwEtnEsBi5cJ65xyeoXxw)
* [7 bwa序列比对,   samtools查看,   bedtools丰度统计](http://mp.weixin.qq.com/s/rdTFTFg0rZOIa2_tuFEOUA)
* [8 分箱宏基因组binning,   MaxBin,   MetaBin,   VizBin](http://mp.weixin.qq.com/s/rZitcvykAlxnsNEzsW5JRg)
* [9 组装assembly和分箱bin结果可视化—Anvio](http://mp.weixin.qq.com/s/FesH_mCunpZLpKC2pIg1UQ)
* [10 绘制圈图-Circos安装与使用](http://mp.weixin.qq.com/s/FJlKY3kU5Fm6bYkjtwRkEw)
* [MetaPhlAn2分析有参宏基因组](http://mp.weixin.qq.com/s/xSjFGwcr1XIAZKdByJAWmQ)



