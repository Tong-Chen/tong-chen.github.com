---
title: 生信宝典之傻瓜式(四)文献挖掘查找指定基因调控网络
author: ct
layout: post
categories:
  - Bioinfo
tags:
  - Bioinfo
---

傻瓜系列重启了，[如何快速查找指定基因的调控网络](http://mp.weixin.qq.com/s/LPWaxbKuS-XlvzkSE-MupQ)介绍了使用在线查询数据库 (http://evexdb.org/)对PubMed和PubMed Central中发表文章的摘要和全文为依据进行文本挖掘探寻基因直接可能的相互作用的工具。反响很好，但现在网站似乎出了点问题，获得的相互作用细节信息不能展开了(推测可能是使用的JS库无法加载)。有朋友留言推荐 **[Cytoscape literature search](http://apps.cytoscape.org/apps/agilentliteraturesearch#cy-app-releases-tab)**，一个存在历史挺久的Cytoscape插件，通过给定关键字搜索文献，并且基于搜索结果构建互作网络，帮助研究者快速搜索和提取基因之间，蛋白之间可能的联系，兼容2.7和3.1版本，下载**32,742**次。

作为Cytoscape的插件，安装很方便，基本的Cytoscape使用见[Cytoscape之操作界面介绍](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484184&amp;idx=1&amp;sn=2384ba8a6a6ea3ed7dac1b42217c710a&amp;chksm=ec0dc692db7a4f84a03feb4de092aa0712b1bca2975f1cee8fac8342d0a65f836f5f94e9d877#rd)和[新出炉的Cytoscape视频教程](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484194&amp;idx=1&amp;sn=61bcbe1c48e195c5c830396865789723&amp;chksm=ec0dc6a8db7a4fbeaa9cdd7245127edd382f3e4d13a61636c2cbc52062b32d7565bf282fca5e#rd)。前段时间[R, Cytoscape, AI](http://mp.weixin.qq.com/s/C4EBufEtFF6bhBKrH8NXng)的培训班也涉及了更多的Cytoscape的使用。

安装完之后，从菜单栏`Apps`-`Agilent Literature Search`启动，使用界面如下。

左侧一般输入一个或多个基因 (若输入多个则每一行输入一个)，右边限制一个环境，可以是物种，也可以是某种疾病如`lung cancer`，或某个过程`stem cell`。下面的选项还可以选择是否使用**别名** (选择后我们输入的`pou5f1`就被转成了`oct4`, `otf4`等)，限定**物种**，限定相互作用的判断 (个人一般使用**relaxed**)。具体每个参数的含义详见后面解释。

前面输入的内容都会在`Query Editor`中转换为逻辑查询表达式的形式，方便查看搜索的内容是否符合自己的需要，也可以自行修改，比如我们把`stem cell`改为`AND`连接。

![](http://www.ehbio.com/ehbio_resource/cyto_agilent_query.png)

点击`蓝色箭头`就可以启动搜索。搜索到的文献展示在左下角，可点击跳转到PubMed，右键删除某一项。

右侧展示的是挖掘出的调控网络，可以根据属性进行一些修饰、美化和查询。

![](http://www.ehbio.com/ehbio_resource/cyto_agilent_result.png)

### 网络查看和美化

首先是调大字体 (`Label Font Size`)，设置搜索出的基因和挖掘出的相互作用基因不同的颜色 (`Fill Color-searchTerm-Discrete Mapping`), 删掉与核心基因没有连线的点，**Apply preferred layout**重新调整布局 (工具栏上的刷新按钮)。

如果觉得线太过扭曲，可以`Layout-Clear all edge bends`，然后再点击`Layout-Bundle edges`使连接看上去圆润。初步修饰下，效果如下：

![](http://www.ehbio.com/ehbio_resource/cyto_agilent_network.png)

如果常用，每次调样式也比较麻烦，可以把样式保存起来，点击样式旁的**三道杠**，选择`Copy style`重新命令 (若不导出，关闭后就不见了)，然后`File-Export`导出。下次查询好之后，再`File-Import`导入就好。也可后台回复 **style**，获取我们这个简单的样式，以此为基础修改。

每个节点，点击**右键**，按下图点选菜单，可以看到支持其相互作用的**文章句子节选**，方便快速阅读和理解潜在的调控关系。

![](http://www.ehbio.com/ehbio_resource/cyto_agilent_evidence.png)

更多Cytoscape的使用见之前的[新出炉的Cytoscape视频教程](http://mp.weixin.qq.com/s/sKEy_Pn9qnWw4W-aXraA5g)。在[R, Cytoscape, AI](http://mp.weixin.qq.com/s/1nf7vwyvC3oemkTq_pu87A)的培训中也有我们的主讲老师讲的更多的Cytoscape的使用。(后台回复 培训 ，跳转到培训网站查看视频)

### 选项解释

**寻求帮助**

在上述查询界面，按`F1`或点`Help`可以打开帮助页面如下。当前截图显示的是通过**View**菜单选择搜索的数据库，现在只有`PubMed`和`USPTO` (美国商标专利数据库)可选。

![](http://www.ehbio.com/ehbio_resource/cyto_agilent_help.png)

**Max Engine Matches**: 限制每个字符串在每个库最大查询到的结果数目。

**Use Aliases**: 选定后，将会根据`Concept Lexicon`中限定的物种寻找左侧输入框输入的内容的别名。查询时，有一个别名匹配上就可以。

**Use context**: 是否使用Context面板 (右侧输入框)限定查询。

**Concept Lexicon Limits Search**: 如果需要把搜索结果限制在某个物种，则勾选。

**Concept Lexicon**: 通常是物种相关的选项，对`Use aliases`的判断和搜索结果提取有效，但不用于限制查询结果。所以如果要在查询时就限制物种，则需要再右侧输入框输入物种的名字，会加快查询速度。

**Interaction Lexicon**: 限制判断相互作用的严格程度。对于每个包含搜索关键字的句子，都会来判断里面是都包含`interaction lexicon`收录的动词，如`activate`, `enhance`, `cause`等。这些关键词可以修改，有严格版和宽松版。

**Load and Save**: 搜索结果可以存储和再次导入。

### 选项进一步解释和自定义

如果Windows下，LiteratureSearch的配置文件在目录**C:\Users\sxbd\CytoscapeConfiguration\app-data\com.agilent.labs.als.AgilentLiteratureSearch-3.1.1\data**下。(把`sxbd`改为您的用户名)

**Interaction Lexicon**：前面提到的`limit`, `relax`, `empty`每一个的效果都记录在文件`interaction-lexicon-map.txt`中，文件内容如下

```
limited	data/strictVerbNames.txt
relaxed	data/verbNames.txt
empty	data/emptyVerbNames.txt
```

每个不同的参数表示使用的关键词列表不同，`empty`表示不进行限定，只要两个词出现在一个句子中就认为有作用。

`strict`表示严格限定，默认要求句子中必须含有收录的**15**个单词中的一个才认为存在相互作用 (在文件`strictVerbNames.txt`)。

`relaxed`默认要求句子中必须含有收录的**75**个单词中的一个才认为存在相互作用，涉及促进、抑制、结合、催化等对应的英文单词和变种，在使用过程中，我们也可以不断完善、添加更多词汇到`verbNames.txt`中，以获得更多关注的相互作用。

**Concept Lexicon**

这个由文件`concept-lexicon-map.txt`控制，默认收录了常见物种的KEGG注释信息、基因的别名信息。

```
Arabidopsis thaliana	data/.uc_Arabidopsis_thaliana	
Bos taurus	data/.uc_Bos_taurus
Caenorhabditis elegans	data/.uc_Caenorhabditis_elegans
Danio rerio	data/.uc_Danio_rerio
Drosophila melanogaster	data/.uc_Drosophila_melanogaster
Escherichia coli	data/.uc_Escherichia_coli
Homo sapiens	data/.uc_Homo_sapiens
Mus musculus	data/.uc_Mus_musculus
Rattus norvegicus	data/.uc_Rattus_norvegicus
Saccharomyces cerevisiae	data/.uc_Saccharomyces_cerevisiae
```

以人的数据为例，前面是KEGG编号、对应的描述，后面是基因的每个名字一行，方便使用别名搜索。

```
6.3.5.8	aminodeoxychorismate synthase	adc synthase	4-amino-4-deoxychorismate synthase	pabb
6.3.5.9	hydrogenobyrinic acid a, c-diamide synthase (glutamine-hydrolysing)	cobb
dynamin	dynamin-1	dynamin1
dynamin-2	dynamin2
epsin	epsin1	epsin-1
nf-kappaB	nfkappaB	nfkb1	nfkb	nf-kappa B	nfkappa B
frizzled	fz	fzd	fzd7
dsh	disheveled	dishevelled	dsh1	dvl1l1	dvl1
bcatenin	beta-catenin	beta catenin))
```

之前[如何快速查找指定基因的调控网络](http://mp.weixin.qq.com/s/LPWaxbKuS-XlvzkSE-MupQ)文章下有朋友留言，非模式生物怎么查找，一个是利用[生信宝典之傻瓜式(四)蛋白蛋白互作网络在线搜索](http://mp.weixin.qq.com/s/JO1J66BtzuY-9a20x0XQcg)中提到的在线工具**STRING**收录了**2031**物种。另外一个就是在这自定义需要的文件，使用此插件搜索。



