---
title: Excel改变了你的基因名，30% Nature文章受影响
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

EXCEL是常用的查看表格的工具，提供了很好的数据筛选、绘图等功能，不少基因表达数据也会在EXCEL中打开查看、筛选和排序。还有 [3 个超赞的 EXCEL 插件，让你 5 分钟从小白变大神](https://mp.weixin.qq.com/s/NTQLwZviroOfQG6b2hI7lg)。

但是EXCEL也会出现比较尴尬的事情，如基因名字的转换。比如gene symbols `SEPT2` (Septin 2)、`MARCH1` [Membrane-Associated Ring Finger (C3HC4) 1, E3 Ubiquitin Protein Ligase], Oct4 (Pou5f1) 会被转为`2-Sep`、`1-Mar`和`4-Oct`. RIKEN 识别符因为`E`的存在会被识别为科学计数法，如`2310009E13`转为`2.31E+13`。

![](http://www.ehbio.com/ehbio_resource/excel_genename_date.gif)

这一事情在`2014`年的`BMC Bioinformatics`上就有报道。下图所示12个月份开头的基因名字都**不可逆**的转换为了日期。

![](http://www.ehbio.com/ehbio_resource/excel_genename_table.jpg)

这些数据不只是存在于Excel表中，还威胁到了公共数据库，如NCBI LocusLink。

![](http://www.ehbio.com/ehbio_resource/excel_genename_ncbi.jpg)

2016年Genome biology对2005-2015期间发表在18个杂志的文章附表中基因名字做了分析，发现Nature中有附表的文章里面，有**30%**以上出现了EXCEL引起的基因名字转换错误，受影响的文章有**74**篇，影响的基因**1375**个。并且出现基因名字转换错误的附表错误的文章逐年增加，这一定程度上也是因为大规模基因研究的迅速开展使得总上传的附件数增多引起的。

并且作者还做了相关性分析，**影响因子越高，受影响的基因列表比例越大**。这可能是因为高影响力的文章涉及了更多的数据集。

BMC bioinformatics虽然首先提出这个问题，后续受影响比例也比较大，有政策，无实施。

![](http://www.ehbio.com/ehbio_resource/excel_gename_gb_journal.gif)


为此，Eric A. Welsh特意开发了一款工具阻止此类转换，提供了在线版本，Excel插件，Perl脚本和Galaxy访问接口，也是煞费苦心。软件发布在Github上，<https://github.com/pstew/escape_excel>，文章发表在`Plos One`。

Excel插件也很好安装，下载解压，`escape_excel-master\release\2017-06-28\EscapeExcelAddin`目录中有`setupEscapeExcel.exe`, 双击安装即可。

![](http://www.ehbio.com/ehbio_resource/excel_escape_addin.gif)

这个插件可以解决以下几种问题，解决方式是在原字符串前加上`=`，并用`"`括起。(只在最开始加个`'`看上去也可以解决问题，没细看作者为啥采用相对复杂的方式)。但是转换后的数据在使用EXCEL的函数时需要注意匹配方式的变化。

![](http://www.ehbio.com/ehbio_resource/excel_escape.PNG)

## 常见受影响基因列表

* 2310009E13
* FEB2
* MAR1
* DEC1
* 2310009E13
* OCT4
* APR1
* SEP2
* SEP-1
* FEB1–FEB11
* MARCH1–MARCH11
* SEPT1–SEPT14

生信分析中经常会做的根据基因名字提取序列、表达量和注释，都会受到这些名字转换的影响，也会受到另外一个常见的换行符的影响`^M`，所以做分析需要谨慎、谨慎、再谨慎。一定多检查结果是否前后一致。

除了要求细心之外，还要求有一定的程序基础，可以从多个角度查看、验证和解决问题，保证一致性。

市面上Linux和Python的课程很多，但真正面向生物数据和生物信息分析的不多。近来频频收到不少朋友说看了我们的生信程序视频课开窍了、入门了，对程序基础的应用理解更深了，我们的课程在<http://bioinfo.ke.qq.com/>可以获取，欢迎更多朋友观看。




1. <https://www.nature.com/articles/ng.3690>
2. <http://blogs.nature.com/naturejobs/2017/02/27/escape-gene-name-mangling-with-escape-excel/>
3. <https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-5-80>
4. <https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0185207>
5. <http://www.theallium.com/biology/scientific-community-capitulates-microsoft-officially-changes-gene-names-dates/>

