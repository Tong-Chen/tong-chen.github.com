---
title: graphviz使用
author: 悟道
layout: post
permalink: /?p=1947
categories:
  - graphviz
tags:
  - graphviz
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

出图命令：

> dot -Tpng exm.dot >exm.png

1.First example:

> digraph G {  
> {node [color=lightblue, style=filled]; &#8220;Conservation&#8221;; &#8220;Binding specificity&#8221;; &#8220;Function in iPS&#8221;;}  
> {node [color=lightgrey, style=filled]; &#8220;Overexpression&#8221;; &#8220;Other work&#8221;}  
> {node [shape=diamond, color=lightgrey, style=filled]; &#8220;Phenotype changes&#8221;;}  
> &#8220;FoxP1&#8243; -> &#8220;Identify isoforms&#8221;;  
> &#8220;Identify isoforms&#8221; -> &#8220;Make sure expression differences&#8221;;  
> &#8220;Make sure expression differences&#8221; -> &#8220;Conservation&#8221;  
> &#8220;Make sure expression differences&#8221; -> &#8220;Binding specificity&#8221; ;  
> &#8220;Make sure expression differences&#8221; -> &#8220;Knock down&#8221; ;  
> &#8220;Make sure expression differences&#8221; -> &#8220;Overexpression&#8221; ;  
> &#8220;Overexpression&#8221; -> &#8220;Phenotype changes&#8221;  
> &#8220;Knock down&#8221; -> &#8220;Phenotype changes&#8221;  
> &#8220;Phenotype changes&#8221; -> &#8220;Other work&#8221; [label="N"];  
> &#8220;Phenotype changes&#8221; -> &#8220;RNA-Seq&#8221; [label="Y"];  
> &#8220;Phenotype changes&#8221; -> &#8220;Chip-Seq&#8221; [label="Y"];  
> &#8220;RNA-Seq&#8221; -> &#8220;Functional analysis&#8221; ;  
> &#8220;Chip-Seq&#8221; -> &#8220;Functional analysis&#8221; ;  
> &#8220;Functional analysis&#8221; -> &#8220;Function in ES&#8221;;  
> &#8220;Functional analysis&#8221; -> &#8220;Function in iPS&#8221;;  
> &#8220;Binding specificity&#8221; -> &#8220;Chip-Seq&#8221; [label="Y"];  
> /* &#8220;Conservation&#8221; -> &#8220;Functional analysis&#8221;[label="needed"];  
> &#8220;Conservation&#8221; -> &#8220;More important&#8221;;*/  
> FoxP1 [shape=Mdiamond];

[<img class="alignleft size-large wp-image-1950" title="flow" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/04/flow-1024x744.jpg" alt="" width="600" height="435" />][1]

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

2.Second example

> digraph G {  
> subgraph cluster_0 {  
> style=filled;  
> color=lightgrey;  
> node [style=filled, color=white];  
> &#8220;Quality estimate&#8221;->&#8221;Mapping&#8221;->&#8221;Filter&#8221;->&#8221;Peak calling&#8221;->&#8221;Peak a nnotation&#8221;->&#8221;Differential analysis&#8221;->&#8221;&#8230;&#8221;;  
> label=&#8221;Flow&#8221;;  
> }
> 
> subgraph cluster_1 {  
> node [style=filled];  
> FastQC->Bwa->Samtools->Macs->Ceas->Scripts->&#8221;&#8230;&#8230;&#8221;;  
> label = &#8220;Tools&#8221;;  
> color=blue;  
> }  
> Reads -> &#8220;Quality estimate&#8221;;  
> Reads -> &#8220;FastQC&#8221;;  
> Reads [shape=Mdiamond];  
> //Quality estimate &#8212; FastQC  
> }
> 
> }

[<img class="size-full wp-image-1951 alignnone" title="chip.analysis.flow" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/04/chip.analysis.flow_.png" alt="" width="525" height="800" />][2]

&nbsp;

3.Third example

4.Forth example

 [1]: http://210.75.224.29/wordpress/wp-content/uploads/2012/04/flow.jpg
 [2]: http://210.75.224.29/wordpress/wp-content/uploads/2012/04/chip.analysis.flow_.png