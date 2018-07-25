---
title: 宏基因组培训
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

### 课程简介

宏基因组/微生物组是当今世界科研最热门的研究领域之一，为加强本领域的技术交流与传播，推动中国微生物组计划发展，中科院青年科研人员创立“宏基因组”公众号，目标为打造本领域纯干货技术及思想交流平台。成立11个月，分享专业技术原创文章近200篇，关注人数20000+，累计阅读超2百万次。

为满足广大读者进一步学习的需求，现联合《生信宝典》组织宏基因组学专题培训课程，进一步学习和交流宏基因组学分析技术，手把手带您快速入门、节约宝贵的时间，助力科研成果早日产出。

课程涉及主要内容如下：

#### 一、宏基因组学概述

1. 背景：国际微生物组、中国微生物组计划
2. 研究对象：人、动物、植物、环境
3. 研究方法：培养组学、扩增子、宏基因组、宏转录组、宏蛋白组、宏代谢组、宏基因组关联分析、宏表观组……
4. 宏基因组学的研究热点：培养组、肠菌与疾病、宏基因组关联分析(MWAS)、多组学联合分析……

![image](http://bailab.genetics.ac.cn/markdown/train/180601overview.jpg)

#### 二、宏基因组测序原理和实验设计

1. 测序发展史与原理
2. 样品制备、实验重复和测序数据量的选择
2. 正确设计实验组与正/负对照
3. 样品制作和建库中的误区、注意事项
4. 宏基因组分析SCI文章的常用套路
5. 宏基因组与扩增子优缺点比较

#### 三、宏基因组常用结果解读

1. 原始数据评估、组装结果好坏的判断
2. 基于基因丰度样品、组间差异展示：相关性、PCA、PCoA、CCA等结果怎么看
3. 差异物种展示和功能通路结果常用图
4. 圈图用场景：多层级比例、差异、基因拼接展示、分类功能基因来源分布等
5. 韦恩图、三元图展示三组及多组间相同与不同
6. 网络图与分组、环境因子相关的意义

#### 四、宏基因组分析流程讲解及实战

1. 实验设计的编写原则
2. HiSeq数据的质控：fastqc, kneaddata Trimmomatic, MultiQC, khmer
3. 物种和功能组成量：metaphlan2, humann2
4. 宏基因组拼接和评估：megahit, SPAdes、quast
5. 基于kmer样品和组间差异分析：sourmash
6. 基因注释：Prokka
8. 基因丰度估计：bwa, salmon等方法快速基因丰度定量，后续可进行PCA、PCoA、CCA等整体组间差异比较；进一步进行edgeR、metastat、Lefse进行组间差异基因分析；
9. 物种注释：获得非冗余基因集物种注释信息，结合第8步丰度值可进行组间差异物种分析；
10. 基因功能分类注释：代谢通路(KEGG)，同源基因簇(eggNOG)注释，结果8中丰度进行组间差异功能比较；

![image](http://bailab.genetics.ac.cn/markdown/train/pipeline_metatranscriptomics.jpg)


#### 五、高级分析与可视化实战

1. R语言统计绘图与可重复计算
2. 宏基因组中鉴定单菌(分箱bin)：Maxin, metabin
3. Bin结果评估及可视化：CheckM, VizBin
5. 有参宏基因组分析：MetaPhlAn2、Humann2
6. 在线绘图：Echart
8. 网络分析: igraph、WGCNA、Cytoscape
9. 其它常用：Graphlan、Krona、iTol


## 你能得到时什么

**深彻理解生物测序数据的基本思想**

![image](http://bailab.genetics.ac.cn/markdown/train/180520think.jpg)

**宏基因组分析三种模式全面的解决方案，以及结果的统计分析**

- 16S扩增子数据PICRUST预测宏基因组
- 宏基因组数据Humann2定量物种和功能
- Denovo宏基因组拼接和binning
- 结果的差异比较和可视化

![image](http://bailab.genetics.ac.cn/markdown/train/180520pipeline.jpg)


### 主讲教师

主讲老师包括中科院微生物所、遗传发育所、基因组所、生物物理所等多名本领域一线技术专家。


### 助教团队

十余名科学院、清华、北大博士(含在读)，轮值讲师和助教，辅助学员学习和矫正培训过程中不足的点。 

### 培训时间

2018-07-14 到 2018-07-15 (线下讲解实战)  
2018-07-21 到 2018-07-22 (可线上线下同时，照顾不能长时间在北京的朋友)  
每天早9点到晚5点，半封闭式教学  
报到时间：开课当天课前半小时内


### 授课地点

北京市西城区鼓楼明德大厦 (北京市旧鼓楼大街47号院2号楼2010)。 

### 课程价格

1. 原价 6999 元/人，   
截止 2018-06-29  4199 元/人  
之后恢复原价6999元/人 (住宿自行解决，提供培训期间午餐)
2. 名额有限，本次课程报名满40人后自动关闭报名通道，目前己有澳大利亚、广州、广西、武汉等30余名朋友报名，仅剩不到十个名额了。
3. 提供易汉博基因科技实习机会或工作机会

### 暑期促销优惠活动

在**2018年6月底前报名且成功缴费**的用户，不仅可以获得上课的前排座位(座位按报名并成功缴费顺序从前到后龙摆尾式排序)，更可同时享受如下四重优惠。

1. 赠送价值**188元线上生信基础课程一门**，目前有《应用Python处理生物信息数据和作图》、《生物信息作图系列R、Cytoscape及图形排版》和《转录组高级分析》和《生物信息中的Linux应用》任选其一。
2. 获赠**32G品牌定制U盘** (内含数据资料)。
3. 多人(N，10>N>1)组团报名并同时缴费，每人还可**获得价值N百元的礼品**(充值或购物卡)。
4. 零元学习588元微生物扩增子实战分析，学员预先购买课程，待完成宏基因组线下课程者，返现90%(10%被腾讯课堂扣除)。


***注意事项**

1. 需自备笔记本电脑，系统不限(**推荐使用Windows 10系统，8G内存，Google Chrome浏览器**)。课程实战练习提供云计算平台。
2. 培训班所有数据，文档为内部资料，仅供参阅，未经允许不得翻印外传登刊。
3. 上课期间禁止录音，录像。
4. 成功付款的学员，若临时有紧急事情不能到来的，可申请延期，更换后续培训班；也可申请退款。
5. 若开课2周 (含) 前申请退款可退还85%费用；开课3个工作日 (含) 前申请退款退还70%的费用。
6. 不可先延期再退款。

更多课程的详细介绍，请扫描下方二维码。

![image](http://bailab.genetics.ac.cn/markdown/train/easy_bio_qr.png)

复制以下链接
http://www.ehbio.com/Training/ 或
点击**阅读原文**跳转报名页

成为实验中不可或缺的人，赶快报名吧！


## 宏基因组相关学习资源

自学能力强、基础好的同学，如果把我们之前分享的资料全部掌握的话，应该可以自行解决本领域的绝大多数分析问题。


**教程系列**
 
- [宏基因组分析教程](http://mp.weixin.qq.com/s/bcyvhFrNr6niqD13rQfZeg)
- [4500元的微生物组培训资料](http://mp.weixin.qq.com/s/li7SdZVaCEyFQF8h6MMh2A)
- [微生物组助手——最易学的扩增子、宏基因组分析流程](https://mp.weixin.qq.com/s/UYzDiwvPChGpw70k6sU0Bg)
- [GigaScience：ASaiM基于Galaxy微生物组分析框架](https://mp.weixin.qq.com/s/qP16gZCFX6o7kzwQq5cwMQ)
- [斯坦福大学统计系教授带你玩转微生物组分析](https://mp.weixin.qq.com/s/Zcjhi6fnXQHIqPodDSPBnw)

**有参分析**
- [MetaPhlAn2一条命令获得宏基因组物种组成](https://mp.weixin.qq.com/s/hpJtU8I8OTPmwOeFh7R2VQ)
- [HUMAnN2：人类微生物组统一代谢网络分析2](https://mp.weixin.qq.com/s/Ee72jnZR4bXLjd8jEYYSFQ)
- [宏基因组有参流程Metagenomics Tutorial (HUMAnN2)](https://mp.weixin.qq.com/s/XkfT5MAo96KgyyVaN_Fl7g)


**De novo**
- [1背景知识-Shell入门与本地blast实战](http://mp.weixin.qq.com/s/jASOBPzpwYCL-fWNUJJp8g)
- [2数据质控fastqc, Trimmomatic, MultiQC, khmer](http://mp.weixin.qq.com/s/3O01eNMe79J_kUTaJjP6ag)
- [3组装拼接MEGAHIT和评估quast](http://mp.weixin.qq.com/s/NMKX0iDuR_qOzmLXxC8MEQ)
- [4基因注释Prokka](http://mp.weixin.qq.com/s/1TM61IrzrpVb5KhZ5A0kZQ)
- [5基于Kmer比较数据集sourmash](https://mp.weixin.qq.com/s/Rmx-z1zxj7GF9ivJGWVvLg)
- [6不比对快速估计基因丰度Salmon](http://mp.weixin.qq.com/s/2fwEtnEsBi5cJ65xyeoXxw)
- [7bwa序列比对, samtools查看, bedtools丰度统计](http://mp.weixin.qq.com/s/rdTFTFg0rZOIa2_tuFEOUA)
- [8分箱宏基因组binning, MaxBin, MetaBin, VizBin](http://mp.weixin.qq.com/s/rZitcvykAlxnsNEzsW5JRg)
- [9组装assembly和分箱bin结果可视化—Anvi'o](http://mp.weixin.qq.com/s/FesH_mCunpZLpKC2pIg1UQ)
- [10绘制圈图-Circos安装与使用](http://mp.weixin.qq.com/s/FJlKY3kU5Fm6bYkjtwRkEw)

**统计分析及可视化**
- [Krona绘制物种或功能组成圈图](https://mp.weixin.qq.com/s/62CXHcz9ZisVsRgbUjTK8A)
- [microbiomeViz：绘制lefse结果中Cladogram](https://mp.weixin.qq.com/s/psGD9-AxgcCfclGhOKR1mQ)
- [MMinte：预测微生物群体内代谢物互作](https://mp.weixin.qq.com/s/1CXMxVlMq8HpvMtTNALKkQ)

如果基础知识体系不完善，自学存在困难的小伙伴，急时上车也是不错的选择。

成为实验中不可或缺的人，赶快报名吧！

## 猜你喜欢

- 10000+：[肠道细菌](http://mp.weixin.qq.com/s/3T768LA6MWujF4yuzK4MKQ) [人体上的生命](http://mp.weixin.qq.com/s/_DUI6tOYTEq0Wu7K7iRTxw) [宝宝与猫狗](http://mp.weixin.qq.com/s/K3y3an-EaX8iaytmxdzHqA) [梅毒狂想曲](http://mp.weixin.qq.com/s/XfeuKLLg3ruXUCFnFAisog) [提DNA发Nature](http://mp.weixin.qq.com/s/lO5uiMjixJ6aYTjPX-IyaQ) [实验分析谁对结果影响大](http://mp.weixin.qq.com/s/cL_IAoPFfmelKMPMgltrfA)  [Cell微生物专刊](https://mp.weixin.qq.com/s/fN0gpD3bZJDXSp8x4ck-3Q)
- 系列教程：[微生物组入门](http://mp.weixin.qq.com/s/sQyl5EctXFB95Oxg8YIasg) [Biostar](http://mp.weixin.qq.com/s/JL-n2nD6YL8vwuRtTVmQlQ) [微生物组](http://mp.weixin.qq.com/s/li7SdZVaCEyFQF8h6MMh2A)  [宏基因组](http://mp.weixin.qq.com/s/bcyvhFrNr6niqD13rQfZeg) 
- 专业技能：[生信宝典](http://mp.weixin.qq.com/s/2b3_8Vvv7McqCkEfUszW3A) [学术图表](http://mp.weixin.qq.com/s/SCT4oso_vI0UNIJZTaG95g) [高分文章](http://mp.weixin.qq.com/s/kD-x7K4hI5KMgGXikyLt0Q) [不可或缺的人](http://mp.weixin.qq.com/s/1nf7vwyvC3oemkTq_pu87A) 
- 一文读懂：[宏基因组](http://mp.weixin.qq.com/s/Vsm6BJgqsSvxEenIBrGVLw) [寄生虫益处](https://mp.weixin.qq.com/s/hX0K9TOLPnrZ6f8lUoSYag) [进化树](https://mp.weixin.qq.com/s/GV8rU3FZdc8Y-x931k_yrQ)
- 必备技能：[提问](http://mp.weixin.qq.com/s/xCif04bqZB14Z4OvesK0SQ) [搜索](http://mp.weixin.qq.com/s/wn2bqIPgT5UD-GP1qzkJFA)  [Endnote](http://mp.weixin.qq.com/s/SPblPs5ByPdb2C400kIK3w)
- 文献阅读 [热心肠](http://mp.weixin.qq.com/s/1uBeAQ0utxuzTTtfUx_UXA) [SemanticScholar](https://mp.weixin.qq.com/s/gaQiUrRqLpfTXzjyfbua6A) [Geenmedical](https://mp.weixin.qq.com/s/hc8g64aHN7qv8YhVfrsuvQ)
- 扩增子分析：[图表解读](http://mp.weixin.qq.com/s/oiVHO2S1JgYrKXPDU6fH2g) [分析流程](http://mp.weixin.qq.com/s/KrYyy3jjzAL0rQzVfV6h4A) [统计绘图](http://mp.weixin.qq.com/s/6tNePiaDsPPzEBZjiCXIRg) 
- [16S功能预测](http://mp.weixin.qq.com/s/sztbvfdf9wa-3HJXc_m8TQ)   [PICRUSt](https://mp.weixin.qq.com/s/LWtiwBbUCAadMZPaKKDMag)  [FAPROTAX](http://mp.weixin.qq.com/s/J8EwJD_PTDhqRaD7kXlK1A)  [Bugbase](https://mp.weixin.qq.com/s/1WdysPZWo0H6NSYiNpcMUQ) [Tax4Fun](http://mp.weixin.qq.com/s/dzsh44ue93xnAs7gTde7wg)
- 在线工具：[16S预测培养基](http://mp.weixin.qq.com/s/YIrDqNvDX0XMazCGxhH1Lg) [生信绘图](http://mp.weixin.qq.com/s/O0QAQyfxnrXlFLw268B7lg)
- 科研经验：[云笔记](http://mp.weixin.qq.com/s/OnwhWlq3cTycf-W1rxgV7g)  [云协作](http://mp.weixin.qq.com/s/W5By9mZ5PI57_xFfZ_JXiw) [公众号](http://mp.weixin.qq.com/s/hd0sdBDAMqMJsXQs0pIjUg)
- 编程模板 [Shell](http://mp.weixin.qq.com/s/YevGR79NnBAF-xtrqL8gAA)  [R](http://mp.weixin.qq.com/s/OQiE882jM6pVwqTiIjyZ1Q) [Perl](http://mp.weixin.qq.com/s/u2ZmTo-z6cbN-L6KVLYNwg) 
- 生物科普  [生命大跃进](http://mp.weixin.qq.com/s/O_0Il0G_v_aSwkUH_noZVA)  [细胞暗战](http://mp.weixin.qq.com/s/M35ebWAelDIK5Iqib06JzA) [人体奥秘](https://mp.weixin.qq.com/s/xlCdN8il1hcutkYK-42fAQ)  


## 写在后面

为鼓励读者交流、快速解决科研困难，我们建立了“宏基因组”专业讨论群，目前己有国内外1700+ 一线科研人员加入。参与讨论，获得专业解答，欢迎分享此文至朋友圈，并扫码加主编好友带你入群，务必备注“姓名-单位-研究方向-职称/年级”。技术问题寻求帮助，首先阅读[《如何优雅的提问》](http://mp.weixin.qq.com/s/H9gkepap0hy3NNskOkO44w)学习解决问题思路，仍末解决群内讨论，问题不私聊，帮助同行。
![image](http://bailab.genetics.ac.cn/markdown/life/yongxinliu.jpg)

学习扩增子、宏基因组科研思路和分析实战，关注“宏基因组”
![image](http://bailab.genetics.ac.cn/markdown/life/metagenome.jpg)

点击阅读原文，跳转最新文章目录阅读
https://mp.weixin.qq.com/s/5jQspEvH5_4Xmart22gjMA
