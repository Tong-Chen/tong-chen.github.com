---
title: 蛋白质组学研究概述
author: zzy
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

本篇介绍下蛋白质组学，如果价格便宜的话，应该是新时代的宠儿了。

![](http://www.ehbio.com/ehbio_resource/proteomics/2.jpg)

古希腊，一个神一样的存在，不只有雅典娜，更孕育了“ome”等一批高大上的词汇。组学表示一组物质整体的表现。蛋白质组学表示特定系统内蛋白质集合的研究。

![](http://www.ehbio.com/ehbio_resource/proteomics/3.jpg)

蛋白质组学有基于二维凝胶分离 (2D-Gel)和质谱鉴定技术。

![](http://www.ehbio.com/ehbio_resource/proteomics/4.jpg)

2D-Gel根据蛋白的等电点和分子质量的差异，通过等点聚焦和SDS-PAGE分离，通过染色和成像把不同电性和大小的蛋白质显示在凝胶上。

![](http://www.ehbio.com/ehbio_resource/proteomics/5.gif)

点的密度、大小、位置不同可以定性查看有无和相对定量地查看丰度差异。

![](http://www.ehbio.com/ehbio_resource/proteomics/6.gif)

chromatography 层析、色谱，(graphy也来源于希腊文，意为 **写**)。携带样品的流动相穿过固定相时，由于样品各组分理化性质存在差异，与固定相作用力弱的组分，移动速度快；反之，移动速度慢。根据不同的保留时间，收集特定属性的样品进行进一步分析。根据流动相的不同又分为气相色谱和液相色谱。

![](http://www.ehbio.com/ehbio_resource/proteomics/7.gif)

高效液相色谱，又称为高压液相色谱，高速液相色谱。流动相为液体，在高压作用下快速流过固定相，分离效能高，灵敏度高，应用范围广，柱子可反复使用。最早洗脱出的是越亲水的。

![](http://www.ehbio.com/ehbio_resource/proteomics/8.gif)

质谱是测量离子质荷比的分析方法，基本原理是使待测样品中的组分在离子源中离子化，经过电场加速形成离子束，进入质量分析器，获得质谱图。与Uniprot数据库比较，得到对应的蛋白定量。


![](http://www.ehbio.com/ehbio_resource/proteomics/9.gif)

常用离子源有：基质辅助激光解吸电离（MALDI）；电喷雾电离（ESI）。

![](http://www.ehbio.com/ehbio_resource/proteomics/10.gif)

飞行时间质谱 (TOF)，分析物的质荷比是根据分析物在真空飞行管中的飞行时间推算出的。飞行时间质谱的质量分析器由调制区、加速区、无场飞行空间和检测器等部分组成。样品分子电离以后，将离子加速并通过一个无场区，不同质量的离子具有不同的能量，通过无场区的飞行时间长短不同，可以依次被收集检测出来。

四极杆 (Quadrupole，Q)质谱仪，从单级四极杆到三级四极杆, 功能越来越强。第一级四极杆选母离子，第二级四极杆作为碰撞室对母离子进行碰撞解离，第三级四极杆作为质量分析器完成离子分析。三级四极杆采集到的MS/MS质谱图信息量大，并且较少发生重排反应，因而四极杆的质谱数据质量要高于离子阱串联质谱数据。

离子阱 (Orbitrap)质谱仪，串联质谱仪，在分析前先将离子聚集储存，离子阱是该仪器的核心部分，既可以作为碰撞室，又可以作为质量分析器。分为线性离子阱和三维离子阱。线性离子阱具有更大的离子容量和扫描速度。


![](http://www.ehbio.com/ehbio_resource/proteomics/11.gif)

蛋白质组实验流程文字和图形总结

![](http://www.ehbio.com/ehbio_resource/proteomics/12.jpg)
![](http://www.ehbio.com/ehbio_resource/proteomics/13.jpg)

定性蛋白质组学

![](http://www.ehbio.com/ehbio_resource/proteomics/14_2.jpg)

从样品中分析全蛋白，胰蛋白酶消化成多肽，经液相色谱-质谱检测，比较实际检测到的质荷比和理论预测的质荷比，鉴定蛋白的种类。

![](http://www.ehbio.com/ehbio_resource/proteomics/15.gif)
![](http://www.ehbio.com/ehbio_resource/proteomics/16.gif)

离子的属性和质量不同会产生不同的质量指纹图谱。

![](http://www.ehbio.com/ehbio_resource/proteomics/17.jpg)

若多肽的氨基酸组成一样，但顺序不同，如何区分？

![](http://www.ehbio.com/ehbio_resource/proteomics/18.jpg)

串联质谱，先获得小肽的质量；再将肽离子诱导碰撞碎裂成更小的碎片离子，获得二级质谱图谱。

![](http://www.ehbio.com/ehbio_resource/proteomics/19.gif)

不同的片段化方式会得到不同的片段

![](http://www.ehbio.com/ehbio_resource/proteomics/20.gif)

![](http://www.ehbio.com/ehbio_resource/proteomics/21.gif)

![](http://www.ehbio.com/ehbio_resource/proteomics/22.gif)

MASCOT软件搜库鉴定蛋白

![](http://www.ehbio.com/ehbio_resource/proteomics/23.gif)

鉴定蛋白翻译后修饰

![](http://www.ehbio.com/ehbio_resource/proteomics/24.gif)

磷酸化肽段富集 （类比于ChIP中的富集和Input）

![](http://www.ehbio.com/ehbio_resource/proteomics/25.gif)
![](http://www.ehbio.com/ehbio_resource/proteomics/26.gif)
![](http://www.ehbio.com/ehbio_resource/proteomics/27.jpg)

定量蛋白质组学

![](http://www.ehbio.com/ehbio_resource/proteomics/28_2.jpg)

![](http://www.ehbio.com/ehbio_resource/proteomics/29.jpg)

Label free相对定量，蛋白的量与Peak强度正相关。

![](http://www.ehbio.com/ehbio_resource/proteomics/30.gif)

酶解标记法, 酶解时加入H<sub>2</sub><sup>18</sup>O，可以在肽段C端加2个重氧原子。

![](http://www.ehbio.com/ehbio_resource/proteomics/31.gif)

iTRAQ 技术采用4种或8种同位素编码的标签，通过特异性标记多肽的氨基基团，而后进行串联质谱分析，可同时比较4种或8种不同样品中蛋白质的相对含量或绝对含量。

![](http://www.ehbio.com/ehbio_resource/proteomics/32.gif)

SILAC: 两组细胞同时培养，A组是在包含正常氨基酸（light）的培养基中；B组的培养基则含有“重型（heavy）”的氨基酸，即稳定同位素标记的氨基酸。最初SILAC使用的标记氨基酸是氚代甲硫氨酸和氘代甘氨酸，目前常用的标记氨基酸有亮氨酸、精氨酸、赖氨酸、甲硫氨酸和酪氨酸等。细胞传代若干代后，稳定同位素标记的氨基酸完全掺入到蛋白中，取代了原有的氨基酸。这样，两个蛋白之间就存在分子量的改变，而其它化学性质无异。

![](http://www.ehbio.com/ehbio_resource/proteomics/33.gif)



![](http://www.ehbio.com/ehbio_resource/proteomics/34.jpg)
![](http://www.ehbio.com/ehbio_resource/proteomics/35.jpg)


![](http://www.ehbio.com/ehbio_resource/proteomics/36_2.jpg)

现存技术的缺点

![](http://www.ehbio.com/ehbio_resource/proteomics/37.gif)

靶向蛋白质组技术主要包括SRM/MRM和PRM两种方法。SRM/MRM （Selected/ Multiple reaction monitoring）使用的是三重四级杆的质谱，利用四级杆高选择性的特点对母离子和子离子依次进行分选。

PRM（Parallel reaction monitoring）技术，该技术结合了四级杆的高选择性以及Orbitrap的高分辨、高精度特性，能够对二级图谱进行独立的鉴定，方法流程更加便捷。与传统的SRM/MRM相比，PRM在复杂背景下具有更优秀的抗干扰能力和检测灵敏度。

![](http://www.ehbio.com/ehbio_resource/proteomics/38.gif)

![](http://www.ehbio.com/ehbio_resource/proteomics/39.gif)

同源搜索或结合转录组数据解决注释缺失的问题

![](http://www.ehbio.com/ehbio_resource/proteomics/40.gif)
![](http://www.ehbio.com/ehbio_resource/proteomics/41.jpg)

总结

![](http://www.ehbio.com/ehbio_resource/proteomics/42.gif)

Ref:
1. http://www.360doc.com/content/15/0529/20/11644963_474287763.shtml
2. http://tech.sina.com.cn/roll/2017-06-05/doc-ifyfuzym8006769.shtml
3. https://www.thermofisher.com/cn/zh/home/life-science/protein-biology/protein-mass-spectrometry-analysis/protein-quantitation-mass-spectrometry/silac-metabolic-labeling-systems.html
4. https://baike.baidu.com/item/%E5%90%8C%E4%BD%8D%E7%B4%A0%E6%A0%87%E8%AE%B0%E7%9B%B8%E5%AF%B9%E5%92%8C%E7%BB%9D%E5%AF%B9%E5%AE%9A%E9%87%8F/12756990?fr=aladdin&fromid=347038&fromtitle=iTRAQ
