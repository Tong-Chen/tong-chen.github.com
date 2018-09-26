---
title: Nature综述|整合组学分析护航健康，推动精准医学时代的到来！
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

![](http://www.ehbio.com/ehbio_resource/omics_nature.png)

**导读**

Konrad J. Karczewski, and Michael P. Snyder撰写的关于整合多组学在疾病研究中的应用一文《Integrative omics for health and disease》，于2018年2月26日发表在nature reviews genetics (Nature系列综述, 2018 IF: 41.465）。  

对于发病原因复杂的疾病通常很难用单一的理论模式进行全面表述，多组学技术通过整合生物系统中诸多相互联系和作用的组分来研究复杂生物过程的机制，从而为更加准确地对疾病进行阐述提供了可能性。同时作者也阐述了多组学技术在临床应用中存在的问题和挑战，并且整合组学正推动着真正的精准医学时代的来临。

>**摘要**
>
>多种组学技术（如基因组、转录组、蛋白质组和代谢组）的进步已在极其详尽的分子水平促使个体化医疗成为可能。尽管每个单独的组学技术都促进了医学的进步并已进入临床实践，然而单个技术难以捕捉大多数人类疾病的整体复杂性。整合多组学技术正成为综合研究生物和疾病的新方法。本文讨论了多组学数据的整合，以及将其应用于人类健康和疾病研究的可能性。我们提供了一些多组学数据整合的例子，用以理解、诊断并监测相应疾病的治疗，包括罕见病、常见病以及癌症和移植生物学。最后我们讨论了多组学技术在临床应用上面临的技术和其它方面的挑战。

  

[生信老司机以中心法则为主线讲解组学技术的应用和生信分析心得](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485782&idx=1&sn=f9b05d0a6b22861a871e062688942b66&scene=21#wechat_redirect)

  
>**名词解释**
>   
>**1\. 可操作性 (Actionability)：** 基础研究的突破能用于改善某种疾病治疗的医学实践。  
**2\. 孟德尔遗传病 (Mendelian diseases)：** 由遵循孟德尔遗传规律（如显性或者隐性）的单个位点或基因引起的疾病。  
**3\. 遗传病因学 (Genetic aetiology)：** 研究引起特定疾病的遗传因素的学科。  
**4\. 表达数量性状位点 (Expression quantitative trait loci (eQTLs))：** 诱发基因表达显著变化的遗传变异。  
**5\. 遗传力 (Heritability)：** 性状的表型变化可归因于加性遗传变异的比例。  
**6\. DNA酶超敏感性 (DNase hypersensitivity)：** 根据染色质被DNA酶I切割的敏感性来度量染色质的开放程度。  
**7\. 结构变异 (Structural variants)：** 1 Kb或者更长区域的一类遗传变异，包括拷贝数重复、插入、缺失以及易位和倒位。  
>**8\. 纵向数据 (Longitudinal data)：** 在一段时间内，从较大的群体中对同一受试者的重复观测结果的集合。

高通量测序及其它大规模并行分析技术（如质谱）成本的快速下降使他们能够广泛应用于临床研究与实践。外显子组和基因组测序技术已被用于疾病的辅助诊断（尤其是罕见病的诊断）、指导癌症的治疗和预后以及建立健康个体的疾病预测模型等。很多科研人员和公司正在致力于开发全基因组范围内的遗传、基因表达和其它组学数据（如微生物组，BOX 1）做为疾病诊断的标记物（详细见TABLE 1）。例如全基因组关联分析（GWAS）已经成功地鉴定出了疾病的风险位点。然而多数情况下，一些疾病相关的驱动变异或驱动基因仍未被鉴定出来。在此情况下，其它组学技术可以在精准病理生理学上对这些疾病提供有效检测。有些组学技术如蛋白质组学可以产生更接近于生物表型的数据，但由于昂贵且不够深入全面，在用于查明病因上仍有很多挑战。因此，几乎没有一种单独的技术能够解释导致人类疾病的分子事件的复杂性。[测序发展史：150年的风雨历程](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485298&idx=1&sn=36c8024abb89fd5f408578af06ef4313&chksm=ec0dc2f8db7a4beed246fffa24f0882bdfb02fa1b0b496a5701f65f799e603e8c09a1ddd8ff2&scene=21#wechat_redirect)

>**Box 1**
>
>**方框1.** **在多组学技术中引入微生物组**
微生物组与许多人类常见疾病有关，但由于不确定其是因是果，使得问题变得更加复杂。基因组数据中，致病性关系简单明确，通常是DNA影响表型（除了癌症导致的突变发生外）。但解密微生物组成与疾病的因果关系却比较困难这些研究需要昂贵的纵向或介入性实验，并且小鼠模型无法全面模拟人体生物学。尽管如此，患有诸如炎症性肠病、II型糖尿病和肥胖症等疾病的患者确实具有与健康人群显著不同的微生物组成。此外，微生物组对免疫功能有强烈影响，在动物模型中被认为是疾病发生的潜在因素。

  

随着对微生物组理解的深入，综合分析该组学及其它组学技术可以加深对人类疾病的理解。最近研究显示，人类基因序列影响整个肠道微生物群的组成，为某些疾病的相关遗传位点提出新的致病解释。此外，人类遗传物质和微生物组之间的互作会影响疾病，同时整合这两种图谱的研究会很有价值。宿主与其微生物组之间的代谢信号互作已成为一个热门的研究领域，越来越多的证据表明来自肠道细菌的代谢物可能在人类疾病中起作用。因此，综合分析基因组、代谢组、微生物组及其它组学可能有助于健康管理和疾病诊治。

<center>表1： 整合组学的数据类型  </center>

![](http://www.ehbio.com/ehbio_resource/omics_table.png)

CPTAC, Clinical Proteomic TumourAnalysis Consortium; EDRN, Early Detection Research Network; ENCODE,Encyclopedia of DNA Elements; GEUVADIS, Genetic European Variation in Healthand Disease; gnomAD, Genome Aggregation Database; GTEx, Genotype–TissueExpression; GWAS, genome-wide association study.

理想情况下，不同的组学技术可以结合起来，用以辅助疾病诊断并全面了解人类的表型和疾病。然而多组学数据的分析引入了新的信息和解读上的挑战。尤其需要新颖的分析和统计方法来将不同类型的数据集整合和质量控制指标的标准化。此外该领域必须重视分子事件的解读、基础发现的可操作性以及是否可以用于指导治疗和临床护理。

下面将介绍整合组学如何通过帮助健康管理及疾病的诊断治疗来影响医学。我们讨论了罕见的孟德尔遗传病如肌营养不良症和更为常见的疾病如自闭症和阿尔茨海默病的临床前和临床应用。此外，我们还研究了多层次组学技术在癌症诊断和治疗中的应用。我们始终都在讨论综合多个数据集的优势，例如多种技术优势互补，有助于深入了解疾病的机制。此外，还讨论了目前的技术方法和将多个来源的数据进行最优组合和解读的挑战，以及将其成功应用于阐明人类疾病机制的一些令人鼓舞的例子。

  

## **_1._ Dissecting Mendelian disease**

## **解析孟德尔遗传病**

在北美，大约10％的住院儿童和20％的婴儿的死亡可归因于孟德尔遗传病。多数情况下，临床医生和病人家属会借助外显子组及基因组测序技术找到孟德尔遗传病的相关致病突变。但是由于疾病类型和实验设计等因素，这一新技术在靶向测序未能找到致病机理的病例中只有25-50%获得了成功。对于主要由隐性变异导致的疾病，只有当此致病变异已被收录在疾病变异数据库（如Clinvar）中或者在一个已知疾病基因上发生了蛋白质截断变异（如提前终止，移码或关键剪接位点变异）时，这种检测技术才最为有效。然而，有时变异的影响可能比较微弱（例如可诱发新的隐性剪接位点的内含子变异），或由于体细胞嵌合导致突变难以被检测到，或多个候选变异都可能是驱动变异，这些都会使导致疾病发生的真正变异变得难以被检测到。此外，不了解遗传病因或对候选变异基因研究较少时，这种诊断会格外复杂。综合其它信息如RNA测序（RNA-seq）或网络分析，有利于检测可能的驱动变异中更重要的分子事件，或提供更多的证据来表明某个候选突变是导致疾病发生的原因。例如在对非典型范可尼贫血症的患者进行多组学分析时，DNA测序和基因组杂交微阵列芯片（aCGH）在识别最终被鉴定为驱动突变的位点是有效的，而RNA-seq可为一些最初不认为有致病性的变异提供致病证据，包括影响剪接模式的内含子变异和同义突变，以及导致转录本被削弱表达的非编码外显子及其上游区域的缺失。

最近，对大约50名患者的两项系统性研究均使用了RNA-seq和其它技术（图1），使得诊断率提高了约10％到35％。其中一项研究表明，全外显子组测序（whole-exome sequencing, WES）并没有为被诊断为肌营养不良症的（muscular dystrophy, MD）患者找到驱动变异，但RNA-seq数据却鉴定出导致剪接异常的隐性剪接突变事件。特别的，即使对这些患者进行了全基因组测序（WGS）鉴定出这些变异，但由于它们多位于内含子区域或被预测为不会影响剪接，也可能不会被视为可诱发疾病的变异。由于测序成本快速降低以及可获得的信息量增加，RNA-seq可能会成为在临床实践中鉴定疾病病理与生理学的有力工具。同样地，随着蛋白质组学技术的成本越来越低和更容易获取，使其可用于鉴定诸如通过影响蛋白质稳定性或翻译后修饰的错义突变而引起的蛋白水平变化。[蛋白质组学研究概述](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485530&idx=1&sn=1b11166354d38dc7999bcfff3d0cf7bc&scene=21#wechat_redirect)

![](http://www.ehbio.com/ehbio_resource/omics_finger1.png)

**图1** 鉴定可用于诊断罕见病的驱动变异。在Kremer和Cummings等人的工作中，采用了多组学方法助力于诊断尚未诊断的疾病。尽管现在外显子组和基因组测序能够在20%至50%的案例中有效地识别驱动变异（取决于不同的遗传和表型），但单一组学技术并不能诊断大多数的病例。（a,b）用来自患者组织的RNA-seq数据可以进行分子诊断，鉴定出异常表达、剪切或者是具有等位基因特异性表达的基因，从而帮助揭示疾病进展的分子机制。（c）在某些情况下，功能验证如蛋白质组可以更进一步助力疾病诊断。（[生物AI插图素材获取和拼装指导](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485734&idx=1&sn=cfa1e683c67ca6fac92f3f1af3a49e85&chksm=ec0dccacdb7a45bab3c9ebcd39089e7be5772d34039fbf0674f1d16b02690410ac3b83c110b8&scene=21#wechat_redirect)，[高颜值可定制在线绘图工具-第三版](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485097&idx=1&sn=b25732da52e95ba99cdbf77e1dc45191&chksm=ec0dc323db7a4a35a0b4eac9c865b70ebc7ed37c53e4bbe41194e241aa37344ddf2935df8a74&scene=21#wechat_redirect)）  

  

## **_2._**  **Genetic architecture of common disease**

## **常见疾病的遗传结构**

很多常见病比如糖尿病、肥胖症、精神分裂症和自闭症等发病机制复杂，是多种遗传和环境因素共同作用的结果。目前已发现数千个基因组位点与人类疾病密切相关。然而一旦确立了这种相关性，难点则是在特定疾病的分子生理病理背景下研究该基因的特征以及与其影响的基因和通路。为此更多多组学数据集的分析方法被开发出来，其中包括网络分析和富集分析。[GO、GSEA富集分析一网打进](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484594&idx=1&sn=77c8a84ceaae6b672f198ebd531c21e4&scene=21#wechat_redirect)


**2.1 Network analyses** 

**网络分析**

多种正交类型数据的整合可用于缩小疾病相关基因的搜索范围并鉴定致病机制。特别是一些网络模型，包括蛋白质-蛋白质相互作用[生信宝典之傻瓜式(四)蛋白蛋白互作网络在线搜索](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484911&idx=1&sn=5c204e8265e1d2517068ff8381236a24&chksm=ec0dc065db7a4973e92b844b0dd9b44445646055d09d68df3b754ce1a454b5b02f73fb9178f4&scene=21#wechat_redirect)、调控和共表达网络，已被证明是鉴定疾病基因和通路的宝贵资源。这些网络可以与任何全基因组范围的数据集（包括单核苷酸多态性（SNP）或基因表达数据）相结合，用于考察在某项研究中与疾病显著相关基因网络的拓扑学性质，这对那些在全基因组统计分析不显著的基因更为适用 （因为可以考虑其加性效应，[GSEA富集分析 - 界面操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484582&idx=1&sn=1e01276e1216c91bd6e1e08db15bd905&chksm=ec0dc12cdb7a483a722d857327b2a49c701a439c92a3b61466d21e912c5e30c17f1fd7321c84&scene=21#wechat_redirect)）。对于遗传变异数据，挑战在于将SNP位点映射到受影响的基因：在某些情况下这种变异的作用比较明确，比如克罗恩氏病的免疫应答相关基因NOD2的移码突变，但更多的情况是变异影响的基因并不明确。此外，多个SNPs可以组团增强调控能力，这时就需要考虑连锁不平衡模式的影响。

尽管存在这些挑战，网络法已经成功地帮助理解了一些人类疾病。例如，在自闭症类群（ASD）患者中具有新的错义或无义突变的基因，往往富集于蛋白-蛋白相互作用网络中与其它基因（[为了速成生物学，一位程序员探索了"爆款"基因背后的秘密](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485036&idx=1&sn=5b12e9ed89bed48bfc5655f9d016cbcd&chksm=ec0dc3e6db7a4af0cc9994ad43b01c91cbfa377f8663782109466970152f3afe48608680aa95&scene=21#wechat_redirect)）尤其是先前认为参与ASD的基因有高度连结的基因中。这种方式提供了一种在候选疾病基因中进行优选的机制，要么是表示这些基因由于是网络的中枢基因而具有更重要的影响，或因为与已知的疾病基因有关而被推定为疾病相关基因。[生信宝典之傻瓜式 (四) 蛋白蛋白互作网络在线搜索](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484911&idx=1&sn=5c204e8265e1d2517068ff8381236a24&scene=21#wechat_redirect)

此外，我们实验室最近的两项工作将基因组学、RNA-seq和蛋白质组学数据整合在一起，鉴定出与自闭症有关的新基因和复合物，并对其功能特点进行了描述。特别是对蛋白-蛋白相互作用网络的分析揭示了一个模块（或称为互作基因群），此模块富集了已知的参与自闭症的基因，以及在自闭症病例中携带拷贝数突变和罕见突变的基因。该模块富集了参与突触传导的基因，并且RNA-seq数据显示其中一个子模块中的许多基因在ASD患者的胼胝体具有差异表达（[DESeq2差异基因分析和批次效应移除](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485368&idx=1&sn=12b20487e9014ce2e69f01d3efbc6ce8&chksm=ec0dc232db7a4b248530e117a86053a9149d9ede5258326e04a4ab375f6858853c2e4c06d07d&scene=21#wechat_redirect)），这为许多ASD患者相比于正常人有更小胼胝体的现象提供了一个假定的分子解释。同样，通过将自闭症患者的罕见变异比对到蛋白质复合体上揭示了参与自闭症的新蛋白质和复合体，包括组蛋白去乙酰化酶（HDAC）、染色质重塑复合体和其它蛋白质复合体。因此，全基因组测序数据和全外显子测序数据与蛋白质互作数据的整合可以为重要疾病（如包括自闭症、II型糖尿病和心脏病）提供新的机制解释。[来一场蛋白和小分子的风花雪月](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247483842&idx=1&sn=653e97fb32eaa73ce9f26b22306cc369&scene=21#wechat_redirect)

**2.2 Enrichment analyses**

**富集分析**

为了理解从DNA到生理机能的遗传信息流整体的调控机制，最近已经进行了许多大规模的富集分析。蛋白质的编码变异是许多生物性状的基础，比如来自GWAS的许多与性状相关的基因位点富集了蛋白质序列的中断变异（非同义变异）。然而只有一小部分的疾病属于这一类，因此将非编码调控注释信息与疾病相关的其它数据整合起来，对于鉴定疾病基因和查明病因非常有价值。特别是，用于测量基因表达（RNA-seq，[转录组分析工具哪家强？](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484106&idx=1&sn=687a0def51f6ea91a335754eb3dc9ca9&chksm=ec0dc740db7a4e564e5b1e93a36e5d9447581e262eec9c2983d1d4e76788d673c9c07dec8f8e&scene=21#wechat_redirect)）以及用于测量基因表达调控区活性的方法（如用于检测转录因子结合位点的染色质免疫沉淀测序（ChIP-seq）或用于检测染色质开放区域的DNA酶高敏感位点测序（DNase-seq）），在鉴定基因组调控的组织特异性研究上具有重要价值。因此，如果疾病相关变异富集在表达数量性状基因位点（eQTL）以及转录因子结合位点，那么许多疾病的病因可能是对应的调控机制异常。最近一项对108个精神分裂症相关位点的研究证实，其中20个位点的基因表达有变化，这可以至少部分解释他们之间的部分关联。[ChIP-seq基本分析流程](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485115&idx=1&sn=dca081a0f1e510670def90cdda7fc5ec&scene=21#wechat_redirect)

最近使用GWAS总结统计和功能注释数据的分区遗传法（partitioning heritability methods），阐明了编码区和调控区变异的相对贡献，结果表明许多常见性状的大部分遗传特征来源自于调控区的变异（DNA酶超敏感的开放染色质区域），以及许多细胞类型特异的增强子区域 （[从Richard Young教授的系列研究看超级增强子发现背后的故事 (附超级增强子鉴定代码)](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485257&idx=1&sn=02000c839eb023a9cb3c5ba07f7d0e4c&scene=21#wechat_redirect)）。

此外，这种富集信息可用于辨别驱动变异以及通过增加对每种性状特异性注释的权重来鉴定与疾病和性状有关的新基因。在撰写本文时，这些方法尚未进入临床实践，但在揭示许多常见疾病的病因方面具有非常重要的价值。

  

## **_3_** **Narrowing causal mechanisms in common disease**

## **聚焦常见疾病的驱动机制**

如前所述，GWAS已成功识别出与疾病在统计学上有相关性的基因位点，但却很少发现驱动变异。整合多种数据类型如功能注释数据，也可以加深对特定疾病相关变异潜在功能的理解。

**3.1 Indirect integration across individuals**

**个体间的间接整合**

目前，确定与某一性状相关的驱动变异的低成本方法是使用多个独立的数据集，从一组具有生物学证据的候选位点中确定疾病形成的机制。此过程可以从GWAS开始，然后对一组基因组范围的统计显著相关位点做后续的功能验证，具体的实验可能取决于所鉴定的基因位点的类型或疾病的遗传结构。对于编码变异，后续确定变异对蛋白质结构或功能影响的实验可以很好地解释疾病的起因。对于非编码区的变异，结果通常更难以解读，但最近的大规模表观遗传学研究如DNA元件百科全书计划（ENCODE）和表观基因组路线图项目（Roadmap Epigenomics projects），可以提示可能的调节机制以及后续实验需要关注的转录因子。例如，对系统性红斑狼疮（SLE）相关变异的详细研究表明，变异不仅影响核转录因子-κB（NF-κB）的结合，并且与肿瘤坏死因子-α诱导蛋白3（TNFAIP3）在mRNA和蛋白质水平上均相关。

Manolis Kellis和其同事最近两项综合多种数据类型的研究，极大地加深了对阿尔茨海默病和肥胖症分子病理学的理解。首先，该研究组结合基因表达和表观组学数据，发现在阿尔茨海默病小鼠模型中上调的基因具有免疫细胞增强子的特征。重要的是，虽然免疫系统基因与阿尔茨海默病之间的联系早已确立，但在此情形下多组学数据类型被证实可用于建立一个效应（所施加）的方向，即阿尔茨海默病人免疫系统基因的表达和调节活性均有协调性地增加。同样地，整合表观基因组和染色体构象数据，以及携带FTO肥胖等位基因的患者的基因表达信息和许多其它数据类型，为风险等位基因的机制提供了解释（图2）。使用CRISPR-Cas9（[CRISPR-CAS9发展历程小记](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484956&idx=1&sn=7de42d26a5c76edc07bcd9b76d05728c&chksm=ec0dc396db7a4a80068548ace16fa3b19b36621695dee3fb20a84395d211e867470cc26f1a31&scene=21#wechat_redirect)）对风险等位基因进行基因组编辑可以修复其异常表达和热量生成，这提供了一种对于肥胖症的潜在治疗方式。

![](http://www.ehbio.com/ehbio_resource/omics_finger2.png)

**图2** 从全基因组关联研究到机制解释。在最近的一项研究中，Claussnitzer和其同事提出了鉴定FTO基因中的一个与肥胖相关变异位点的疾病驱动机制的综合方法。（[热图、箱线图在线绘制](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485097&idx=1&sn=b25732da52e95ba99cdbf77e1dc45191&chksm=ec0dc323db7a4a35a0b4eac9c865b70ebc7ed37c53e4bbe41194e241aa37344ddf2935df8a74&scene=21#wechat_redirect)，[教师节献礼 \- 文章用图的修改和排版](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484434&idx=1&sn=88b56a24270bd8ee34714f58bc0baa2c&chksm=ec0dc198db7a488e8818b5560a5547a4e574e2d16967953398acd3f38d90723bcbd713e0cbcc&scene=21#wechat_redirect)）  

图a展示了肥胖相关生物机制的整体研究策略，并对每一步进行了顺序编号。最开始的全基因组关联研究（GWAS）中曼哈顿图展示了FTO基因区与肥胖显著相关（图b）。首先，研究人员确定了相关的组织或细胞类型（步骤1）以及下游靶基因。这主要通过调控组学包括染色质状态信息和染色体构象捕获（Hi-C）数据来分析实现的。同时他们确立了该变异为发育基因IRX3和IRX5（步骤2）的表达数量性状基因位点（eQTL）。这是因为在有风险突变的个体中这些基因的表达增加而相邻其它基因的表达则没有改变（图C）。进一步发现IRX3和IRX5的表达与参与线粒体功能的基因表达负相关，与参与脂肪细胞大小调控的基因表达正相关（图d）。然后使用CRISPR-Cas9编辑实验揭示核苷酸驱动变异在ARID5B的富含AT的结合基序中（步骤3，4），并验证了其其分子效应，包括表达特征的改变和调节能量平衡的表型效应对（步骤5）。最后，使用小鼠模型在生物体水平上确立了驱动变异（步骤6）。AKTIP, AKT interacting protein; CEU, Utah residents (CEPH) with northern and western European ancestry; CHD9, chromodomain helicase DNA binding protein 9; CRNDE, colorectal neoplasia differentially expressed; FXR, farnesoid X-activated receptor; LD, linkage disequilibrium; PGC1α, peroxisome proliferatoractivated receptor-γco-activator 1-α; PRDM16, PR domain zinc-finger protein 16; RBL2, RB transcriptional co-repressor like 2; RXR, retinoid X receptor; SNPs, single-nucleotide polymorphisms; TF, transcription factor; TSS, transcription start site; UCP1, mitochondrial brown fat uncoupling protein 1.

**3.2 Direct integration within an individual**

**个体内的直接整合**

多组学技术数据的整合可以在生物调控的多个层次之间建立联系。绘制单个个体的多组学特征图谱将会是全面揭示导致特定生理表型的分子机制的有力工具。然而这些方法需要对同一个体实施多次干预及技术处理，所以比较昂贵，限制了其应用于大量样本。我们实验室第一次进行了这个实验，随访了一个人7年多，而另一个类似的研究随访了另一个人1年。在Chen等的文章中，基因组分析预测到升高的II型糖尿病风险，随后通过详尽的组学分析，包括转录组学、蛋白质组学、代谢组学和其它测量技术等进行了深入验证。特殊地，在呼吸道合胞病毒感染期间，RNA-seq和液相色谱-串联质谱（LC-MS/MS）的蛋白质组学发现参与胰岛素信号传递和响应的基因下调，同时血糖浓度上升至糖尿病患者的水平。多组学技术的优势在于可以在共不变的遗传和个体背景下追踪分子机制的联系，因为可以跟踪分子事件的连续进展，如GWAS鉴定的疾病相关基因的差异表达导致了RNA和蛋白质水平及其相应代谢物的差异。

然而，由于组学分析实验有很高的多重假设检验负担（如基因组中所有的基因或成千上万的代谢物），更大的样本量将有助于确定这种相关性的普遍性。最近一项研究监测了23个个体的不同组学特征，确定了体重增加时的炎症特征，并发现某些代谢途径在体重减轻后没有恢复到正常水平。该分析强调了个体纵向组学特征的相似性，以及在稳态和实验干扰下的个体特异性特征。为了进一步明确这些差异，将这些分析扩展到数千个个体的研究已在早产、炎症性肠病和II型糖尿病中展开。同样地，最近两个独立的研究组分别对遗传和代谢组学数据进行了分析：其中一个计算了100多个个体的多基因风险评分，并与代谢产物的测量值相关联；另一个则是在健康志愿者中鉴定了与个体代谢产物和代谢通路异常相关的罕见有害变异。此外，随着健康个体的组学参考数据库的建立（比如已经可用的有：外显子组数据、基因组数据（如Genome Aggregation Database (gnom AD)和RNA-seq数据），在这些对照组背景下解读个体水平的数据将变得更加容易。

其它工作包括弗雷明汉心脏研究（Framingham Heart Study）和基因组表征研究，如基因型-组织表达（GTEx）项目，以及被提议的enhanced GTEx（eGTEx）项目中扩展到基因表达之外的分析 （[癌症组织特异性基因怎么找？这是个不错的开始](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486593&idx=1&sn=cb9c3877de90e1bd70a6016b6553e4f1&chksm=ec0dc90bdb7a401d4ccf46cf2e2b6a7d542020f6d450173ac25f75937a0bca957a45954b5ab7&scene=21#wechat_redirect)）。这些项目采用了广度优先的组学分析策略，其中大量的个体是通过一组数量有限的只测定一组分子标记（例如全基因组DNA甲基化分析）的技术来绘制图谱。

  

## **_4._ Cancer**

## **癌症**

多组学分析已经并将继续产生巨大影响的领域是对于癌症图谱分析、诊断和治疗的领域。实际上，许多之前讨论的策略（如网络法）在识别癌症的遗传机制上将会是有效的。然而，癌症中不同突变类型 (conceptual differences in cancers)使分析变得复杂化并需要特殊处理。除了识别体细胞变异的技术挑战外，癌症病例中大多数明显的遗传改变是良性的，并不会促进癌细胞生长。因此，确定哪个突变是驱动突变或哪种通路参与其中仍是一个严峻挑战。此外，尽管一些癌症在个体间具有相同的遗传特征，但驱动突变的种类仍然高度多样化，这可能会导致预后和治疗的差异。[肿瘤化疗无效是对预先存在的突变的选择还是诱发新突变，Cell给你答案](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486660&idx=2&sn=5520c681db46dc00f019eaa142b86911&chksm=ec0dc94edb7a405848807c8629d995ead4d4b3f22bb6688bfa4c69fd958e895b10032ad19d72&scene=21#wechat_redirect)  

**4.1 Identifying driver mutations**

**鉴定驱动突变**

一个典型的识别驱动突变的过程包含对多个肿瘤进行全基因组测序（WGS）来识别共有的突变基因。添加功能数据有助于对这些基因的驱动基因的可能性进行排序，因为驱动突变更可能出现在特定癌症表达的基因中。例如，在使用全外显子测序（WES）结合拷贝数变异（CNV）微阵列数据鉴定驱动突变的分析中，RNA-seq数据支持融合基因EGFR-SEPT14的表达，后续功能验证表明该突变确实可影响神经胶质瘤的生长。在另一项使用类似技术的不同分析中，个体内多个转移灶的驱动突变和演化进程在转移灶之间基本相似，表明单个转移灶足以进行下游分析。通过这种方式，使用额外多组学数据与遗传数据共同分析，提供了一种机制来过滤大量的遗传变异，最终获得与功能相关的驱动变异。

**4.2 Molecular signatures of cancer**

**癌症的分子标记**

除了识别驱动突变之外，多组学数据还可以揭示在癌症中活跃的生化途径并将其分类为各种亚型。因此，这是确定患者体内靶向哪种通路的一个有用工具，即使在这些通路中未检测到强候选突变（如难以表征的非编码突变或间接效应）。例如，转录组学和DNA甲基化模式分析已被用于识别与预后相关的癌症亚型。最近，临床蛋白质组学肿瘤分析联盟（CPTAC）的三项研究使用基于蛋白质表达特征的蛋白质组学方法鉴定了结肠直肠癌、卵巢癌和乳腺癌的亚型。重要的是，蛋白质组学数据显示出与转录组和遗传数据重叠但不完全相同的相关性，表明不同的数据类型揭示不同的信息。这些研究展示了的不同遗传和转录过程通过蛋白质组学变化发挥作用。最后，影像学信息与多组学信息的整合有望在癌症诊断和预后中发挥重要作用。

最近，调节基因表达的非编码区域的研究对于理解癌症的调控模式变得越来越有价值。将调控信息的数据集与来自癌症基因组图谱（TCGA，[UCSC XENA - 集大成者(TCGA, ICGC)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484383&idx=1&sn=09c58de206f409fa375fb7af94d0084c&chksm=ec0dc655db7a4f438cb7e53f281cb5c6bf2484619b3c72d7eafe064ea6a342f69587353531af&scene=21#wechat_redirect)，[TCGA数据库在线使用](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484304&idx=1&sn=6ad44dafdc7613e33e13aac48edb32aa&chksm=ec0dc61adb7a4f0c504f3aeb207132aef479572ea756ce15868cbc57f88e9ea25102752b646a&scene=21#wechat_redirect)）的WGS数据整合的一项研究，揭示了一些调控区域富含癌症患者的携带突变。在此情况下，这些非编码区域中哪些突变是驱动变异仍然难以确定，表明还需要相关研究继续对这些变异做进一步筛选；尽管如此，具有相同癌症的个体之间共有的网络拓扑结构可以指示癌症亚型，这些亚型可能有不同的预后和治疗策略。最后，鉴于癌症生长对代谢变化的强烈依赖性，代谢组学很可能在未来的癌症诊断或预后中发挥重要作用。[代谢与肿瘤，超强综述](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486660&idx=1&sn=98a8a96b60c94583c671bc978210b53d&scene=21#wechat_redirect)

  

## **_5._ Challenges**

## **挑战**

到目前为止，大多数整合模型已在科研领域被报道和发表。从首次成功诊断到多机构和国际采纳，临床基因组学的应用在过去几年中迅速扩大。同样，随着纵向多组学分析，最近有了第一个研究实例，在以后也会类似地成为一种临床工具。

然而，对于临床采用的任何技术，在检测和解读中都需要高特异性和灵敏度。目前，除了在特殊情况下使用WES或WGS，这些技术在临床实践中并不经常使用，因为对许多疾病来说它们并未被证明优于当前的检测。未来，必须建立临床指南以确保准确性和有效性，并且必须进行测试以展现其非劣效性和成本优势。

尽管存在以上挑战，组学分析仍是检测大规模变化或通路水平变化的有效方法，比进行数千个独立测试更便宜且通常更全面，并且纵向分析可以显示患者特异的趋势，并可通过重复测量增加统计支持。虽然建立临床指南仍面临挑战，但随着我们对生物的理解和参考数据库的成熟，解释遗传变异（尤其是罕见或新变异）的许多概念可应用于常见分子事件如差异表达基因、新蛋白磷酸化或独特代谢组标记。

**5.1 Analytical challenges**

**分析挑战**

在临床实践中广泛采用综合组学，必须解决各种分析挑战，尤其是用于数据的聚合、可扩展性和集成到电子健康记录（EHR）的统计方法。最重要的是，由于每个数据集都有自己的方差和偏差，因此需要一个稳定且可重复的统计框架来正确分析多个统计上不相干的数据集。多组学数据可以在多个阶段或多维度宏方式 (meta-dimensional)进行分析。简单地说，从这些数据中得出推论的一个方法就是对数据集进行成对分析，增加证据来支持某个结论。然而，同时分析三个或更多个数据集需要更复杂的多维方法，如贝叶斯模型 ([贝叶斯学习记录](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247483765&idx=1&sn=2e991fe6bc748017cf117968d1198e96&scene=21#wechat_redirect))、神经网络或降维[一文看懂PCA分析](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484036&idx=1&sn=22ee356d0c9680d56dada1b777985ed2&scene=21#wechat_redirect)和[还在用PCA降维？快学学大牛最爱的t-SNE算法吧（附Python/R代码）](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484978&idx=1&sn=07b7f734ad0ad44562186c1ef3663057&scene=21#wechat_redirect)。多组学数据类型本质上的不同使得问题进一步复杂化：例如遗传变异数据是离散和静态的，而RNA-seq数据是连续的并且可以提供纵向信息 （[WGCNA分析，简单全面的最新教程](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485220&idx=1&sn=007188964e7c43d75dcd0b11b880bbfa&chksm=ec0dc2aedb7a4bb84c460da4d34aee1092baaedc038fc467ffee7f70ccb55dd843fdc03f48fe&scene=21#wechat_redirect)）。

尽管上述数据分析方法对于理解生物学和疾病是有效的，但它们可能不一定适用于临床上个体水平的数据分析。在基因组学领域，通过个体的基因型和GWAS数据库，可以计算多基因风险值来评估个体的患病风险。构建这样的多组学分析框架仍然面临一个主要障碍，即可能会面临一些比如难以将一个群体的结果应用于另一个群体的个体中类似的挑战。

除了分析方法的挑战之外，这些分析和所有相关数据的存储还需要巨大的计算资源：尽管个人的多组学数据量是可控的（例如，太字节数量级（1TB, 10^12 bytes））。但是这些数据需要放入更大的背景集中以理解与背景分布的偏差，这需要来自数千个样本（艾字节数量级（1EB , 10^18 bytes））的数据。幸运的是，云计算慢慢可以缓解这些问题，根据每个医院或医疗保健服务系统的特定需求提供弹性的计算和存储设备，同时提高计算过程的可重复性。[可重复性编程bookdown](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484988&idx=1&sn=b9543625901cf3aabd4e8b0373b52347&scene=21#wechat_redirect)和[Python文学化编程 - Jupyter notebook使用和插件拓展](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484855&idx=1&sn=d67d4bf2fa18ac7593b392c21321706c&scene=21#wechat_redirect) 。

目前，这种综合数据集通常没有可用于研究的标准格式，更不用说用于结构化的临床系统；因此，需要建立基础设施结构来管理这些数据，而这会带来财务和行政负担。特别是，卫生信息学家的任务是建立一个在电子健康记录（HER）中存储遗传和转录组学数据的强大基础设施。此外，需要临床医生和研究人员的共同努力来决定将哪些信息报告给患者并纳入EHR。

**5.2 Accuracy and validation**

**准确性和验证**

个体水平上，全基因组数据集存在固有错误率，结构变异也仍然难以检测和识别（因此也很少被提及）。更连续和纵向的数据如mRNA表达和蛋白质组数据，根据所测定的组织特征其准确性可能更难以评估，但是这些方法有较高技术重复和生物学重复性。在某些情况下，这些技术独立地识别同一生物学过程的不同方面，因此可以相互验证：例如RNA-seq可以重现由WES或WGS鉴定的外显子变异，而蛋白质组表达可以验证RNA-seq的表达。然而，在需要高可信度的临床环境中，这些测试目前由其它独立的技术验证，可能包括现有的临床测试如酶法或低通量测定试验。

对于癌症基因组学，解读异质性数据是一项重大挑战。由于每个肿瘤是由具有不同程度体细胞突变的细胞组成的嵌合体，即使不区分伴随突变和驱动突变，变异的检测也很困难。特别是癌症中的体细胞突变是纯系突变还是仅在组织中的一部分细胞中出现，使得变异的发现复杂化，因此需要高覆盖度和高质量数据将其与测序错误区分开来。利用细胞游离DNA（cell-free DNA）的超深度测序追踪血液中痕量癌症突变的存在以及利用单细胞测序检测癌症的异质性正成为强有力的方法。然而，用于检测早期癌症的细胞游离DNA方法需要稳健的方法来区分真正的低频（变异）事件与测序错误，并且单细胞测序仍然很昂贵。尽管如此，这些方法已经被用于解析肿瘤异质性并在产前检测中识别出癌症的一个附带突变。随着其它组学数据集与超深度测序结合，我们期望这些方法能够优势互补，为临床分子咨询提供独特而且强大的方法。

**5.3 Interpretation**

**解读**

即使拥有高度精确的数据，另一个困难在于对基因组规模结果的解读，特别是罕见的和新的分子事件，它们通常远远超过可以合理地进行功能验证的（分子）事件的数量。个体基因组中的许多变异，特别是以前没有见过且没有明确功能效应的，被称为“不确定意义的变异（VUS）”，该问题对于其它数据类型（例如转录组或蛋白质组数据）也存在。另外，判断临床上重要的分子事件如RNA表达阈值在不同的数据类型中很难确定。幸运的是，可用于外显子组、基因组测序（gnom AD）和基因表达的大型群体参考数据集已可用。它们通过提供群体中的实际（变异）频率来帮助解释罕见事件。特别是，驱动变异在受影响的个体中应该比在更多的无症状群体中有更高的变异频率，这可以支持或否定先前的致病机制。此外，医生可能会发现不相关条件下的其它致病性分子事件，也称偶发性发现，对于哪些结果反馈给患者到什么程度的信息仍存在相当大的争议。

当结合多组学技术时，这些问题有时会得到改善，尤其是对于那些难以进行统计分析的、罕见的及新的分子事件。特别是，显示为正交信息的多组学技术的直接整合可以为某个分子事件提供额外的证据：例如，如果RNA-seq显示VUS（不确定意义的变异）影响关键疾病基因的剪接，则可以证实其潜在的致病机制。通过这种方法，多技术整合可以建立起单一技术无法实现的因果关系链。

**5.4 Finding the relevant tissue**

**寻找相关组织**

为了维持样品间的一致性，许多大规模研究对已经得到的样品进行了分析，例如血液或细胞系，包括转化的淋巴母细胞样细胞系（ [被高中生物骗了这么多年，原来人体内细胞的DNA是有不同的？](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485441&idx=1&sn=4b103429791cc4f26b4922e95050af0a&chksm=ec0dcd8bdb7a449deb92453075afd43b00ff40b6f36ffdc8b3d2255ec4fa4981d14a20a6cd3e&scene=21#wechat_redirect)）。然而，对于临床应用，理想情况是研究与特定疾病相关的组织，因为基因表达在不同组织中显著变化（图3）。GTEx、表观组学路线图和哺乳动物基因组的功能注释5(FANTOM5)项目为多组织基因表达和表观基因组数据提供了参考数据集。多数情况下，疾病相关组织可能已有记录，例如MD（肌营养不良）的肌肉组织。然而，如果疾病定义不太明确或组织不可用，则可以通过对疾病的网络分析来鉴定组织。事实上，已证明使用疾病相关组织对MD患者的诊断是有益的。对肌肉组织的转录组分析得到的诊断结果不同通过储蓄替代组织（例如血液或成纤维细胞）来获得，因为疾病相关基因在这些里面表达低。

在将此类数据用于临床应用时，应注意确保来自患者样本的数据与参考数据集具有可比性，这对于整合其它组学数据（例如代谢组学和蛋白质组学）将是至关重要的。当然，在组织（例如大脑）中存在大量细胞异质性的情况下，这种分析更加复杂：在此情况下，具有单细胞分辨率的技术将为解析每种单独的细胞类型提供有价值的见解。在原代组织难以获得或难以维持培养的情况下，使用CRISPR系统将突变引入诱导多能干细胞（iPS，[周琪院士正面回应：60万一针有用吗？（干细胞治疗）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485358&idx=1&sn=6589592ef174e1513ae79e2a8d9a1250&chksm=ec0dc224db7a4b327fe1a65f4b92cd6ad10c5e11dcb01f24a02375463a981b1cb6e5a04d8567&scene=21#wechat_redirect)）可以为分子验证提供一个强有力的方法。

![](http://www.ehbio.com/ehbio_resource/omics_finger3.png)

**图3** 寻找相关组织。由于其可用性和易于采集（a部分），血液通常是最方便的实验组织，但它通常不是观察特定疾病如主要影响脑或肺的疾病的分子表型的理想组织。特殊地，相比于疾病近端组织（例如肌营养不良的肌肉组织），血液的转录图谱（包括表达水平、剪接模式和增强子的使用）可能不适于检测这些疾病。

**5.4 Actionability and therapeutics**

**可操作性和治疗**

在讨论临床中使用的任何技术时，可能最重要的是其可操作性。实际上，一部分信息不足以说明其有意性：掌握诊断知识并结束诊断过程对患者和家属来说是很有帮助的。 然而，在一个被称为“精准医学”或“个性化医疗”的体系中，可以指导干预的数据将十分有用。尤其是，对患者的疾病亚型进行分类以推荐特定的药物，在组学分析（BOX 2）的基础上来确定潜在移植是否匹配良好，或确定新疾病的驱动机制（并开发可以靶向直接分子产物的治疗方案），可以改善治疗结果并延长患者的生命。然而，即使是与治疗结果在统计学上存在相关性的非驱动性分子事件也有可操作性，特别是以改变生活方式的建议形式，包括饮食、监测和预防性治疗；事实上，具有高遗传性冠心病风险的个体从他汀类药物治疗中获益更大。

  

>**Box 2**
>
>**方框2** **. 移植供体和受体的多组学分析**
每年有数千名患者接受器官和造血干细胞移植，但移植患者的死亡率仍然很高。检测供体与受体匹配的惯例做法涉及人白细胞抗原（HLA）分型，最近已使用高通量测序技术开发了这种方法。然而，越来越清楚的是，非HLA因子可以显著影响移植物抗宿主反应（GVHD）的预后和发展，因为HLA匹配的同胞供体移植比HLA匹配但却无关的供体移植具有更低的GVHD风险，且常见的非HLA多态性与GVHD有关。

>因此，多组学可用于确定最佳供体-受体匹配，以及监测排斥标记物。例如，对细胞游离DNA进行测序可以检测循环的供体DNA，其水平与器官排斥的严重程度相关。另外，对这种细胞游离DNA进行测序可同时检测病毒DNA以指示感染标志物。其它组学数据，例如RNA或蛋白表达，也可用于评估供体-受体间的相容性，以及监测排斥标志物。整合组学技术可能成为移植生物学的有用工具。  

  

## **_6._ Conclusions and future perspectives**

## **结论和未来展望**

目前，组学技术（尤其是基因组测序以及较小程度的RNA-seq）仅在极少数情况下显示出优于传统的临床测试，因此将这些技术纳入临床实践存在较大的技术和监管障碍。然而，由于使用多种技术可以更清晰地了解健康和疾病，这些技术的整合很可能在未来的临床实践中成为普遍现象。此外，最近大型生物银行计划（如UK Biobank, Million Veterans Project和“All of Us”计划）收集了生物数据并对数百万人进行多组学分析，这将对人类疾病产生深刻的理解，并为更多其它的研究和临床应用提供有价值的参考数据库。

**6.1 Predictive models of disease risk for healthy individuals and early detection of disease**

**健康个体的疾病风险预测模型和疾病的早期检测**

与传统的临床检测一样，大规模组学数据的分子测量可以整合到疾病风险模型中。特别是最近，已经开发了一组用于计算特定疾病遗传风险的方法，称为多基因风险评分。这些方法成功地将某个疾病（如心血管病等疾病）的患者分为高风险和低风险类别。在有了基于遗传学或是家族史的疾病风险预测结果后进行针对性检测。例如，如果一个患者被预测患有II型糖尿病的风险，则进行葡萄糖和糖基化血红蛋白（HbA1c）水平的测定和其它测试，例如葡萄糖耐受性测试。然而，如果在未来能够同时高质量和低成本地进行代谢组学的测量，那么将不再需要进行单独化学测试。此外，来自可穿戴设备的持续收集的数据可与组学数据相结合用于在疾病症状出现之前的早期检测。

**6.2 Disease management**

**疾病管理**

除了疾病预测和早期诊断外，整合组学在疾病治疗和预后方面的作用将会变得越来越强大。来自转录组、表观基因组、微生物组、蛋白质组和代谢组的信息以及成像和可穿戴设备的数据都将用于帮助破译疾病，促进预后，从而指导治疗。在癌症中，肿瘤-正常组织对（tumour–normal pairs）的DNA和RNA测序已经鉴定了易位（变异）和基因表达的特征，针对性的靶向治疗进而治愈疾病。在未来，随着多组学的测量数据与疾病的预后关联，这种数据驱动的范例很可能会成为医学研究的有力工具，也将有助于促进临床诊断和治疗。

原文：Integrative omics for health and disease,  DOI: 10.1038/nrg.2018.4

翻译：RPM，宋红卫，凌路頔  

  

整合组学这么有用，要不要入门下生物信息学？[生物信息之程序学习](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247483927&idx=1&sn=23adf2b9d13400f2081f790e674e2cba&chksm=ec0dc79ddb7a4e8b5bb7a413744319a90f425371b30e2c85224b7c183cc4ad4bbd5d9749bb7b&scene=21#wechat_redirect)，[该如何自学入门生物信息学](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486486&idx=1&sn=32960c5a409236f7c808eb3d7e16ec4c&chksm=ec0dc99cdb7a408a87eb783c2f987029456666f7235c01e40513bf6e9ab97d9c6025408f8efc&scene=21#wechat_redirect)，[关于编程学习的一些思考](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486311&idx=1&sn=aa1c105982b7781201c6b99b94b4f112&chksm=ec0dceeddb7a47fb7f2f9a1c3b6e9606ba3da31b5c4dc3b58034e427ff31409919b0ee611a5e&scene=21#wechat_redirect)。也可以加入我们的培训班，一起学习，广受好评哦。

### 蛋白质组学研究

*   [蛋白质组学研究概述](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485530&idx=1&sn=1b11166354d38dc7999bcfff3d0cf7bc&scene=21#wechat_redirect)
    

### 转录组研究

*   [39个转录组分析工具，120种组合评估(转录组分析工具哪家强-导读版)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484106&idx=1&sn=687a0def51f6ea91a335754eb3dc9ca9&scene=21#wechat_redirect)
    
*   [39个转录组分析工具，120种组合评估(转录组分析工具大比拼 （完整翻译版）)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484106&idx=2&sn=a09fa127d625c4072ae0343795346c56&scene=21#wechat_redirect)
    
*   [无参转录组分析工具评估和流程展示](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484402&idx=1&sn=f214ec35ff71bc4577f884584e9c9732&scene=21#wechat_redirect)
    
*   [120分的转录组试题（第一份答案）](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485337&idx=1&sn=c216e59d64a2369dc2b62bec8905e160&scene=21#wechat_redirect)
    
*   [120分的转录组试题（第二份答案）](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485353&idx=2&sn=8fab8057d8acd21407cc5e4ade98f498&scene=21#wechat_redirect)
    
*   [120分的转录组试题（第三份答案）](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485353&idx=3&sn=1342b515dc9b42555107db49b4d77f00&scene=21#wechat_redirect)
    
*   [DESeq2差异基因分析和批次效应移除](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485368&idx=1&sn=12b20487e9014ce2e69f01d3efbc6ce8&scene=21#wechat_redirect)
    

### 文献精读

*   [肿瘤化疗无效是对预先存在的突变的选择还是诱发新突变，Cell给你答案](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485395&idx=1&sn=b02eda7f1076ca1c53350bdc0d77020f&scene=21#wechat_redirect)
    
*   [“人鸡胚胎”破解生命起源奥秘，百年来首次证实“组织者”存在于人体 ｜《Nature》发表重磅论文](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485372&idx=1&sn=9dada1ff1dfcd10b4c292b74f793213b&scene=21#wechat_redirect)
    
*   [被高中生物骗了这么多年，原来人体内细胞的DNA是有不同的？](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485441&idx=1&sn=4b103429791cc4f26b4922e95050af0a&scene=21#wechat_redirect)
    
*   [周琪院士正面回应：60万一针有用吗？（干细胞治疗）](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485358&idx=1&sn=6589592ef174e1513ae79e2a8d9a1250&scene=21#wechat_redirect)
    
*   [CRISPR-CAS9发展历程小记](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484956&idx=1&sn=7de42d26a5c76edc07bcd9b76d05728c&scene=21#wechat_redirect)
    
*   [一场大病引起的诺贝尔2017年生理学奖角逐](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484544&idx=1&sn=6f86e3a88dd588eb873dd78cd9ebcbc8&scene=21#wechat_redirect)
    
*   [Science搞反狗脑 - 人脑和狗脑一样？](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484637&idx=1&sn=0d2ddad01c323f18cdf426e6eeb9546a&scene=21#wechat_redirect)
    
*   [一篇压根不存在的文献被引用400次？！揭开” 幽灵文献” 的真面目](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484720&idx=1&sn=0105ed274a0a95d28ca9701ae2b4aa11&scene=21#wechat_redirect)
    
*   [基于人工智能的文献检索，导师查找，更聪明](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484687&idx=2&sn=f1c743aaaf7765139cb48560c722917b&scene=21#wechat_redirect)
    
*   [GeenMedical：文献查询、筛选、引用排序、相似文献、全文下载、杂志分区、影响因子、结果导出、杂志评述、直接投稿，一站服务](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484667&idx=1&sn=996cf1c19ebff278db5141d7c2a0ed9a&scene=21#wechat_redirect)
    
*   [YANDEX搜索，不翻墙稳定使用近谷歌搜索](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484837&idx=1&sn=09fc49b83dc6b68862b5909630b080a5&scene=21#wechat_redirect)
    
*   [Nature我的研究对后人毫无用途：21%的学术论文自发布后从未被引用](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484883&idx=1&sn=8f5e747e34f51fd84a84f1d235759395&scene=21#wechat_redirect)
    
*   [SCI-HUB镜像,  SSH隧道访问学校内网](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484973&idx=1&sn=f3b4fa48b3a7911416e1592206dd06e2&scene=21#wechat_redirect)
    
*   [为了速成生物学，一位程序员探索了”爆款”基因背后的秘密](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485036&idx=1&sn=5b12e9ed89bed48bfc5655f9d016cbcd&scene=21#wechat_redirect)
    
*   [Nature邀请6位专家为您支招如何写出一流论文？](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485086&idx=1&sn=a6b1826e63d4ab32cda3fdda5c2b537c&scene=21#wechat_redirect)
    
*   [Cell：荧光标记out了，AI不用“侵入”也能识别细胞死活和类型](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485227&idx=2&sn=2ce0a0820f07fd281f333ed7241032e3&scene=21#wechat_redirect)
    
*   [如果你经常用PubMed，那么这个插件将非常好用！](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485323&idx=1&sn=8fef0d264748d81488cf8364c6a5eab0&scene=21#wechat_redirect)
    
*   [生物研究中不可缺少的数字概念，多少，多大，多快](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484889&idx=1&sn=4f50f79a9c1b64cc10051f8ab4ad4173&scene=21#wechat_redirect)
    
*   [王秀杰研究组合作发现m6A修饰在小脑发育中的新功能 （附2018上半年m6A研究文章和点评）](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485507&idx=1&sn=b7fba1b18cd6dd868444371a254f9852&scene=21#wechat_redirect)
    
*   [把人类宝宝和黑猩猩幼崽一起养大，会发生什么有趣的事情呢？结局可能是有些出乎意料的～～](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485529&idx=1&sn=2f78b5af2e8e0f4c3a869f63a2f4cc22&scene=21#wechat_redirect)
    
*   [你体内的细胞“成精了”？居然还互相看对了眼？](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486381&idx=1&sn=a92c1670e598af7b99da4bf73ba4f978&scene=21#wechat_redirect)
    
*   [父爱无言！科学家首次发现来自爸爸的基因，可以通过胎儿来控制妈妈对宝宝的爱](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486530&idx=1&sn=c9f7ef3baa9735638115b407db67f2e9&scene=21#wechat_redirect)
    
*   [2018 Cell系列相变最强综述，未来已来，你在哪？](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486630&idx=1&sn=7d086ec4aa13fdf6af727e833f079444&chksm=ec0dc92cdb7a403ae912517d3df464797a74785de96d92cdd3617d6752fc73e52a64c580dcab&scene=21&subscene=126&ascene=0&devicetype=android-22&version=2607023a&nettype=WIFI&abtest_cookie=BQABAAgACgALABIAEwAFAJ6GHgAmlx4AWZkeAGmZHgBtmR4AAAA=&lang=zh_CN&pass_ticket=Jf)
    

### 更多阅读

[画图三字经](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484523&idx=1&sn=34b595177cbe0fa8faf34d09d71ac8ec&scene=21#wechat_redirect) [生信视频](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485004&idx=1&sn=5f9f7b2cb20a191be87c17ab9d9980e4&chksm=ec0dc3c6db7a4ad0718d640bce966f25aa23eee1648e87c784a183ba80a7f8419f32c538d3c1&scene=21#wechat_redirect) [生信系列教程](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485155&idx=2&sn=73ffb2532846ca4b49bf0e74f11896ca&chksm=ec0dc369db7a4a7fc1494f739fe0a9f7c756d778a6b4d997ec7e385ff421f6f9894b761de95b&scene=21#wechat_redirect)

[心得体会](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247483927&idx=1&sn=23adf2b9d13400f2081f790e674e2cba&chksm=ec0dc79ddb7a4e8b5bb7a413744319a90f425371b30e2c85224b7c183cc4ad4bbd5d9749bb7b&scene=21#wechat_redirect) [癌症数据库](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484383&idx=1&sn=09c58de206f409fa375fb7af94d0084c&chksm=ec0dc655db7a4f438cb7e53f281cb5c6bf2484619b3c72d7eafe064ea6a342f69587353531af&scene=21#wechat_redirect) [Linux](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484606&idx=1&sn=c5f2654e3ede87f534bc352f286a6357&chksm=ec0dc134db7a48228044e720eff4cc39ea2b9258db7d20faafbcae29a47ef7de334678fad35a&scene=21#wechat_redirect) [Python](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247483866&idx=1&sn=310341a1c8d348958c304df03dfd06a0&chksm=ec0dc450db7a4d46e369637cd2867b0e56389bf4f2e1d0dce409bba38882e61e5063308a13af&scene=21#wechat_redirect)

[高通量分析](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484034&idx=1&sn=e7680ee935f8603214227b37eeb2c567&chksm=ec0dc708db7a4e1eca4e38845381f328c49c84a90ad6580c3ba3761511772636e5ec0f185931&scene=21#wechat_redirect) [在线画图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485097&idx=1&sn=b25732da52e95ba99cdbf77e1dc45191&chksm=ec0dc323db7a4a35a0b4eac9c865b70ebc7ed37c53e4bbe41194e241aa37344ddf2935df8a74&scene=21#wechat_redirect) [测序历史](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485298&idx=1&sn=36c8024abb89fd5f408578af06ef4313&scene=21#wechat_redirect) [超级增强子](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485257&idx=1&sn=02000c839eb023a9cb3c5ba07f7d0e4c&scene=21#wechat_redirect)

[培训视频](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485237&idx=1&sn=33dba0d3ddf7cc71d319715722e36c14&scene=21#wechat_redirect) [PPT](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485139&idx=1&sn=a9b45f10c8722e78e54bfdd93587dc72&scene=21#wechat_redirect) [EXCEL](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485378&idx=1&sn=970e2a8cec0ee600d71eec2981d385aa&scene=21#wechat_redirect) [文章写作](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484941&idx=1&sn=799b8a6376d2e17e24fd39d9fc10b3b3&scene=21#wechat_redirect) [ggplot2](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247486262&idx=1&sn=d38221a4063d866b1f10f4c9ebab5f88&chksm=ec0dcebcdb7a47aa03ff27872048304d33be27d1ab8bd3af0aefc320366a4bd3aceb943cb384&scene=21#wechat_redirect)

[海哥组学](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485782&idx=1&sn=f9b05d0a6b22861a871e062688942b66&chksm=ec0dccdcdb7a45ca9414e53a8977ce834a1074f239885cf150a4a9f93d9a90880569350847da&scene=21#wechat_redirect) [可视化套路](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485822&idx=1&sn=240cc5593ddc303d6c5d66edc7841033&chksm=ec0dccf4db7a45e24e0db1f84defc3924bc1728a9306e19b74e14e24f59082c4f081712f21d5&scene=21#wechat_redirect) [基因组浏览器](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485735&idx=1&sn=be17e018bce29190832357c658bb4255&chksm=ec0dccaddb7a45bb37d80f74694dfd6ca8a006b33e16b8907a808204ff480dbdc045077d0ef4&scene=21#wechat_redirect)

[色彩搭配](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247485182&idx=1&sn=7b5c1d800560eddcf898ed410720a2a3&scene=21#wechat_redirect)   [图形排版](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484492&idx=1&sn=10c9b2308065b6260cfc69ea9e8d065f&scene=21#wechat_redirect) [互作网络](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484964&idx=1&sn=32a1f7af15e8a28a224a52beef28ca59&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484624&idx=1&sn=7f97f3cd03d6891f71ac3bb778ad84bb&chksm=ec0dc15adb7a484c0c1a3cfe25892c22d3ffc21276d7ac8ed5794f020b99003a86b3c6d5bc31&scene=21#wechat_redirect)


