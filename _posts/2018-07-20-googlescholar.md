---
title: 如何快准狠地找到相关领域的经典文献？(5年内高引杂志和文献)
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

大多做科研的童鞋们大概都会遇到一个头疼的问题：怎么找文献？如何保证找到的文献都是相关领域的经典文献？之前我们有两篇推送：

* [基于人工智能的文献检索，导师查找，更聪明](http://mp.weixin.qq.com/s/ikU0mVyX6BQNgljD1jCrRA)
* [GeenMedical：文献查询、筛选、引用排序、相似文献、全文下载、杂志分区、影响因子、结果导出、杂志评述、直接投稿，一站服务](http://mp.weixin.qq.com/s/hc8g64aHN7qv8YhVfrsuvQ)

本文教你如何根据H5指数查找相关领域的高精尖经典文献。

首先来了解一下什么是H指数、H5和H5中位数？

* **H指数（H-index）**：于2005年由美国加州大学学圣迭哥分校物理学家 Hirsch 教授提出，用于评价个人学术影响。Hirsch将该指数定义为：若某位科学家的Np篇论文中有h篇论文每一篇的引量都至少为h次，且其他（Np-h）篇论文中每篇的引量都<=h，那么这位科学家的H指数即为h。

* **H5指数**：是指在过去整整5年中所发表文章的H指数；该指数打破了H指数不会随时间的推移而减少，只会增加或保持不变的情况。

* **H5中位数**：是指出版物的H5指数所涵盖的所有文章获得的引用次数的中位值，即H5核内文献的被引频次的中位数。H5中位数指数不考虑 H核内的最低被引频次，而是考虑H核内所有文章的引用次数的中位值来评价期刊刊载的重大研究成果。（备注：H核内是该评价标准中的一个专有名词） 

谷歌学术计量（GSM：Google Scholar Metrics）公布了包括英、汉、葡、德、西、法、韩、日、荷、意10种语言的期刊H5和H5中位数排名，可以进入链接（https://scholar.google.com/citations?view_op=top_venues&hl=en） 查看不同类型期刊的排名。

![](http://www.ehbio.com/ehbio_resource/all_journal_h5.png)

`Nature`排名第一，随后是NEJM和Science，Cell排名第六。Nature communication和`NAR`影响因子虽在10左右，H5 index排名都在前15。`PloS ONE`虽不被看好，排名也在25之内，引用量还是很大的。

点击数字，可以看到近5年文章的引用排名。

`Nature`的前10高引领域分布广，包括深度学习，太阳能电池，登革热、范德华力、癌症基因组突变和微生物组，确实都是比较火的领域。

![](http://www.ehbio.com/ehbio_resource/Nature_h5.png)

新英格兰杂志，各种癌症和慢性病，3篇Melanoma，2篇肺癌，2篇中风，一篇PD-1，[诺贝儿热门领域](https://mp.weixin.qq.com/s/MjmfuKAlNvG8Z2vkxe2ouw)。

![](http://www.ehbio.com/ehbio_resource/NEJM_h5.png)

`Cell`杂志高引文章次数低于Nature和NEJM，排名第一的是**衰老**，最多的是`CRISPR-Cas9`，中国人的名字比较多，张峰、王浩毅、Lei Qi。剩下的是3D Genome和[超级增强子](https://mp.weixin.qq.com/s/2wSNDuz9CtC1ym1QvWHcPg)。

![](http://www.ehbio.com/ehbio_resource/Cell_h5.png)

也可以查看某一个子类，在此我们以生物信息学相关的期刊为例，依次点击`Categories —— Engineering & Computer Science —— Bioinformatics & Computational Biology`即可。

下面为谷歌学术计量统计的从2013-2017年生信期刊H5指数排名

Publication | h5-index | h5-median 
---|---|-
Bioinformatics |	110	| 188
PLOS Computational Biology |	79	| 112
BMC Bioinformatics	| 61	| 86
Briefings in Bioinformatics	| 56	| 81
Database: The Journal of Biological Databases & Curation	| 43	| 63
Journal of Theoretical Biology	| 42	| 69
BMC Systems Biology	| 37	| 50
GigaScience	| 36	| 44
IEEE/ACM Transactions on Computational Biology and Bioinformatics	| 32	| 44
Genomics, Proteomics & Bioinformatics	| 29	| 48
Journal of Mathematical Biology	| 29	| 40
Mathematical Biosciences	| 28	| 36
Journal of Biomedical Semantics	| 26	| 34
Journal of Computational Biology	| 23	| 37
International Conference on Research in Computational Molecular Biology	| 21	| 37
Mathematical biosciences and engineering: MBE	| 20	| 27
Algorithms for Molecular Biology	| 19	| 26
Pacific Symposium on Biocomputing	| 19 | 26
Computational Biology and Chemistry	| 19	| 24
Genomics & Informatics	| 18	| 30

还可以点击各期刊的H5指数链接，查看构成某个期刊H5指数的核心文章。

![img](http://www.ehbio.com/ehbio_resource/H5_index.png)
![img](http://www.ehbio.com/ehbio_resource/H5_indexPaper.png)

排第一的是做系统进化分析的`RAxML`, 第二的是Illumina测序质量过滤工具`Trimmomatic` （高通量测序的发展功不可没），第三和四的`STAR`和`HTseq`常用于处理转录组数据的比对和定量 （实际上STAR自带HTSeq的功能，[易生信 - 转录组专题分析第4期开课啦](https://mp.weixin.qq.com/s/Qv0UR5YHp7oBN5ObbNVznw)）。



这样，你便轻松找到了感兴趣领域里的高引量文献，慢慢享用吧~

可能有人会质疑了，根据H5指数查找是否靠谱？

不要担心，有学者专门做过统计，发现H5指数和H5中位数与传统意义上的期刊评价指数（IF、IF5、ES和AIS）均成极显著正相关，且相关系数大都在0.9以上，表明H5指数和H5中位数在对期刊的评价中有较大的优势。

但同时这样的评价标准也是存在一些问题的，如不能查看谷歌的H5指数往年数据，因此不能进行横向比较；H5指数对于新创刊的期刊或新发文章没有时间优势，可能没办法及时追踪到最新的前沿。

而跟进科研动态的途径有很多，比如1）设置学术期刊或出版公司的电子邮件提醒；2）关注感兴趣作者的社交账号；3）加入科学界的Facebook——Researchgate，里面有很多业内大咖，还有可能与世界同行进行交流；4）定期访问文章官网，查看文章最新动态；5）关注相关专业的论坛和网站等等，但这需要你勤快一点，多多浏览。

找到想要的文献之后，就是如何获取全文了。Sci-Hub是一个提供大量自动且免费的付费学术论文的网站（https://lovescihub.wordpress.com/） ，于2011年由哈萨克斯坦研究生亚历珊卓·艾尔巴金创立，在Pubmed上输入文献名字，获取文章DOI号后，在上述网址中输入文献DOI号即可下载。


