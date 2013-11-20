---
title: R语言biomaRt包访问Ensemble,Uniprot,NCBI,EBI,TAIR
author: 悟道
layout: post
permalink: /?p=640
categories:
  - bioinformatics
  - R
tags:
  - bioinformatics
  - R
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

Ensemle的biomart工具可以帮助我们批量提取想要的注释信息和不同数据库序列编号之间的转换，给我们提供了极大的方便，而且ensemble网站提供了Perl的API接口， 对于不习惯使用perl的人， 应该如何操作才能让自己的工作更有效率呢？

这里我们推荐R语言的包biomaRT来帮助你完成这个任务。

这是一个关于biomaRt包的描述，可参考网站<http://rss.acs.unt.edu/Rdoc/library/biomaRt/DESCRIPTION>  
Package: biomaRt  
Version: 1.10.0  
Title: Interface to BioMart databases (e.g. Ensembl, Wormbase, Gramene  
and Uniprot)  
Author: Steffen Durinck <durincks@mail.nih.gov>, Wolfgang Huber  
<huber@ebi.ac.uk>, Sean Davis <sdavis2@mail.nih.gov>  
Maintainer: Steffen Durinck <durincks@mail.nih.gov>  
Depends: methods, XML, RCurl  
Suggests: annotate  
biocViews: Annotation  
Description: The package provides an API in R to query BioMart  
databases such as Ensembl (http://www.ensembl.org), a software  
system which produces and maintains automatic annotation on  
metazoan genomes.  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

下面介绍下如何使用。

首先下载并安装 <http://bioconductor.org/packages/release/bioc/html/biomaRt.html>

或参见<http://210.75.224.29/wordpress/?p=390>

[][1]

我用一个例子来演示如何使用这个包。

<div class="wp_codebox">
  <table>
    <tr id="p64040">
      <td class="line_numbers">
        <pre>1
2
3
4
5
6
7
8
9
10
</pre>
      </td>
      
      <td class="code" id="p640code40">
        <pre class="r" style="font-family:monospace;">library(biomaRt)
&nbsp;
plant=useMart("plant_mart_7")
alythia=useDataset("alyrata_eg_gene", mart=plant)
id=read.table("locus")
id=as.vector(id$V1)
&nbsp;
attributes=c('ensembl_peptide_id', 'description','go_biological_process_id','name_1006','go_cellular_component_id','go_cellular_component__dm_name_1006', 'go_molecular_function_id', 'go_molecular_function__dm_name_1006','interpro','interpro_description')
result=getBM(attributes=attributes, filters="ensembl_peptide_id", values=id, mart=alythia)
write.table(result, file="alyrataAnno", quote=FALSE, row.names=FALSE, sep='\t')</pre>
      </td>
    </tr>
  </table>
</div>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
下面来解释每行的意思和主意事项， 最后提供mart、attribute和filter列表以供参考。

首先调用包 ** >>>library(biomaRT)**

选择需要的数据库mart **>>>plant=useMart(&#8220;plant\_mart\_7&#8243;)**

如何知道都支持哪些数据库mart和对应的版本呢？ 可以使用函数listMarts()

**>>>listMarts()**

biomart version  
ensembl ENSEMBL GENES 60 (SANGER UK)  
snp ENSEMBL VARIATION 60 (SANGER UK)  
functional_genomics ENSEMBL FUNCTIONAL GENOMICS 60 (SANGER UK)  
vega VEGA 40 (SANGER UK)  
bacterial\_mart\_7 ENSEMBL BACTERIA 7 (EBI UK)  
fungal\_mart\_7 ENSEMBL FUNGAL 7 (EBI UK)  
metazoa\_mart\_7 ENSEMBL METAZOA 7 (EBI UK)  
plant\_mart\_7 ENSEMBL PLANT 7 (EBI UK)  
（这里截取了部分，自己可以利用write.table()来存储）  
**>>>lm=listMarts()**  
得到的lm是一个列表，可以使用lm[1]和lm[2]访问每一列的内容，同时可以使用lm[[1]]访问每个分量的内容。

选好数据库之后就要选择想要使用的数据集，  
**>>>alythia=useDataset(&#8220;alyrata\_eg\_gene&#8221;, mart=plant)**

同样的我们可以利用listDatasets()函数获得当前数据库下的数据集>>>listDatasets(plant)  
**  
>>>listDatasets(plant)**

dataset description  
1 sbicolor\_eg\_gene Sorghum bicolor genes (Sbi1)  
2 bdistachyon\_eg\_gene Brachypodium distachyon genes (Brachy1.0)  
3 alyrata\_eg\_gene Arabidopsis lyrata genes (Araly1)  
4 oindica\_eg\_gene Oryza sativa indica group genes (2005-01-BGI)  
5 ptrichocarpa\_eg\_gene Populus trichocarpa genes (JGI2.0)  
6 vvinifera\_eg\_gene Vitis vinifera genes (IGGP_12x)  
（这里截取了部分，自己可以利用write.table()来存储）

这样我们就可以选择合适的filter和attribute来进行操作了，开始之前，我们仍然需要用listFilters(alythia)和listAttributes(alythia)来查找当前可以利用的filters和attributes。

提取属性，我们需要用到getBM函数，其原型为：[getBM][2](attributes, filters = &#8220;&#8221;, values = &#8220;&#8221;, mart, curl = NULL, output = &#8220;data.frame&#8221;, list.names = NULL, na.value = NA, checkFilters = TRUE, verbose = FALSE)  
【attributes和values的类型为字符向量】  
我们需要设定属性值  
**>>>attributes=c(attributes=c(&#8216;ensembl\_peptide\_id&#8217;, &#8216;description&#8217;,'go\_biological\_process\_id&#8217;,'name\_1006&#8242;,&#8217;interpro_description&#8217;)  
)**  
设定过滤变量**>>>filters=&#8221;ensembl\_peptide\_id&#8221;**  
(如果我们想获得全基因组获全蛋白质组的数据，我们可以不指定filters，直接使用  
**result=getBM(attributes=attributes, mart=alythia))**

设定了filter，就要给出filter的取值，如果设定了多个filter，则需指定多组值。  
可以通过**>>>id=c(&#8220;Al\_scaffold\_0001\_1000&#8243;,&#8221;Al\_scaffold\_0001\_1004&#8243;)**来给定你选择的id，  
或者从文件中读入,，但是需要把数据框转换称字符向量。  
>>>**id=read.table(&#8220;locus&#8221;)**  
>>>**id=as.vector(id$V1)**

到现在可以提去想要的东西了  
>>>**result=getBM(attributes=attributes, filters=filters, values=id, mart=alythia)**

把结果存储下来  
>>>**write.table(result, file=&#8221;alyrataAnno&#8221;, quote=FALSE, row.names=FALSE, sep=&#8217;\t&#8217;)**

任务完成:)  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

其它参考资料：  
<http://blog.csdn.net/jiuyizhizhu/archive/2010/06/05/5649834.aspx>  
biomart参考手册

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;更新 2011-06-26&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

由于biomart数据库的更新和改动，前述脚本对于植物不能正常工作，现在再更新一个鲁棒性稍好些的脚本，随着问题的发现和解决，也会持续更新。

<div class="wp_codebox">
  <table>
    <tr id="p64041">
      <td class="code" id="p640code41">
        <pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">#!/bin/bash</span>
&nbsp;
<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #000000;">1</span><span style="color: #000000; font-weight: bold;">&gt;&</span><span style="color: #000000;">2</span> <span style="color: #ff0000;">"If you are not sure about the parameters, first run <span style="color: #000099; font-weight: bold;">\
</span>biomartAnnoPre.sh and follow the steps given"</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">test</span> <span style="color: #007800;">$#</span> <span style="color: #660033;">-lt</span> <span style="color: #000000;">3</span>; <span style="color: #000000; font-weight: bold;">then</span>
	<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #000000;">1</span><span style="color: #000000; font-weight: bold;">&gt;&</span><span style="color: #000000;">2</span> <span style="color: #ff0000;">"Usage $0 locusName animal[plant] dataset [annoOutput]"</span>
	<span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span>
<span style="color: #000000; font-weight: bold;">fi</span>
&nbsp;
<span style="color: #007800;">locusName</span>=<span style="color: #007800;">$1</span>
<span style="color: #007800;">specie</span>=<span style="color: #007800;">$2</span>
<span style="color: #007800;">dataset</span>=<span style="color: #007800;">$3</span>
<span style="color: #666666; font-style: italic;">#这里如此处理是为了配合split和cat的使用。因为当数据过大时，会被ensembl踢掉，需要拆分成小的数据集来抓取</span>
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">test</span> <span style="color: #007800;">$#</span> <span style="color: #660033;">-eq</span> <span style="color: #000000;">3</span>; <span style="color: #000000; font-weight: bold;">then</span>
	<span style="color: #007800;">file</span>=<span style="color: #007800;">$locusName</span>.Anno
<span style="color: #000000; font-weight: bold;">else</span>
	<span style="color: #007800;">file</span>=<span style="color: #007800;">$4</span>
<span style="color: #000000; font-weight: bold;">fi</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">test</span> <span style="color: #007800;">$specie</span> == <span style="color: #ff0000;">'animal'</span>; <span style="color: #000000; font-weight: bold;">then</span>
	<span style="color: #007800;">martindex</span>=<span style="color: #000000;">1</span>
<span style="color: #000000; font-weight: bold;">elif</span> <span style="color: #7a0874; font-weight: bold;">test</span> <span style="color: #007800;">$specie</span> == <span style="color: #ff0000;">'plant'</span>;<span style="color: #000000; font-weight: bold;">then</span>
	<span style="color: #007800;">martindex</span>=<span style="color: #000000;">10</span>
<span style="color: #000000; font-weight: bold;">else</span>
	<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #000000;">1</span><span style="color: #000000; font-weight: bold;">&gt;&</span><span style="color: #000000;">2</span> <span style="color: #ff0000;">"Wrong parameter, should be either &lt;animal&gt; or &lt;plant&gt;"</span>
	<span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span>
<span style="color: #000000; font-weight: bold;">fi</span>
&nbsp;
<span style="color: #c20cb9; font-weight: bold;">cat</span> <span style="color: #000000; font-weight: bold;">&lt;&lt;</span>END <span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #007800;">$file</span>.r
library<span style="color: #7a0874; font-weight: bold;">&#40;</span>biomaRt<span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #007800;">mart_choose</span>=as.matrix<span style="color: #7a0874; font-weight: bold;">&#40;</span>listMarts<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #007800;">$martindex</span>,<span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#93;</span>
<span style="color: #007800;">ctmart</span>=useMart<span style="color: #7a0874; font-weight: bold;">&#40;</span>mart_choose<span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #007800;">ctdataset</span>=useDataset<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">$dataset</span>"</span>, <span style="color: #007800;">mart</span>=ctmart<span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #666666; font-style: italic;">#attri = listAttributes(ctdataset)</span>
<span style="color: #666666; font-style: italic;">#attri_index=c(3,5, 24, 25, 26, 28, 29, 30,66, 68, 63)</span>
<span style="color: #666666; font-style: italic;">#ct_attri=attri[attri_index, 1]</span>
<span style="color: #666666; font-style: italic;">#采用上面被注释掉的三行鲁棒性可能会更强，但是listAttributes()改变之后，结果可能不是想要的，这里采取了保守的方式，若属性不存在即会提示错误。</span>
<span style="color: #007800;">ct_attri</span>=c<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"ensembl_peptide_id"</span>, <span style="color: #ff0000;">"description"</span>,<span style="color: #ff0000;">"go_id"</span>,<span style="color: #ff0000;">"name_1006"</span>,<span style="color: #ff0000;">"definition_1006"</span>, <span style="color: #ff0000;">"namespace_1003"</span>, <span style="color: #ff0000;">"goslim_goa_accession"</span>,<span style="color: #ff0000;">"goslim_goa_description"</span>, <span style="color: #ff0000;">"interpro"</span>, <span style="color: #ff0000;">"interpro_description"</span>, <span style="color: #ff0000;">"pfam"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #c20cb9; font-weight: bold;">id</span> = read.table<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">$locusName</span>"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #007800;">id</span>=as.vector<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #c20cb9; font-weight: bold;">id</span>\<span style="color: #007800;">$V1</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #007800;">result</span>=getBM<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">attributes</span>=ct_attri, <span style="color: #007800;">filters</span>=<span style="color: #ff0000;">"ensembl_peptide_id"</span>, <span style="color: #007800;">values</span>=<span style="color: #c20cb9; font-weight: bold;">id</span>, <span style="color: #007800;">mart</span>=ctdataset<span style="color: #7a0874; font-weight: bold;">&#41;</span>
write.table<span style="color: #7a0874; font-weight: bold;">&#40;</span>result,<span style="color: #007800;">file</span>=<span style="color: #ff0000;">"<span style="color: #007800;">$file</span>"</span>,<span style="color: #007800;">quote</span>=FALSE,row.name=FALSE,<span style="color: #007800;">sep</span>=<span style="color: #ff0000;">'\t'</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
END
&nbsp;
Rscript <span style="color: #007800;">$file</span>.r</pre>
      </td>
    </tr>
  </table>
</div>

 [1]: http://210.75.224.29/wordpress/?p=390
 [2]: http://rss.acs.unt.edu/Rdoc/library/biomaRt/html/getBM.html