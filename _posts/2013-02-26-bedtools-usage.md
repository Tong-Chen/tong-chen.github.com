---
title: Tips for bedtools usage
layout: post
categories:
  - seq
  - NGS
  - letter
tags:
  - NGS
  - seq
---

1.交集，计算reads或peak分布

{% highlight bash %}
#gene.bed为标准的6列bed文件，其名字位于输出结果的第10列。bam文件所代表的bed的名字在输出结果的第4列
#-f 只对-a/-abam后的文件有效，所以intersectBed的两个输入文件位置不可对掉
#因为是RNA-Seq，所以使用-split参数
#-g group -c opcols -o ops
intersectBed -abam mapped.bam -b gene.bed -bed -wb -f 0.5 -split ｜ cut -f 4,16 | sort -k16 | \
groupBy -i - -g 2 -c 1 -o collapse >gene.reads.groupBy
#如果intersectBed的两个文件都用 sort -k1,1 -k2,2n 排序过，可以加上-sorted 参数
intersectBed -abam mapped.bam -b gene.bed -bed -wb -f 0.5 -split -sorted ｜ cut -f 4,16 | sort -k16 | \
groupBy -i - -g 2 -c 1 -o collapse >gene.reads.groupBy

{% endhighlight %}

2.覆盖度，区间内的read计数或区间的RPKM

{% highlight bash %}
#coverageBed的输出为在原有bed文件的每行后面增加四列，
#第一列是与-b后的文件每个区间重叠的-abam文件的特征的个数（reads数）。 6+1
#第二列是-b后的文件每个区间覆盖度不为0的碱基数目。                    6+2
#第三列是-b文件每个区间的长度                                         6+3
#第四列是第二列除以第三列                                             6+4
coverageBed -split -abam mapped.bam -b gene.bed | cut -f 4,7,9 | awk 'BEGIN{OFS="\t";FS="\t"}{print $1,10^9*$2/$3/total_reads)}' >file
coverageBed -counts -split -abam mapped.bam -b gene.bed | cut -f 4,7,9 >file

{% endhighlight %}

3. Test the computational mode of intersectBed

When you use `intersecBed` only with -a and -b, it will output the overlapped regions for bins in the first bed file. But what would happen if the bins in the first bed file can match to multiple bins in the second file? `intersectBed` will compare each bin in the first bed to all bins in the second bed nd output overlapped regions for each pair if they have.

{% highlight bash %}
#Test the output and the compotational mode of intersectBed
#Given two bed files
$ cat test1.bed
chr1	0	1000	1_a
chr1	500	2000	1_b
chr2	3000	4000	1_c
$ cat test2.bed
chr1	0	800	2_a
chr1	500	1000	2_b
chr2	3800	4000	2_c
chr2	3500	4000	2_d
chr2	3000	4000	2_e
$ intersectBed -a test1.bed -b test2.bed
chr1	0	800	1_a #1_a is compared with 2_a and 2_b and get two overlapped regions
chr1	500	1000	1_a
chr1	500	800	1_b
chr1	500	1000	1_b
chr2	3800	4000	1_c #1_c is compared with 2_c, 2_d and 2_e.
chr2	3500	4000	1_c
chr2	3000	4000	1_c
{% endhighlight %}
