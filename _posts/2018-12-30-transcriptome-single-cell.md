---
title: 群体和单细胞转录组数据分析
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

在广大粉丝的期待下，《生信宝典》联合《宏基因组》于**2019年5月3日-2019年5月5日在北京鼓楼**推出《**群体和单细胞转录组数据分析**》专题培训，为大家提供一条走进生信大门的捷径、为同行提供一个转录组实战分析学习和交流的机会、助力学员真正理解分析原理和完成实战分析，独创四段式教学(3天集中授课+自行练习2周+再集中讲解答疑+上课视频回看反复练习)，**"教—练—答—用"四个环节统一协调，真正实现独立分析大数据**。

关于学习生物信息学分析的重要性，请阅读[《生物信息9天速成班—成为团队中不可或缺的人》](http://mp.weixin.qq.com/s/1nf7vwyvC3oemkTq_pu87A)。

## 课程简介

本课程一共3天，每天6节课，共18节课，全部课程均理论与实战结合(只要课上讲的都是可以带你自己实现的分析)。从分析平台搭建、Linux和R基础、图表解读和实战、转录组设计、分析标准流程、差异基因分析、功能富集分析、及各类高级分析(差异剪接、WGCNA分析、通路图绘制等)，单细胞分析 (Cellranger, Seurat, Scater, Monocle)和CNS级图片修改排版。3天时间，老司机带您完成自学需要3个月甚至是1年的崎岖之路，助力您真正玩转转录组分析。

### 课程大纲

每节课1小时一个主题，理论结合实战，学懂原理，实战实操，全是老司机多年经验和代码的无私分享。下面是课程安排，如11代表第一天第一节课，26代表第二天第六节课，41为两周后的线上集中视频答疑。

编号 | 主题 | 简介
---|---|-
11|转录组概述|转录组设计、应用、批次效应等
12|转录组分析流程简介|基于/不基于比对的分析流程讲演
13|Salmon定量实战|不基于比对直接定量基因和转录本的表达
14|差异基因分析|DESeq2差异基因分析
15|富集分析和可视化|GO富集分析
16|富集分析和可视化|GSEA富集分析
17|R基础|数据读写、处理和可视化
21|二代三代测序原理介绍|建库测序过程及注意事项
22|转录组软件安装|Linux下一键配置
23|STAR比对拼装差异剪接|和差异基因分析
24|WGCNA基因加权共表达|网络分析和性状关联
25|Cytoscape绘制|共表达网络和调控通路网络图
26|文章常见图表解读|和Illustrator制作CNS标准图版
27|Linux基础|详细解释代码和文件格式转换
31|单细胞转录组特点介绍|注意事项
32|单细胞数据预处理|细胞和基因筛选
33|单细胞分型PCA, TSNE, SC3聚类|Seurat, Scater使用
34|单细胞发育演化分析|Pseudotime, Monocle使用
35|单细胞Marker基因鉴定|差异分析，功能分析
36|考试、圆桌论坛|自评学习效果、知识点回顾
41|答疑-线上|答疑、考试内容串讲

**教程内容简介如下：**

### 转录组的应用、设计和案例分享

![](http://www.ehbio.com/ehbio_resource/Transcriptome_product.jpg)

1. 转录组学研究技术介绍
2. 转录组学实验设计和测序原则、注意事项
3. [二代](https://mp.weixin.qq.com/s/SS9YBSpgUoU9gI86u-0ATg)、三代测序过程和原理解析
4. 转录组学文章案例分析
5. 在线基因表达资源数1据库

### 转录组分析流程实战

![](http://www.ehbio.com/ehbio_resource/Transcriptome_flow.png)

1. [转录组分析流程评估](https://mp.weixin.qq.com/s/NUEi6oRFL7B3f1FpCD4Xug)
2. [测序数据质量评估和清洗](https://mp.weixin.qq.com/s/tDMih7ISLJcL4F4sWBq3Vw)
2. 不基于比对的[差异基因分析](https://mp.weixin.qq.com/s/Vmhx_TGxNkQzkekf93Xl4w)
3. 基于比对的差异基因分析
4. 转录本组装和选择性剪接分析
5. [目标基因GSEA/GO富集分析](https://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg)

### 常见图表解读和图形编辑排版

在培训上，结合发表高水平文章，进一步讲解16种常用分析图的原理和使用范围，让你不仅读懂图，更知道如何应用于自己的研究，并亲自轻松完成绘图。

针对大家使用R语言绘图学习时间成本较高的问题，易生信团队针对常用16种图开发了[免费绘图网站](https://mp.weixin.qq.com/s/MnM_MyosBdEvKV0W018KeA)，一键出图，更可鼠标点选参数修改图形的个性样式。

成果发表是科研过程中不可缺的一部分，发表成果又少不了图形展示。文章图表排版是否整齐规范、协调一致、重点突出对一篇文章的发表也是有不少贡献的。之前推出的[文章发表图的修改和排版](https://mp.weixin.qq.com/s/IJNyhinakY0lSXgCN7b9ug)讲演了部分图形编辑和排版操作，本次培训也会实践从原始图形、到细节修饰再到排版发表的整个过程和注意事项。

### 转录组高级分析

![](http://www.ehbio.com/ehbio_resource/WGCNA_flow.png)

1. [WGCNA基因共表达分析](https://mp.weixin.qq.com/s/PMb2xwADvnMwaipyFXdtzQ)
2. WGCNA基因、表型关联分析
3. [Cytoscape 共表达网络](https://mp.weixin.qq.com/s/sKEy_Pn9qnWw4W-aXraA5g)绘制
4. 转录组常见图形在线绘制
5. [KEGG/Reactome通路图绘制](https://mp.weixin.qq.com/s/jI6Gz1JKxnGB9jDRSFjd0g)，表达映射
6. [基因互作的文献挖掘和数据库挖掘](https://mp.weixin.qq.com/s/1LNae0pG0w_Q-rRxhI96Pg)展示

### 单细胞转录组分析

![](http://www.ehbio.com/Training/Public/images/singlecell.png)

1. 单细胞数据预处理和校正
2. 细胞分型，PCA,  TSNE,  SC3聚类 (Seurat, Monocle, Scater)
3. 单细胞发育演化分析
4. 转录组常见图形在线绘制
5. 单细胞Marker基因鉴定，差异分析和功能分析

### 生信基础知识

1. Linux/Windows下Rstudio和Linux命令的使用
2. Linux/Windows下转录组分析流程的搭建

生物学家必要掌握的[Shell](https://mp.weixin.qq.com/s/rXjQfyEX2FnuW9HTM_Uc8Q)和[R语言](https://mp.weixin.qq.com/s/EZ8R4v4f_jU3aaUP-1p1MQ)基础知识。

(如果基础薄弱，报名付款成功后，可免费**领取[基础程序课](https://ke.qq.com/course/289264)**，做好准备工作, [让程序成为我们的得力工具而不是学习新知识的绊脚石](http://mp.weixin.qq.com/s/u8AmzvO0-PIS33ficKOrUQ)。)

### 定制内容

如果您看到文章中有哪些图或分析工作需要重现，也请提出，一起讲述。

如果您有其它关注的问题，也请报名时提出，把这次课程变成您的**定制讲解**。

### 120分的转录组试题来测试下

* [120分的转录组试题（第一份答案）](https://mp.weixin.qq.com/s/lsaubsJofGRbCVnrhmTygw)
* [120分的转录组试题（第二份答案）](https://mp.weixin.qq.com/s/Vh2c-JegoaMr0Ws2gDuFhA)
* [120分的转录组试题（第三份答案）](https://mp.weixin.qq.com/s/BadU3ZVPAlxBn0_QehVnXQ)


### 往期精彩回顾

![image](http://bailab.genetics.ac.cn/markdown/train/1809/41.jpg)
![image](http://www.ehbio.com/Training/Public/assets/images/sandai.jpg)
![image](http://www.ehbio.com/ehbio_resource/%E4%BA%8C%E4%BB%A3%E4%B8%89%E4%BB%A3%E8%BD%AC%E5%BD%95%E7%BB%84%E6%B5%8B%E5%BA%8F_%E8%85%BE%E8%AE%AF%E8%AF%BE%E5%A0%82_%E8%AF%84%E4%BB%B7.png)


### 主讲教师


陈同，博士，2015毕业于中科院遗传与发育生物学研究所，生物信息专业博士，在Cell Stem Cell(IF=23.2，第一作者兼封面文章)，Nucleic Acids Research，Stem Cells and Development等高水平杂志以第一作者或主要作者发表文章，运营有数万人关注的[《生信宝典》](https://mp.weixin.qq.com/s/2b3_8Vvv7McqCkEfUszW3A)微信公众号，给你不一样的学习生信体验。 


刘永鑫，博士。2008年毕业于东北农大微生物学专业。2014年中科院遗传发育所获生物信息学博士学位，2016年博士后出站留所工作，任宏基因组学实验室工程师，目前主要研究方向为宏基因组学数据分析与可重复计算。发表论文10余篇，SCI收录7篇。2017年7月创办[“宏基因组”公众号](https://mp.weixin.qq.com/s/oa1M7FZ7f4PUtIsE5QZdMA)，目前分享宏基因组、扩增子原创文章185篇，关注人数2.3万人，累计阅读近300万次。

### 助教团队

十余名中国科学院、清华、北大博士(含在读)，轮值讲师和助教，辅助学员学习和矫正培训过程中不足的点。 

### 授课模式

本课程以讲解流程和实际操作为主，采用独创四段式教学，封装好的代码全部分享，随处可用：

- 第一阶段 3天集中授课；
- 第二阶段 自行练习2周；
- 第三阶段 在线直播答疑；
- 第四阶段 培训视频继续学习；
- 实现教-练-答-用四个环节的统一协调。

### 培训时间

2019-5-3 到 2019-5-5 (线下讲解实战)  
每天早9点到晚6点，半封闭式教学 (最后1小时为集中讨论时间，最后一天会稍微提前一些，多留出时间讨论，也方便老师乘车返回)  
报到时间：开课当天


### 授课地点

北京市西城区鼓楼附近

### 课程价格

1. 截止 2019-4-26  4500 元/人
2. 名额有限，每次课程报名满40人后自动关闭报名通道
3. 提供易汉博基因科技实习机会或工作机会

### 课程福利

1. 座位按报名并**缴费或预付款成功**顺序从前到后龙摆尾式排序 
2. 赠送程序基础课一份 (http://bioinfo.ke.qq.com)
3. 多人 (N，10>N>1) 组团报名并同时缴费，每人还可减免**N-1**百元 (最高500)
4. 赠送金士顿U盘一个（32G含培训数据和脚本）
5. 附推荐语分享对应的招生信息到朋友圈，截图发到train@ehbio.com 可获得**200元**生信宝典腾讯课堂课程优惠券（可拆分供多个课程使用）

**注意事项** *

1. 需自备笔记本电脑，推荐使用win10系统，4G以上内存(推荐8G)。课程实践根据需要会提供云计算平台
2. 培训班所有数据，文档为内部资料，仅供参阅，未经允许不得翻印外传登刊
3. 上课期间禁止录音，录像
4. 成功付款的学员，若临时有紧急事情不能到来的，可申请延期，更换后续培训班；也可申请退款
5. 若开课2周 (含) 前申请退款可退还85%费用；开课3个工作日 (含) 前申请退款退还70%的费用 (若已开发票需承担相应手续费)
6. 不可先延期再退款
更多课程的详细介绍，请扫描下方二维码。

![image](http://bailab.genetics.ac.cn/markdown/train/1809/easy_bio_qr.png)

![image](http://bailab.genetics.ac.cn/markdown/train/1809/201807.jpg)

复制以下链接
http://www.ehbio.com/Training/ 或
点击**阅读原文**跳转报名页，成为实验中不可或缺的人，赶快报名吧！

