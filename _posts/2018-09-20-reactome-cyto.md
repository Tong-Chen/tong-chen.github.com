---
title: 没钱买KEGG怎么办？REACTOME开源通路更强大
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

之前搜集[免费生物AI插图](https://mp.weixin.qq.com/s/bNrWaK-Rd7I7M0In07_XWg)时简单提到了通路数据库Reactome（https://reactome.org/）， 那些精美的生物插图只能算是该数据库附赠的小礼品，他的**主要功能还是作为一个开源的通路数据库，为相关领域的研究者提供直观的可视化生物信息学工具**。在一定程度上，可以替代收费的KEGG数据库，而且拓展出很多新的通路。

目前该库覆盖了**19个物种**的通路研究，包括经典的代谢通路、信号转导、基因转录调控、细胞凋亡与疾病。数据库引用了100多个不同的在线生物信息学资源库，包括[NCBI](https://mp.weixin.qq.com/s/4a5U8GdBoNFXkykL6m2EeA)、[Ensembl](https://mp.weixin.qq.com/s/2OoXy4f1t0hE8OUqsAt1kw)、UniProt、[UCSC基因组浏览器](https://mp.weixin.qq.com/s/we3raL4XowZp4vQ9zPqfYQ)、ChEBI小分子数据库和[PubMed文献数据库](https://mp.weixin.qq.com/s/v45sZXXCMNZGzzHE1gd-gw)等。（具体见下图和表）

![img](http://www.ehbio.com/ehbio_resource/Reactome_stats.png)

SPECIES | PROTEINS | COMPLEXES | REACTIONS | 	PATHWAYS
---|---|---|---|-
D. discoideum	| 2174 | 1932 |	1766 | 848
P. falciparum	| 772 |	731	| 613	| 470
S. pombe	| 1465	| 1473	| 1230	| 673
S. cerevisiae	| 1652	| 2160	| 1878	| 834
C. elegans	| 5088	| 3360	| 2829	| 1137
S. scrofa	| 18418	| 8405	| 7335	| 1602
B. taurus	| 9905	| 8492	| 7363	| 1606
C. familiaris	| 11153	| 8225	| 7093	| 1599
M. musculus	| 12769	| 9560	| 8331	| 1620
R. norvegicus	| 11754	| 8682	| 7498	| 1606
*H. sapiens	| 10763	| 11674	| 11896	| 2222
G. gallus	| 12305	| 7462	| 6420	| 1631
T. guttata	| 7394	| 6350	| 5354	| 1500
X. tropicalis	| 9363	| 7434	| 6390	| 1562
D. rerio	| 14261	| 7362	| 6286	| 1561
D. melanogaster	| 9959	| 4806	| 4023	| 1391
A. thaliana	| 6522	| 1901	| 1729	| 790
O. sativa	| 13433	| 1835	| 1677	| 786
M. tuberculosis	| 13	| 47	| 39	| 12

## Pathway Browser


现在就来体验一下！在首页点击**Pathway Browser**进行通路检索。

![img](http://www.ehbio.com/ehbio_resource/reactome/Reactome_Browser.png)

### 界面介绍

* **标记1处**选择物种；

* **标记2处**可以按照不同的生物功能来检索自己所需要的通路；

* **标记3处**的大框是不同的生物反应按照模块划分组成的多个烟花状的有向无环图；

1 ）在此方框中，结合*滚轮*可以放大缩小通路图；

2） 也可以通过右下角的操作按钮来放大缩小通路图，通过方向按钮调节整个画面；

3）右上角可将当前画面下载成*PNG*或者*PPTX*([你和PPT高手之间，就只差一个iSlide](http://mp.weixin.qq.com/s/gKPs7k5JqFBlYJPv7h_-hA))的格式；

4） 网页右侧还有半隐藏的一个工具，鼠标放上会弹出，在这里可以*修改通路图的背景色*等；

* **标记4处**是对当前所选通路的描述、参与该通路的所有分子、通路中相关基因的表达等；

![img](http://www.ehbio.com/ehbio_resource/skills20.png)

1\. 可以通过特定关键词（比如基因、小分子、代谢产物）检索相关通路，这里以**Developmental Biology**为例，直接在左侧点击即可。

   Pathway通路都是一层层往下递进的，最高层的通路含有太多路径，无法单个详细显示。从而该数据库以形象生动的图形化方式将**Developmental Biology**通路下9个子通路简洁地展现出来。
 ![img](http://www.ehbio.com/ehbio_resource/reactome/Reactome1.png)

   刚刚所说的标记3的展示框中，点击左上角第三个图标可以切换**pathway overview**和**open pathway diagram**两种视图效果。点击一下，便可以切换到烟花状的有向无循环图形式。

2\. 根据自己的研究选择感兴趣的通路，在此我们以**HOX基因**在后脑发育的早期胚胎发生过程中的激活为例。

![img](http://www.ehbio.com/ehbio_resource/reactome/Reactome3.png)

3\. 在**Activation of anterior HOX genes in hindbrain developmentduring early embryogenesis**通路中有许多关键的反应，点击一个感兴趣的，视图界面跳转至对应的通路图。

![img](http://www.ehbio.com/ehbio_resource/reactome/result2.png)
![img](http://www.ehbio.com/ehbio_resource/reactome/result1.png)

## Details Panel

1\. Discrimination

此部分是对选定通路的概述、研究进展和重要发现，参考资料和作者信息等。

![img](http://www.ehbio.com/ehbio_resource/reactome/description.png)

2\. Molecules

展示了通路中包含的所有分子，包括**化学成分、蛋白、基因**。点击右侧`+`，将详细条目展示出来，点击`蓝色编号`将跳转至相应的其它数据库。点击`Download`可将数据下载下来。
![img](http://www.ehbio.com/ehbio_resource/reactome/molecules2.png)

3\. Structures

   对于一个反应，此处展示的结构图来自Rhea数据库；对于简单的分子，展示的结构图来自ChEBI；而若是一个含蛋白质的通路，则显示来自PDBe的蛋白3D结构。

![img](http://www.ehbio.com/ehbio_resource/reactome/structure.png)

4\. Expression

   此部分展示参与上面所选通路的所有基因表达情况，表达数据来自**基因表达图谱**。可点击`download`下载基因表达数据以进行后续的个性化分析。
![img](http://www.ehbio.com/ehbio_resource/reactome/Reactome7.png)


## Analyze Data

该数据库除了可以检索通路外，在首页点击**Analyze Data**，还可进行基因分析。

该工具**支持两种类型的分析**，第一种是分析一系列基因涉及到哪些具体的通路，另外一种是对比物种间的通路差异。**两种分析显示的方式相同，都通过对通路标黄来显示（颜色可自行调整）**。这里我们利用数据库中提供的数据查看了某一些基因的通路，结果如图所示。

![img](http://www.ehbio.com/ehbio_resource/skills24.png)

![img](http://www.ehbio.com/ehbio_resource/skills25.png)

## Cytoscape里reactomeFIPlugIn 插件使用

Cytoscape是一个功能强大的网络互作分析工具，之前有介绍。在腾讯课堂 （https://bioinfo.ke.qq.com）有免费视频可看。

* [Cytoscape教程1](http://mp.weixin.qq.com/s/m9uJm8GwSXb3xaRxtod08Q)
* [Cytoscape之操作界面介绍](http://mp.weixin.qq.com/s/ZSoW7-qWs3BuSB7bkDnfmA)
* [新出炉的Cytoscape视频教程](http://mp.weixin.qq.com/s/sKEy_Pn9qnWw4W-aXraA5g)

在Apps里有众多的插件工具用来实现不同的分析功能，同时还能**与很多数据库关联**，直接在电脑本地调用数据库中的数据进行网络分析，可以说是非常的方便啦！

下面介绍的**reactomeFIPlugIn**插件便可以实现利用cytoscape在本地调用reactome数据库中的数据，让用户轻松在软件中进行各种分析。

1\. 首先按照下图所示步骤选择`Apps`下的`App Manager`，在Search框中输入插件名，点击`Install`安装`reactomeFIPlugIn`

![img](http://www.ehbio.com/ehbio_resource/reactome/cyto_reactome_install.png)

2\. 安装好的插件将保存在Apps下，在工具栏依次点击`Apps/Reactome FI/Reactome Pathways`，cytoscape将通过网络加载Reactome数据库中的通路信息（<https://reactome.org/PathwayBrowser/>），加载完成后各通路将显示在左侧`Control Panel`处。

![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_0.png)

![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_1.png)

3\. 选择感兴趣的Pathway，点击鼠标右键，在弹出菜单中选择`View Reactome Source`，可以查看该通路在Reactome中的详情注释；或者选择`View in Reactome`将跳转至Reactome网页查看详情。


![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_2.png)
![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_3.png)


4\. 在上述右键弹出菜单中选择`Search`，输入想查找的Pathway，查找到的Pathway将以**蓝色背景凸显**。

![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_4.png)
![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_5.png)

5\. 在鼠标右键弹出的菜单栏中选择`View in Diagram`或`Show Diagram`

**Show Diagram**：如果选定的路径有自己的路径图，可以在弹出菜单中选择`Show Diagram`，将其路径图显示在Cytoscape中央。

**View in Diagram**：如果选定的路径布局为较大的路径中的子路径，则可以在弹出菜单中选择`View in Diagram`查看通路图。打开图表后，所选路径包含的反应将以**蓝色突出**显示。
![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_6.png)

6\. 在Cytoscape中央通路图的空白区域点击鼠标右键，选择弹出菜单中的`Convert to FI Network`，可以将通路图转换成功能互作网络图，原始的通路图将在cytoscape的左下角显示。

![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_7.png)
![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_8.png)

7\. 鼠标右键在跳出的菜单栏中选择`Analyze Pathway Enrichment`可进行Pathway富集分析，此时会弹出一个框，要求选择上传一个基因集文件。该文件可以是一下三种格式中的任一一种：1）每行一个基因；2）所有基因以逗号分隔放在一行；3）所有基因以制表符分隔放置在一行。


1）基因富集的通路**根据FDR值以不同的颜色背景凸显**；

2）基因富集的通路信息在Table Panel中展示；

3）使用`View in Diagram`或`Show Diagram`在通路图查看命中的pathway，并可以在通路图结果展示面板中点击鼠标右键后，选择`Export Annotations`将当前通路图保存下来。
![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_9.png)

![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_11.png)

![img](http://www.ehbio.com/ehbio_resource/reactome/CytoReactomeFI_10.png)

后面的皆可以参考<https://bioinfo.ke.qq.com>免费视频中Cytoscape的使用来把基因表达信息或修饰信息映射到网络图进行更多展示了。

* [GO、GSEA富集分析一网打进](http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg)
* [GSEA富集分析 - 界面操作](http://mp.weixin.qq.com/s/3Nd3urhfRGkw-F0LGZrlZQ)
* [Bedtools使用简介](https://mp.weixin.qq.com/s/bIXom5bSDov-4sPqsTRc6A)
* [OrthoMCL鉴定物种同源基因 （安装+使用）](https://mp.weixin.qq.com/s/lC1KiRygr5RefMZLVPREdQ)
* [Rfam 12.0+本地使用 （最新版教程）](http://mp.weixin.qq.com/s/5OIRHA22ZLr5Z8bEhDiBqg)
* [轻松绘制各种Venn图](http://mp.weixin.qq.com/s/zn654JqG9OeO71rJUTDr2Q)
* [ETE构建、绘制进化树](http://mp.weixin.qq.com/s/DD1nZnx5mYxWGrohNgdPvQ)
* [psRobot：植物小RNA分析系统](http://mp.weixin.qq.com/s/kWkEQOX-6SKMAUQmAuc86w)
* [生信软件系列 - NCBI使用](http://mp.weixin.qq.com/s/4a5U8GdBoNFXkykL6m2EeA)
* [去东方，最好用的在线GO富集分析工具](https://mp.weixin.qq.com/s/l6j2encDfEQkt2UeNCMFhg)
* [2018 升级版Motif数据库Jaspar](https://mp.weixin.qq.com/s/S1SlhNfPvcXOwRQZvrm6GQ)
* [一文教会你查找基因的启动子、UTR、TSS等区域以及预测转录因子结合位点](https://mp.weixin.qq.com/s/vFO7uAtI6nh-zTW7RHCixA)
* [拿到基因两眼一抹黑？没关系，先做个基因富集分析吧！](https://mp.weixin.qq.com/s/pzcZacJkeM-71-FPJwJL2g)
* [科研小萌新，掌握这些技巧，轻松玩转各个基因！](https://mp.weixin.qq.com/s/_ZkOaUwE1AjBjghuNbAH8A)
* [引起相变的无序结构域（IDRs）怎么预测？跟踪热点，提升文章档次！](https://mp.weixin.qq.com/s/amI-66u9DnIZITKHgO0UgQ)
* [如果你经常用PubMed，那么这个插件将非常好用！](https://mp.weixin.qq.com/s/v45sZXXCMNZGzzHE1gd-gw)
