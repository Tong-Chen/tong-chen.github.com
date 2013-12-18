---
title: Records for useful commands in bioinformatics analysis
author: 悟道
layout: post
categories:
  - seq
  - NGS
  - letter
tags:
  - seq
  - NGS
---

The post collects my daily used commands or scripts in bioinformatics analysis especially focusing on next generation sequencing.


#### File format transfer
#####Bed to GTF or Gff

I usually use this online tool, [`bedToGtf`](http://genepattern.broadinstitute.org/gp/pages/index.jsf).

Still, there are several ways to do this which I have not tested.

* [scripture](http://www.broadinstitute.org/software/scripture/)

{% highlight bash %}
java -Xmx1000m -jar <path_to_scripture>/scripture_alpha2.jar -task toGFF -cufflinks -in your_file.bed -source SCRIPTURE -out your_file.gtf
{% endhighlight %}

* bedToGenePred

{% highlight bash %}
bedToGenePred input.bed stdout | genePredToGtf file stdin output.gtf
{% endhighlight %}

* one-line script

{% highlight bash %}
awk '{print $1"\t"$7"\t"$8"\t"($2+1)"\t"$3"\t"$5"\t"$6"\t"$9"\t"(substr($0, index($0,$10)))}' foo.bed > bed.gtf # one easy command to generate gtf
{% endhighlight %}


##### Gtf to bed

* gtf2bed from [bedops](https://bedops.readthedocs.org/en/latest/content/reference/file-management/conversion/gtf2bed.html)

{% highlight bash %}
# (< a file) simply means read in the file
$ gtf2bed < foo.gtf | sort-bed - > foo.bed 
{% endhighlight %}

* gtf2bed.pl from [clipper](http://code.google.com/p/ea-utils/source/browse/trunk/clipper/gtf2bed)

{% highlight bash %}
 $ perl gtf2bed.pl input.gtf > output.bed 
{% endhighlight %}

* If you want to get the 5'UTR, CDS, 3'UTR, start-codon and stop codon separately, I recommend use my own script [parseGTF.py](https://github.com/Tong-Chen/NGS/blob/master/parseGTF.py) and [sortGTF.py](https://github.com/Tong-Chen/NGS/blob/master/sortGTF.py). Please see detailed usage for this script in [parseGTF](http://tianxia-world.tk/2013/03/parsegtf-py/).

{% highlight bash %}
sortGTF.py gtf-file >sorted.gtf-file
parseGTF.py sorted.gtf-file chrom-sizes-file >gtf.bed
{% endhighlight %}

* GTF to Bed12 (use [UCSC tools](http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/))
{% highlight bash %}
gtfToGenePred mm9.gtf stdout | genePredToBed stdin mm9.bed12
{% endhighlight %}

#### Sequence extraction
* Extract FATSA sequence for `gtf` file
    * gffread from [cufflinks](http://cufflinks.cbcb.umd.edu/gff.html)  

{% highlight bash %}
gffread -w output.fa -g gename_assembl.fa refgene.gtf
{% endhighlight %}

* Extract FATSA sequence for `bed` file
    * I recmmend my script [seqExtract.3.py](https://github.com/Tong-Chen/NGS/blob/master/seqExtract.3.py) 

{% highlight bash %}
seqExtract.3.py -i genome.fa -b "bed1,bed2..."
{% endhighlight %}
 	
