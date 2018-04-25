---
title: 从Richard Young教授的系列研究看超级增强子发现背后的故事 (附超级增强子鉴定代码)
author: ct
layout: post
categories:
  - Bioinfo
tags:
  - Python
  - Bioinfo
  - 生物信息
---

`Richard Young`教授，美国科学院院士，就职于Whitehead研究所，是基因转录和表观调控研究的先驱，做出了很多开创性发现。

2013年关于**超级增强子**的研究，引燃了这个领域。超级增强子的发现看上去是偶然，但遍历其在转录调控领域的研究，这个发现又是必然，是知识积累到一定程度，融汇贯通的结果。

也许我们在处理高通量数据的过程中，也发现过类似的区域，但因为不敏感或不确信，更多的是因为没有足够的**知识积淀**来解释这个现象存在的原因或意义，导致我们与大发现失之交臂。

超级增强子发现的那一年，有幸遇到Richard Young教授，就请教了下为啥会起这个名字，Young教授说，看到这个区域了，为了**方便研究**就随便给了个名字。看来会起名字，是科学研究的第一步。要不然叫着都不顺口，怎么去跟导师交流，怎么能让人记住，让自己记住。

当然这只是大牛的谦虚，人家起这个名字是因为看得远，一语道出了重要作用。

接下来我们捋一捋大牛10年间做过的研究，跟随大牛的脚步，去学下如何做数据分析。

2000年发明 **ChIP-chip**，鉴定了`Gal4`和`Ste12`的结合图谱，并结合不同生长条件下的转录图谱，进行了转录因子结合和基因表达的**关联分析**。这篇文章，放在现在，也很具有参考意义。

这是华人大牛**任兵**教授在Richard Young教授做博后时的重要产出之一。

