---
title: 生物研究中不得缺少的数字概念
author: ct
layout: post
categories:
  - Bioinfo
tags:
  - Bioinfo
---

对于我们做数据分析的人来说，需要关注很多数字，如[软件安装](http://mp.weixin.qq.com/s/A4_j8ZbyprMr1TT_wgisQQ)时[系统是64位还是32位](http://mp.weixin.qq.com/s/xq0JfkHJJeHQk1acjOAJUQ)，[程序的运行时间多久，运行内存需求多大](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483954&amp;idx=1&amp;sn=11247591a6ef98a4d25404278d577ed0&amp;chksm=ec0dc7b8db7a4eaeb7ae3fd2fa2fbfa7bfd13f5e90d7a42d405f6f8e8783761de048f7ccbc58#rd)，[测序原始文件多大](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484047&amp;idx=1&amp;sn=3e2a79d9f56040a57ac2e16cf1923b54&amp;chksm=ec0dc705db7a4e133e6e91de9ac11a6c0690f03d7b3b760b358e9b0d1a2d57974599419d9fff#rd)，[比对完之后的BAM文件多大，多少基因被检测到了，有多少是差异表达的](http://mp.weixin.qq.com/s/BmtIOcIzIutufFilbJIgEA)等。

生物体内也存在一些数据，对我们直观地了解生物体的大小、理解生物体内部的组织方式和调节方式有重要启发作用。

比如看下面几个例子：

1. 生物体有没有足够的时间复制基因组？

   大肠杆菌的基因组约为**5 M bp**，复制速率在**200-1000 bp/s**。细菌的每条染色体通常只有一个复制起始点。复制子在复制起始位点组装，对向移动，需要至少**2500秒**，也就是41.7分钟完成基因组的复制。而其在营养条件好的情况下分裂一次只需要**20分钟**。那么这是怎么实现的呢？

   实际上，大肠杆菌基因组的复制是**嵌套进行**的。第一次复制未完成时，下一次的复制已经开始了。在任何一个给定的时间点，可以有6个或8个复制叉同时进行DNA的复制。因此当子染色体进入分裂后的子细胞时，已经为下一次的分裂准备好了部分复制的染色体。

2. 5 ml的细菌培养液中有多少突变？

   大肠杆菌复制错误率为**10<sup>-9</sup>/bp**，基因组大小为**10<sup>7</sup>** (双链)，每次基因组复制产生的平均突变为**0.02**个。在5 ml饱和的大肠杆菌培养液中，有**10<sup>9</sup>~10<sup>10</sup>**个细胞。如果只是考虑最后一次复制，从**10<sup>9</sup>**个细胞到**10<sup>10</sup>**个就会产生**10<sup>7</sup>**个单碱基突变 (等同于基因组大小)。如果是从一个菌繁殖而来的，那么理论上每一个非致死性突变都会存在于培养液的菌中。

3. 饱和的大肠杆菌培养液的密度怎样？

   饱和的大肠杆菌培养液中大约有**10<sup>9</sup>** cells/ml。每个细胞重量为**10<sup>-12</sup>**克，悬液的菌浓度是 1 mg/ml。细胞之间的平均距离是**10 um**, 这个密度只有白蚁肠道中菌的密度的**1/10**。可见肠道菌群的丰富。

4. 大分子扩散的距离有多大？

   一个蛋白穿过**HeLa**细胞平均约需要**10 s**。轴突大约是**1 mm**长，HeLa细胞的100倍，而扩散时间与距离的平方成反比，所以大约需要**两天**，一个蛋白才可以从轴突的一端扩散到另一端。这表明需要有其它的机制负责长距离运输大分子。一个速度为**1 um/s**的分子马达可以在**15分钟**一个蛋白运输 **1 mm**的轴突长度。
   
### 大小和长度


细菌(大肠杆菌)：直径0.7-1.4 um；体积 0.5-5 um<sup>3</sup>。10<sup>8</sup>-10<sup>9</sup> cell/ml的菌液OD600约等于1。

酵母(酿酒酵母)：直径3-6 um; 体检 20-260 um<sup>3</sup>。

哺乳动物细胞体积：100-10,000 um<sup>3</sup>；HeLa细胞是500-5000 um<sup>3</sup> (贴壁生长时直径是15~30 um)。

细胞核体积一般为细胞体积的**1/10**。

细胞膜的厚度是 4-10 nm。

平均蛋白的直径是 3-6 nm。

碱基对的大小是：直径 2 nm X 高度 0.34 nm

水分子的直径是 0.3 nm

### 生命过程时间

细胞周期时间：大肠杆菌 20-40 min；出芽酵母 70-140 min; HeLa细胞 15-30 hr。

DNA复制速度：大肠杆菌 200~1000 bases/s; 人 40 bases/s;

RNA聚合酶的转录速速度：10-100 bases/s。

核糖体的翻译速度：10-20 aa/s。

增殖的细胞中mRNA的半衰期小于细胞周期；蛋白的半衰期大于等于细胞周期。

### 基因组大小和突变率

大肠杆菌： 5 Mbp

酿酒酵母：12 Mbp

线虫：100 Mbp

果蝇：120 Mbp

拟南芥：120 Mbp

小鼠：2.5 Gbp

人：2.9 Gbp

小麦：16 Gbp

蛋白编码基因数目

大肠杆菌：4000

酿酒酵母：6000

线虫，拟南芥，小鼠，人：20000

DNA复制突变率 10<sup>-8</sup>~10<sup>-9</sup>/bp

转录的错误插入率是 10<sup>-4</sup>~10<sup>-5</sup>/bp

翻译的错误插入率是 10<sup>-3</sup>~10<sup>-4</sup>/bp

![](http://www.ehbio.com/ehbio_resource/bionumber_sum.png)

这些数字都是实验验证的，但应该作为经验法则而不是一层不变的数字对待。毕竟变化是生活的调味剂，唯一不变的也就只有变化了。

后台回复<数字生物>或点击<http://www.cell.com/pb/assets/raw/journals/research/snapshots/PIIS0092867410006732.pdf>获取原版Snapshot。

更多生物相关的数字见

<http://bionumbers.hms.harvard.edu/search.aspx?task=searchbypop>

公众号

[http://mp.weixin.qq.com/s/JQBZv6snTkZzFwEG12riWw](http://mp.weixin.qq.com/s/JQBZv6snTkZzFwEG12riWw)
