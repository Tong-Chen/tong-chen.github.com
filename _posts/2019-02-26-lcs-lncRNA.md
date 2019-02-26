---
title: 超简便的国产lncRNA预测工具LGC
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

在过去几年里，研究发现`long non-coding RNAs (lncRNAs)`在疾病和生物调控过程中扮演着重要角色。但在大量非模式物种中lncRNA的鉴定仍是一项富有挑战性的工作。该工作需要确定的序列信息，注释信息以及构建物种特有的训练集，但具有lncRNA研究所需的足够完整的序列与注释的物种只占很少数。
LGC是由北京基因组所基于python2 ([Python极简教程（一）](https://mp.weixin.qq.com/s/9BNrq8Lu7hjtO2BAKOIXOA))开发的一款快速lncRNA预测工具，该工具通过`ORF`（开放阅读框）长度和`G`C含量间的关系进行相关运算来鉴定lncRNA。LGC最大特点是能够基于**跨物种策略**进行lncRNA发掘。因此LGC可以支持**有参数据**和**无参数据** ([无参转录组分析工具评估和流程展示](http://mp.weixin.qq.com/s/4HANWJY4oL7jGziroHfEpQ))进行`lncRNA`鉴定。在区分从植物到哺乳动物的不同物种的lncRNA和蛋白编码RNA方面，LGC鉴定的准确率高达**90%**。

LGC基于物种特异性模型和人类模型性能研究

![](http://www.ehbio.com/ehbio_resource/LGC_specific.png)

LGC与现有常见lncRNA鉴定工具准确性敏感性特异性评估

![](http://www.ehbio.com/ehbio_resource/LGC_sensitivity.png)


LGC提供了在线服务器版和Linix/Unix本地版 (*如果您也开发了软件，希望同时做个线上版，欢迎联系我们开发，专业服务，质优价廉，也投个核酸研究*)

## Webserver 
	
(http://bigd.big.ac.cn/lgc/calculator)

![](http://www.ehbio.com/ehbio_resource/LGC_online1.png)

漂亮简洁的应用页面，只需要`fasta`（无参有参数据都可用）序列就可以进行`lncRNA`鉴定（可以直接粘贴自己感兴趣的序列或上传fasta文件（文件小于100MB）进行批量鉴定）。另外对人类，果蝇，小鼠，斑马鱼四个物种可以通过上传BED（小于3MB）或GTF(小于3MB)格式文件进行lncRNA挖掘。[生信分析过程中这些常见文件的格式以及查看方式你都知道吗？](https://mp.weixin.qq.com/s/ziVuUJ_y9drKJN12WXnPfg)
                     
![有参鉴定界面](http://www.ehbio.com/ehbio_resource/LGC_online2.png)

![Webserver运行](http://www.ehbio.com/ehbio_resource/LGC_online4.png)


![获取序列分析结果表，并下载](http://www.ehbio.com/ehbio_resource/LGC_online5.png)
 
## 本地运行

当然，网页版在速度与通量上仍有一定的局限性（对原始fasta数据库的拆分，再逐批上传鉴定真的好麻烦）。如果分析的数据比较多，可以在`linux`服务器搭建本地版本进行全库的LncRNA检索。 （不熟悉Linux，来看看[免费Linux系统和生信宝典原创学习教程](https://mp.weixin.qq.com/s/rXjQfyEX2FnuW9HTM_Uc8Q)）

在构建本地版的LGC时，LGC官网推荐的安装流程是先安装`python2`和`biopython`，但我个人习惯使用`anaconda2`以及其下的`bioconda`（[解决生物软件安装烦恼](https://mp.weixin.qq.com/s/VeexRyguwozqrMaOeeMF7Q)），可以大大简化安装过程和更好的解决依赖性问题（conda install 想补什么补什么，[Linux - Conda软件安装方法](http://mp.weixin.qq.com/s/A4_j8ZbyprMr1TT_wgisQQ)）。

命令如下

```
wget http://bigd.big.ac.cn/biocode/tools/4/releases/1.0/file/download?filename=lgc-1.0.tar.gz
tar zxf lgc-1.0.tar.gz
chmod 755 lgc-1.0.py
#确保conda，lgc-1.0.py在环境变量里
lgc-1.0.py input.fasta output.txt 
# Or
python lgc-1.0.py input.fasta output.txt
```

![运行程序](http://www.ehbio.com/ehbio_resource/LGC_commang1.png)

![结果文件](http://www.ehbio.com/ehbio_resource/LGC_commang2.png)

结果文件各列的意义

|Sequence Name|序列名称|
|ORF Length	|开放阅读框长度|
|GC Content	|GC含量|
|Conding Potential Score	|编码潜在评分：编码转录物的潜在评分，如果大于0，则为蛋白质编码RNA;如果小于0，则为ncRNA。“0”表示mRNA与lncRNA概率相同|
|Coding Label	|编码类别|
|pc	|编码序列的概率|
|pnc	|非编码序列的概率|
|fc	|编码序列的终止密码子概率|
|fnc	|非编码序列的终止密码子概率|

这样，我们就可以通过设置合理的筛选条件，来筛得感兴趣的lncRNA进行后续的研究，比如：

* [DESeq2差异基因分析和批次效应移除](https://mp.weixin.qq.com/s/Vmhx_TGxNkQzkekf93Xl4w)
* [WGCNA分析，简单全面的最新教程](https://mp.weixin.qq.com/s/PMb2xwADvnMwaipyFXdtzQ)
* [基因共表达聚类分析和可视化](http://mp.weixin.qq.com/s/ST2SAmfKOptpJOHS8podmQ)
* [GO、GSEA富集分析一网打进](http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg)
* [GSEA富集分析 - 界面操作](http://mp.weixin.qq.com/s/3Nd3urhfRGkw-F0LGZrlZQ)
* [无需写代码的高颜值富集分析神器](https://mp.weixin.qq.com/s/GidnT_ivj3o3asn3327JpQ)
* [去东方，最好用的在线GO富集分析工具](https://mp.weixin.qq.com/s/l6j2encDfEQkt2UeNCMFhg)

参考资料：
Wang G, Yin H, Li B, et al. Characterization and identification of long non-coding RNAs based on feature relationship[J]. bioRxiv, 2018: 327882.
生信宝典: [Nature Method：Bioconda解决生物软件安装的烦恼](
https://mp.weixin.qq.com/s/VeexRyguwozqrMaOeeMF7)
生信宝典[Linux学习-环境变量和可执行属性](
https://mp.weixin.qq.com/s/poFpNHQgHDr0qr2wqfVNdw?)