![](http://www.ehbio.com/ehbio_resource/RA2000.jpg)


2002年，扩大样本量，整合分析106个调控因子的结合图谱。构建了106个调控因子与2343个基因之间的4000多调控结合关系，构建**调控网络** ([网络构建](https://mp.weixin.qq.com/s/sKEy_Pn9qnWw4W-aXraA5g))，发现调控因子之间存在较强的互调控关系。

![](http://www.ehbio.com/ehbio_resource/RA2002.jpg)

2004年综合**结合图谱**、**Motif分析**、**序列保守性**揭示转录调节代码，即转录因子在启动子区的结合模式及其在不同环境下的调控变化。(现在做motif分析，也无外乎这些)

![](http://www.ehbio.com/ehbio_resource/RA2004_1.jpg)

![](http://www.ehbio.com/ehbio_resource/RA2004_2.jpg)

这样就把转录因子的分析工作能做的都做了，下面就到了组蛋白修饰方面。

2008年，活性启动子区的双向转录，发现转录延伸与**H3K79me2**相关。

![](http://www.ehbio.com/ehbio_resource/RA2008.jpg)

2010年，承接上面的工作，发现`cMyc`调节`Pol II`启动转录延伸。在人胚胎干细胞中，约30%的基因有转录起始进程，却检测不到转录延伸。转录复合体招募形成后不会立即转录，而是在启动子近端停留；转录因子cMyc则发挥促进转录复合体运转的作用。

这篇文章也是研究的一个很好的范例，首先确认**是不是** (转录起始和延伸不成比例)，然后看**谁参与** (关联不同转录因子，这里有个背景是cMyc与之前发现的转录释放因子PTEFb存在互作)，然后**多方证据**证明cMyc确实与POL II的释放有关 (这里选取的对照、和采用的计量方式都值得借鉴)。最后**干扰**下，确实有效果。完美结束故事。


![](http://www.ehbio.com/ehbio_resource/RA2010_1.jpg)

![](http://www.ehbio.com/ehbio_resource/RA2010_2.jpg)

![](http://www.ehbio.com/ehbio_resource/RA2010_3.jpg)

当然关于cMyc的研究却没结束，2012年有一篇cell，发现cMyc可以引起肿瘤细胞中**整体**转录水平升高。(**注意**：cMyc肿瘤中绝大部分活性基因的增量表达，做肿瘤转录组时，严格一些记得要加**spike-in**，不然相对定量就容易把差异抹去了)

还是2010年，发现Mediator和cohesin可以通过介导染色体结构调节基因表达。**Mediator**很关键，也是后面发现超级增强子的一个功臣。

大规模shRNA筛选哪些基因的敲除对多能性基因的表达影响最大。

![](http://www.ehbio.com/ehbio_resource/RA2010M1.jpg)

从结合图谱确认Mediator和cohesin敲低后，影响基因表达的机理。后续有**3C**实验验证染色体结构确实发生了变化。

![](http://www.ehbio.com/ehbio_resource/RA2010M2.jpg)

2013年发现**超级增强子** (super enhancer)，成簇的增强子。最开始定义是：Oct4，Sox，Nanog共结合的区域包含成簇的增强子定义为超级增强子，其调控转录的强度和敏感性都更高。

后来关联到上一篇工作提到的Mediator：**Med1**的结合强度把增强子分成2类，大约40%的Med1信号出现在231个大的增强子上。这个关联就成了超级增强子鉴定的一个依据。


![](http://www.ehbio.com/ehbio_resource/Super1.jpg)

随后是超级增强子的结构特征和功能分析，这个GSEA图很有意思，充分利用上一篇文章中的大规模敲除结果，发现超级增强子调控的基因富集与对多能性因子影响最强的基因中，定格了超级增强子的重要功能。[GSEA还不会，看这里](https://mp.weixin.qq.com/s/3Nd3urhfRGkw-F0LGZrlZQ)。

![](http://www.ehbio.com/ehbio_resource/Super2.jpg)

超级增强子的富集峰图很有意思，平常见多了**Gene body**区域的富集，习惯了有高有低的分布。而超级增强子内TF的结合分布均一，这个图咋一看上去没什么特色，而这个没特色作者却能解释成很重要的特色，是很好的看问题视角。区域内怎么分布没关系，反正是普遍高，高于两端区域，就是好的现象。

![](http://www.ehbio.com/ehbio_resource/Super3.jpg)

关联完转录因子，再关联**组蛋白修饰**，毕竟转录组因子数据少，又有细胞特异性，不适合用于大规模鉴定，发现**H3K27ac**可以标记超级增强子，并有细胞特异性。再刷一波cell。

![](http://www.ehbio.com/ehbio_resource/Super4.jpg)

来一张图，检验下做调控的你知识储备是否足够，看看这些调控元件知道多少？如果都不知道，怎么能谈得上活学活用、关联分析呢？

![](http://www.ehbio.com/ehbio_resource/RA_review.jpg)

Richard Young教授的文章还有很多，这里选了一部分表观调控为主的文章，其在胚胎干细胞调控网络、miRNA调控等领域都有很多好工作，每一篇文章都值得拿过来掰开了慢慢看。也许看的多了，可以从中看出大牛思考的蛛丝马迹，给自己的科研加一些助力。后台回复 **RA**获取文章全文和采访视频。想重复文章的图，参考之前发布的[ChIP-seq基本分析流程](https://mp.weixin.qq.com/s/nldZ1_wiCmCtLO3MWJuQ8Q)，和我们的视频课 <https://ke.qq.com/course/291881>。

### 超级增强子鉴定代码

这个是基于super-enhancer的文章描述和Richard Young教授实验室发表的ROSE软件，制作的一个简化版，也是我们在本期ChIP-seq培训时大家一起讨论出来的解决方式，发布出来，供大家批评指教。线下集训是很好的方式，欢迎大家参加正在筹备的[二代三代转录组测序分析实战班](https://mp.weixin.qq.com/s/Pf8oVwPCDrlaT8KMxWu7xg)。

这个流程没有考虑鉴定出的增强子与基因区的关系，另外流程稍作修改，可用于鉴定**各种超级图谱**，如超级TF结合，超级组蛋白修饰结合，都可以。

```
# 组成型增强子排序
bedtools sort -i mm10.enhancer.bed >mm10.enhancer.sort.bed

# 距离在12.5 kb内的增强子归为一簇
bedtools cluster -d 125000 -i mm10.enhancer.sort.bed >mm10.cluster.enhancer.bed

# 计算每个增强子的H3K27ac结合强度
bedtools coverage -c -a mm10.cluster.enhancer.bed -b MESC_H3K27ac/MESC_H3K27ac.rmdup.bam \
        >mm10.cluster.enhancer.H3K27ac.profile_tmp

# 对每簇增强子的结合强度做簇内加和
# 注意： -g 指定以那一列分组，指定的应该是标记分簇的数字所在的列; 
# -c 表示对coverage所在的列计算加和 (-o sum)，注意列需要根据实际指定
bedtools groupby -i mm10.cluster.enhancer.H3K27ac.profile_tmp -g 5 -c 6 -o sum \
        >mm10.cluster.enhancer.H3K27ac.profile
```

以下为R代码请在R中运行

```
#####以下为R代码
enhancer = read.table("mm10.cluster.enhancer.H3K27ac.profile", 
        header=F, row.names=NULL, sep="\t")
head(enhancer)
# 注意查看丰度信息是否在第二列，若不在，则需做相应修改
H3K27ac = sort(enhancer$V2)

plot(H3K27ac, col=2, type="l")

# 计算拐点, 代码取自ROSE
numPts_below_line <- function(myVector,slope,x){
  yPt <- myVector[x]
  b <- yPt-(slope*x)
  xPts <- 1:length(myVector)
  return(sum(myVector<=(xPts*slope+b)))
}

inputVector <- H3K27ac
#set those regions with more control than ranking equal to zero
inputVector[inputVector<0]<-0 

# This is the slope of the line we want to slide. This is the diagonal.
slope <- (max(inputVector)-min(inputVector))/length(inputVector) 

# Find the x-axis point where a line passing through that point has the minimum number 
# of points below it. (ie. tangent)。
# 该点就是切点
xPt <- floor(optimize(numPts_below_line, lower=1, \
        upper=length(inputVector),myVector= inputVector,slope=slope)$minimum) 

y_cutoff <- inputVector[xPt] #The y-value at this x point. This is our cutoff.

b <- y_cutoff-(slope* xPt)
abline(v= xPt,h= y_cutoff,lty=2,col=8)
points(xPt,y_cutoff,pch=16,cex=0.9,col=2)
abline(coef=c(b,slope),col=2)
title(paste("x=",xPt,"\ny=",signif(y_cutoff,3),"\nFold over Median=", 
        signif(y_cutoff/median(inputVector),3),"x\nFold over Mean=",
        signif(y_cutoff/mean(inputVector),3),"x",sep=""))

#Number of regions with zero signal
axis(1,sum(inputVector==0),sum(inputVector==0),col.axis="pink",col="pink") 

## 超级增强子cluster
enhancer[enhancer$V2>=y_cutoff,1]
```




