---
title: Using RankProd and limma to sort out DE genes
author: 悟道
layout: post
permalink: /?p=3068
categories:
  - R
  - sta
tags:
  - R
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.data

<pre class="brush: bash; title: ; notranslate" title="">head(a,5)
             wt1    wt2    mu1    mu2
A2LD1_2    109.6  130.4   92.0   88.8
A2M_3     3982.3 4308.7 1615.0 1368.6
AAAS_4     131.1  122.2  130.0  114.9
AACS_5     152.3  116.0  155.5  162.4
AADACL1_6  486.4  628.2  348.6  349.7

</pre>

2.Required packages

<pre class="brush: bash; title: ; notranslate" title="">source("http://bioconductor.org/biocLite.R")
biocLite('RankProd')
biocLite('lima')
</pre>

4.Perform analysis

<pre class="brush: bash; title: ; notranslate" title="">library(RankProd)
cl &lt;- c(0,0,1,1)
#data &lt;- data1 #for old process, delete unneeded columns
data.RPout &lt;- RP(data, cl, num.perm=100, logged=F, na.rm=F, plot=F,rand=123) 
#rand mens giving a seed to make each operation repeatable. logged to indicate if the data is log transformed.
RP.tbl &lt;- topGene(data.RPout, cutoff=0.1, method="pfp" ,logged=F,gene.names=rownames(data))
#RP.tbl$Table1
#RP.tbl$Table2

write.table(RP.tbl$Table1, file="UPinMu.txt"
        ,quote=F, sep=" \t" ,row.names=T,col.names=T)
write.table(RP.tbl$Table2, file="DWinMu.txt"
        ,quote=F, sep=" \t" ,row.names=T,col.names=T)

&gt; head(RP.tbl$Table1)
              gene.index RP/Rsum FC:(class1/class2) pfp P.value
GCA_4613            4612  1.8612             0.1151   0       0
FLJ35767_4355       4354  2.5149             0.1365   0       0
SH3GL3_12363       12362  2.9130             0.1400   0       0
CNN3_2603           2602  3.4641             0.1332   0       0
IFITM3_5812         5811  3.4996             0.1349   0       0
BEND7_1050          1049  5.7850             0.1581   0       0
&gt; head(RP.tbl$Table2)
               gene.index RP/Rsum FC:(class1/class2)    pfp P.value
KYNU_6370            6369  1.1892            11.3029 0.0000       0
KYNU_6371            6370  1.6818             9.9690 0.0000       0
TF_13505            13504  3.2237             5.4590 0.0000       0
ALDH5A1_332           331  4.6058             4.4151 0.0000       0
FAM107B_3938         3937  4.9492             4.3848 0.0020       0
LOC643031_7455       7454  7.3104             3.8425 0.0017       0
</pre>

<pre class="brush: bash; title: ; notranslate" title="">library(lima)
design &lt;- cbind(ctl=1,KDvsCtl=c(0,0,1,1))
fit &lt;- lmFit(log2(data),design) #limFit needs log transformed data
fit &lt;- eBayes(fit)
fitTT &lt;- topTable(fit,coef="KDvsCtl" ,adjust.method="BH",num=Inf) #num=Inf means output all genes
fitTT$sig &lt;- fitTT$adj.P.Val&lt;0.05
fitTT$P.Value &lt;- -log10(fitTT$P.Value)
write.table(fitTT,file="Result", quote=F, sep="\t",row.names=F,col.names=T)
#logFC &gt; 0 means gene upregulated in Mu cells
head(fitTT,5)
              ID     logFC  AveExpr         t  P.Value   adj.P.Val        B
6369   KYNU_6370 -3.496799 7.289008 -34.07340 7.141460 0.001116004 8.042680
5811 IFITM3_5812  2.890454 8.352838  28.79580 6.722458 0.001420670 7.503120
6370   KYNU_6371 -3.315112 6.344728 -26.96924 6.559511 0.001420670 7.267837
6506  LITAF_6507  2.392265 7.350691  25.45207 6.415663 0.001451375 7.048397
2602   CNN3_2603  2.911140 6.547313  24.57275 6.328375 0.001451375 6.909944
      sig
6369 TRUE
5811 TRUE
6370 TRUE
6506 TRUE
2602 TRUE

</pre>