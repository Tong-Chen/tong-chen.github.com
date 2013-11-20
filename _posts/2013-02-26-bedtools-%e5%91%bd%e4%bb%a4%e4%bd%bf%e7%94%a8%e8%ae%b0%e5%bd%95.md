---
title: bedtools 命令使用记录
author: 悟道
layout: post
permalink: /?p=2905
categories:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.交集，计算reads或peak分布

<pre class="brush: bash; title: ; notranslate" title="">#gene.bed为标准的6列bed文件，其名字位于输出结果的第10列。bam文件所代表的bed的名字在输出结果的第4列
#-f 只对-a/-abam后的文件有效，所以intersectBed的两个输入文件位置不可对掉
#因为是RNA-Seq，所以使用-split参数
#-g group -c opcols -o ops
intersectBed -abam mapped.bam -b gene.bed -bed -wb -f 0.5 -split ｜ cut -f 4,16 | sort -k16 | \
groupBy -i - -g 2 -c 1 -o collapse &gt;gene.reads.groupBy
#如果intersectBed的两个文件都用 sort -k1,1 -k2,2n 排序过，可以加上-sorted 参数
intersectBed -abam mapped.bam -b gene.bed -bed -wb -f 0.5 -split -sorted ｜ cut -f 4,16 | sort -k16 | \
groupBy -i - -g 2 -c 1 -o collapse &gt;gene.reads.groupBy
</pre>

2.覆盖度，区间内的read计数或区间的RPKM

<pre class="brush: bash; title: ; notranslate" title="">#coverageBed的输出为在原有bed文件的每行后面增加四列，
#第一列是与-b后的文件每个区间重叠的-abam文件的特征的个数（reads数）。 6+1
#第二列是-b后的文件每个区间覆盖度不为0的碱基数目。                    6+2
#第三列是-b文件每个区间的长度                                         6+3
#第四列是第二列除以第三列                                             6+4
coverageBed -split -abam mapped.bam -b gene.bed | cut -f 4,7,9 | awk 'BEGIN{OFS="\t";FS="\t"}{print $1,10^9*$2/$3/total_reads)}' &gt;file
coverageBed -counts -split -abam mapped.bam -b gene.bed | cut -f 4,7,9 &gt;file
</pre>

3.