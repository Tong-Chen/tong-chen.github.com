---
title: fastaq格式
author: 悟道
layout: post
permalink: /?p=1563
categories:
  - seq
tags:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

Fastq格式是用来保存第二代测序数据的格式，其中同时包含了测序序列与测序质量，而且序列本身和测序质量都以单个的ASCII字符来表示。Fastq没有标准的后缀名，一般使用“.fq”或者“.fastq”，当然，“.txt”亦可。

Fastq格式一般包含四行：第一行以“@”起始，后跟相应的描述信息（类似于Fasta格式）；第二行是序列本身；第三行由“+”起始，后面的描述信息可有可无，若有的话，则与第一行中的完全一样；第四行是第二行测序序列的测序质量，字符数与第二行相等。

Fastq格式示例如下：

> @SEQ_ID  
> GATTTGGGGTTCAAAGCAGTATCG<wbr>ATCAAATAGTAAATCCATTTGTTC<wbr>AACTCACAGTTT  
> +  
> !&#8221;\*((((\*\*\*+))%%%++)(%%%%).1\*\*\*-+\*&#8221;))**55CCF>>>>>>CCCCCCC65</wbr></wbr>

上面讲的是常见的（单端测序的）Fastq格式，对于双端测序，还应注意以下几点：  
1. 双端测序一般有两个文件（也可通过某种规则把两个文件合并成一个）。  
2. 第一个文件与第二个文件的行数完全一样，且测序序列的排列顺序完全一致。  
3. 在第一个文件中，描述信息的结尾是“/1”，表示是双端测序的一端；第二个文件中同样位置/行数的相对应的测序序列的描述信息则以“/2”结尾，表示是双端测序的另一端。

双端测序的Fastq格式示例：

@SRR372739.1 B2GA001:1:2:1039:1169**/1**  
NACATGAAAAGATGTTTAACGTTGGAATGTATATNG  
+  
#\*\*(()\*\*&#8221;:-78:AA7AAAAA#############

@SRR372739.1 B2GA001:1:2:1039:1169**/2**  
GCAGAAACTNAACTAATAAAGTTGGAATGTNTNTCG  
+  
BB?BB:96<#>>9>>BB@BBABB:A###########

&nbsp;

引用并修改自： http://blog.sina.com.cn/s/blog_5d1edf6a0100u87d.html

其它参考：http://en.wikipedia.org/wiki/FASTQ_format

http://maq.sourceforge.net/fastq.shtml

&nbsp;