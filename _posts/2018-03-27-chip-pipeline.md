---
title: ChIP-seq基本分析流程
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

前年在中科院做培训时，整理了一套ChIP-seq分析流程，截选实战部分，略作修改，分享出来，希望大家指正。

那次培训内容比较杂，还有关于TCGA、ICGC、ProteinAtlas等数据库的使用, 前面已经分享过，链接如下：

* [UCSC XENA - 集大成者(TCGA,  ICGC)](https://mp.weixin.qq.com/s/we3raL4XowZp4vQ9zPqfYQ)
* [ICGC数据库使用](http://mp.weixin.qq.com/s/UTlEtyDITPx9ZQOpJFczBw)
* [TCGA数据库在线使用](https://mp.weixin.qq.com/s/etg52j9F9uvcGY-qEcAvFQ)

下面步入正题，从ChIP-实验、测序注意事项、测序深度，到分析整体流程，再到每一步如序列比对，富集效率评估、热图、峰图可视化，deeptools2使用、peak calling和motif分析等。

我们也打算于**2018年4月14在北京鼓楼**推出《**ChIP-seq分析专题培训**》，在此基础上继续深入讲解ChIP-seq分析，希望有兴趣的朋友加入。具体见文末或点击 **阅读原文**了解。

![](http://www.ehbio.com/ehbio_resource/ChIP_theory.jpg)

![](http://www.ehbio.com/ehbio_resource/ChIP_analysis1.jpg)

![](http://www.ehbio.com/ehbio_resource/ChIP_analysis2.jpg)

![](http://www.ehbio.com/ehbio_resource/ChIP_analysis3.jpg)

![](http://www.ehbio.com/ehbio_resource/ChIP_analysis4.jpg)


在广大粉丝的期待下，《生信宝典》联合《宏基因组》于**2018年4月14在北京鼓楼**推出《**ChIP-seq分析专题培训**》，为大家提供一条走进生信大门的捷径、为同行提供一个ChIP-seq实战分析学习和交流的机会、助力学员真正理解分析原理和完成实战分析，独创线下集中授课2天+自行练习5天+再集中讲解答疑2天**三段式教学**，并提供学习视频，**教、学、练、答**结合，真正实现独立分析大数据。

关于学习生物信息学分析的重要性，请阅读[《生物信息9天速成班—成为团队中不可或缺的人》](http://mp.weixin.qq.com/s/1nf7vwyvC3oemkTq_pu87A)。

ChIP-seq基本分析流程如上。课程将在这个基础上，提供更深入地分析指导。

1. 座位按报名并成功缴费顺序从前到后龙摆尾式排序。
2. 赠送价值**188元线上生信基础课程一门**，目前的《应用Python处理生物信息数据和作图》、《生物信息作图系列R、Cytoscape及图形排版》和《生物信息中的Linux应用》任选其一。(http://bioinfo.ke.qq.com)
3. 获赠**32G品牌定制U盘** (内含数据资料)。
4. 多人(N，10>N>1)组团报名并同时缴费，每人还可**获得价值N百元的礼品**(京东购物卡)。

具体信息请点击 **阅读原文** (www.ehbio.com/Training)访问。


