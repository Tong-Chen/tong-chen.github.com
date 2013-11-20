---
title: RNA-Seq
author: 悟道
layout: post
permalink: /?p=1925
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

# Quality control

见[Next Generation Sequencing Analysis &#8211; ChIP-Seq][1]

Reads trimming

>     fastx_trimmer -f 1 -l 25 -z -o sequence.trim.fastq.gz -Q33 [http://seqanswers.com/forums/showthread.php?t=7596]
>     fastx_clipper -a 'ACTGTAGGCACCATCAATC' -i test.fq -Q 33 -n
>     fastq_quality_trimmer -i m6a_P16.clipped.delN.fq -o m6a_P16.clipped.delN.trimq20.fq -t 20 -l 30 -v -Q 33

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

## `Duplicates and multiple hits`

    http://seqanswers.com/forums/showthread.php?t=6854
    http://davetang.org/muse/2012/05/25/how-to-deal-with-multi-mapping-tags/

# Get GTF file for tophat

http://genomewiki.ucsc.edu/index.php/Genes\_in\_gtf\_or\_gff_format

<http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/>

> <pre>$ cat $HOME/.hg.conf
db.host=genome-mysql.cse.ucsc.edu
db.user=genomep
db.password=password
$ chmod 600 .hg.conf
$ genePredToGtf hg19 knownGene knownGene.gtf
$ genePredToGtf mm9 refGene stdout | sort -k1,1 -k4,4n &gt; mm9.db.refGene.gtf</pre>

# 

# Reads mapping

<http://www.nature.com/nprot/journal/v7/n3/full/nprot.2012.016.html>

## Tophat

<http://tophat.cbcb.umd.edu/index.html>

直接下载二进制版本，解压即可运行

>  tophat -o ./ -r 20 <tt>--solexa1.3-quals</tt> -p 8 -g 60 <tt>--library-type</tt>=fr-unstranded \
> 
> -G $(trans) &#8211;transcriptome-index $(transIndex) \
> 
> &#8211;max-multihits 10  &#8211;coverage-search \  
> &#8211;microexon-search index read\_1.fastq read\_2.fastq
> 
> -r: reprsents the gap between mate reads. If the length of your fragment is 200bp, where each end is 90bp, -r is 200 &#8211; 90-90 = 20
> 
> -mate-std-dev default 20
> 
> <tt>--solexa1.3-quals</tt>: Use this option for FASTQ files from pipeline 1.3 or later.
> 
> -p number of threads
> 
> -G mm9.db.refGene.gtf
> 
> &#8211;transcriptome-index directory-to-save-transcriptiom-index-file-for-following-run
> 
> &#8211;library-type
> 
> If you don&#8217;t specify &#8211;library-type, TopHat just treats your reads as  
> unstranded. (The default is \*unstranded\*). Actually, library-type is only intended for paired-end, so if you specify the library-type fr-unstranded option, should be the same as non-specified. [http://seqanswers.com/forums/showpost.php?p=41795&postcount=9]
> 
> &#8211;max-multihits The maximum outputted map loci of each read. using **-g 1** to get unique mapped reads.
> 
> -g 20 defaults bowtie2 use -k 41.
> 
> -g 1 bowtie2 use -k 11

## Result of tophat:

1.255 is for what TopHat considers unique mappings, 3 for mappings with one additional alignment, 1 for 4-9 alignments, 0 for 10+ alignments. [Tophat1 bowtie1] {http://seqanswers.com/forums/showthread.php?t=2629}

2.50 is for what TopHat considers unique mappings, 1 for mappings with 3 alignments, 3 for two, 0 for many.

3.Consider NH tags for the number of hits. So remember to check this tag.

4.One possible way is to define a read as being uniquely mapped if the best two alignments have identical number of differences (mismatches plus gaps). [http://lh3lh3.users.sourceforge.net/mapuniq.shtml]

##  Correct Tophat output

> It&#8217;s been noticed that the current Tophat (v2.0.3) can assign wrong XS:A tag for strand-specific paired-end library, at least for some reads. Here is such an example:
> 
> HWI-ST560:74:D14ELACXX:4:1201:8827:168386 pr1 chr1 10024104 50 50M = 10020756 -3398 TGGTTCTTGAAACTGCTGGTTCAGCATCTGTGTACTAACATCAATCCCGG IJJJJJJJIIIGJJJJJJJJJJJJJJJJJJJJIJJJJHHHHHFFFFFCCC AS:i:0 XN:i:0 XM:i:0 XO:i:0 XG:i:0 NM:i:0 MD:Z:50 YT:Z:UU NH:i:1 XS:A:+  
> HWI-ST560:74:D14ELACXX:4:1201:8827:168386 pR2 chr1 10020756 50 36M1628N14M = 10024104 3398 GATGATTTGAAATATGAGACTTCTAAGGCATAATATTGTTTGCAGTGCAC CCCFFFFFHHHHHJJJJJJJJJJJJJJJJJJJJIIIIJJJJIJIJHJGEC AS:i:0 XM:i:0 XO:i:0 XG:i:0 MD:Z:50 NM:i:0 XS:A:- NH:i:1
> 
> This is a dUTP protocol where &#8220;R2/r1&#8243; FLAG for the read pair indicate the reads are a transcript on the + strand, which means both reads should be assigned as XS:A:+. However /2 is assigned to XS:A:-.
> 
> I&#8217;ve written an awk script to solve the problem:
> 
> <div>
>   #!/bin/awk -f
> </div>
> 
> <div>
>
> </div>
> 
> <div>
>   BEGIN{
> </div>
> 
> <div>
>       if(save_discrepancy_to_file!=&#8221;") system(&#8220;[ -e " save_discrepancy_to_file " ] && rm &#8221; save_discrepancy_to_file);
> </div>
> 
> <div>
>   }
> </div>
> 
> <div>
>   {
> </div>
> 
> <div>
>       if($1 ~ /^@/) print;
> </div>
> 
> <div>
>       else
> </div>
> 
> <div>
>       {
> </div>
> 
> <div>
>           for(i=1;i<=NF;i++) if($i!~/^XS/) printf(&#8220;%s\t&#8221;,$i); else XS0=$i;
> </div>
> 
> <div>
>           XS1=XS0;
> </div>
> 
> <div>
>           if($2~/^0x/ || $2~/^[0-9]+$/){   # FLAG in HEX or Decimal format
> </div>
> 
> <div>
>               if(libtype==&#8221;fr-firststrand&#8221;) XS1=((and($2, 0&#215;10) && and($2, 0&#215;40)) || (and($2,0&#215;80) && !and($2,0&#215;10)))?&#8221;XS:A:+&#8221;:&#8221;XS:A:-&#8221;;
> </div>
> 
> <div>
>               if(libtype==&#8221;fr-secondstrand&#8221;) XS1=((and($2, 0&#215;10) && and($2, 0&#215;80)) || (and($2,0&#215;40) && !and($2,0&#215;10)))?&#8221;XS:A:+&#8221;:&#8221;XS:A:-&#8221;;
> </div>
> 
> <div>
>           }
> </div>
> 
> <div>
>           else if($2~/^[:alpha:]/){   # FLAG in string
> </div>
> 
> <div>
>               if(libtype==&#8221;fr-firststrand&#8221;) XS1=($2~/r.*1/ || ($2~/2/ && $2!~/r/))?&#8221;XS:A:+&#8221;:&#8221;XS:A:-&#8221;;
> </div>
> 
> <div>
>               if(libtype==&#8221;fr-secondstrand&#8221;) XS1=($2~/r.*2/|| ($2~/1/ && $2!~/r/))?&#8221;XS:A:+&#8221;:&#8221;XS:A:-&#8221;;
> </div>
> 
> <div>
>           }
> </div>
> 
> <div>
>           print XS1;
> </div>
> 
> <div>
>
> </div>
> 
> <div>
>           if(save_discrepancy_to_file!=&#8221;" && XS1!=XS0) print >> save_discrepancy_to_file;
> </div>
> 
> <div>
>       }
> </div>
> 
> <div>
>   }
> </div>

## Parse tophat output

1.samtools view -c -f 0&#215;2 accepted_hits.bam  #get the number of proper paired reads

samtools view -F 0&#215;2 accepted_hits.bam #get properly paired reads

2.**samtools flagstat accepted_hits.bam **

102925213 + 0 in total (QC-passed reads + QC-failed reads)

0 + 0 duplicates 102925213 + 0 mapped (100.00%:nan%)

102925213 + 0 paired in sequencing

51854282 + 0 read1

51070931 + 0 read2

65032742 + 0 properly paired (63.18%:nan%)

96061406 + 0 with itself and mate mapped

6863807 + 0 singletons (6.67%:nan%)

0 + 0 with mate mapped to a different chr

0 + 0 with mate mapped to a different chr (mapQ>=5)

> p=0&#215;1 (paired),
> 
> P=0&#215;2 (properly paired),
> 
> u=0&#215;4 (unmapped),  
> U=0&#215;8 (mate unmapped),
> 
> r=0&#215;10 (reverse),
> 
> R=0&#215;20 (mate reverse)  
> 1=0&#215;40 (first),
> 
> 2=0&#215;80 (second),
> 
> s=0&#215;100 (not primary), 有多个匹配位置，但不配对。  
> f=0&#215;200 (failure)
> 
> d=0&#215;400 (duplicate)

3.Get unique mapped reads (one approach, not test,http://seqanswers.com/forums/showthread.php?t=6189)

1. Run the data using tophat and allow up to 40 maps per read (default)  
2. Use a samtools feature to get rid of all mappings that are not mate paired and in a proper pair. [`samtools view -F <code>-f 0x02` -b in.bam > out.paired.bam</code>]

3. Count up how many times an individual read is in the sam file and remove all read pairs that are not mapped to a unique site, putting them in a separate &#8220;multihits&#8221; file.  
4. Keep all the uniquely mapped proper mate paired hits in a unique hits sam file.

## Cufflink

The SAM file supplied to Cufflinks **must** be sorted by reference position. If you aligned your reads with TopHat, your alignments will be properly sorted already

> cufflinks -p 8 -o ./ ./accepted_hits.bam
> 
> cufflinks -p 8 &#8211;GTF-guide $(trans) &#8211;label $(line) -o $(line)/cufout $(line)/topout/accepted_hits.bam >$(line).log 2>&1
> 
> <tt>-N/--upper-quartile-norm</tt> With this option, Cufflinks normalizes by the upper quartile of the number of fragments mapping to individual loci instead of the total number of sequenced fragments. This can improve robustness of differential expression calls for less abundant genes and transcripts. [Y]
> 
> -M specifies mask file (rRNA, etc)
> 
> <tt>--total-hits-norm</tt> With this option, Cufflinks counts all fragments, including those not compatible with any reference transcript, towards the number of mapped hits used in the FPKM denominator. This option can be combined with <tt>-N/--upper-quartile-norm</tt>. It is active by default.
> 
> &#8211;multi-read-correct Tells Cufflinks to do an initial estimation procedure to more accurately weight reads mapping to multiple locations in the genome. [Y]
> 
> <tt>--min-frags-per-transfrag <int></tt> Assembled transfrags supported by fewer than this many aligned RNA-Seq fragments are not reported. Default: 10.
> 
> <tt>-v/--verbose</tt> Print lots of status updates and other diagnostic information.

## Cuffmerge

##  Tips:

Do each sample once, get the junctions.bed file for each, convert it into TopHat&#8217;s .juncs format using the included script bed\_to\_juncs (this is an undocumented script for now), and pool all the .juncs files. Then remap each sample using the -j flag with this pooled .juncs file. This will improve your spliced alignment sensitivity, no matter how long your reads are. [<http://seqanswers.com/forums/showpost.php?p=16265&postcount=27>]

Others

## Cuff系列输出结果

### cuffcompare：

输入：transcripts.gtf 一般不用merged.gtf因为里面没有表大量

cuffcompare_corrected.combined.gtf: ；可以用来做cuffdiff的输入参数，但通常使用cuffmerge的merged.gtf  
cuffcompare\_corrected.loci和cuffcompare\_corrected.tracking 可以用来整合每个样品中的转录本在另外一个样品的对应的名字。这两个文件会列出每个样品的哪些转录本共同构成了或属于一个新的combined的转录本

sample/cufout/*.tmap: cuffcompare还会在每个样品的cufflink输出文件夹（即给定的transcripts.gtf的文件夹中）产生一个tmap文件，这个文件包含了新拼接的转录本与已知转录本的关系，来识别新的isoforms，antisense等

### cuffmerge：

merged.gtf: 是cuffdiff的输入文件，并且这里面包含所有转录本的唯一标识，以及他们与已知基因的关系代码（class code）。起初我用cuffcomapre吧merged.gtf与标准gtf相比，以求得到这个代码，后来竟然发现这个class code已然存在于merged.gtf中，可以直接使用。

## Strand-specific

1.Make sure the type of your sample. Click here <http://210.75.224.29/wordpress/?p=2577>

一般来讲，如果第一条reads总是在第二条reads的转录方向的上游，就说明这是5‘端先测的，对应于fr-secondstrand.

反之则为3’端先测的，对应于fr-firststrand.

单端测序的判定需要依靠有确定已注释转录本的junction reads，如果多个reads直接比对到正确的junction reads上，则为5‘端先测。如果多个都比对到junction reads的互补链上则为3’端先测。

对于链特异性的单端测序，如果是fr-secondstrand，map到什么链就来源于什么链。如果是fr-firststrand，map到什么链就来源于互补链。

For strand-specific data, if reads map to its source strand then use this reads. If reads map to  the complementary strand then use the reverse complementary strand of this reads.

2.check the correctness of tophat out

for fr-secondstrand, reads 2 must be after reads 1 (transcriptional orientation)

> &#8212;&#8212;&#8211;reads1&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;reads2&#8212;&#8212;&#8212;&#8212;&#8212;->+
> 
> <&#8212;&#8212;reads2&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;reads1&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;_

sam文件中flag为pPR1（0X63，99）和pPr2（0X93，147）的应该来源于正链，即XS:A:+. 从坐标上看，2数值更大。

flag为pPr1（0X53，83）和pPR2（0Xa3，163）的应该来源于负链，即XS:A:-。从坐标上看，1数值更大。

flag为r1（0X50）或R2（oXa0）的都来源于负链。 (80-95, 336-351) (160-175, 416,431)

for fr-firststrand, such as dUTP,

> > &#8212;&#8212;&#8211;reads2&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;reads1&#8212;&#8212;&#8212;&#8212;&#8212;->+
> > 
> > <&#8212;&#8212;reads1&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;reads2&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;_

flag为pPr1（0X53，83）和pPR2（0Xa3，163）的应该来源于正链，即XS:A:+。从坐标上看，1数值更大。  
sam文件中flag为pPR1（0X63，99）和pPr2（0X93，147）的应该来源于负链，即XS:A:-. 从坐标上看，2数值更大。  
flag为r1（0X50）或R2（oXa0）的都来源于正链。

flag为r的总是处于基因组坐标的最大值处，为R的总是处于基因组坐标的左侧。  
3.

## <a href="http://onetipperday.blogspot.com/2012/11/dont-trust-cufflinks-fpkm-for-short.html" target="_blank">Don&#8217;t trust Cufflinks FPKM for short genes</a>

This issue has been discussed elsewhere on this board. As Nicholas points out, RNA-Seq really isn&#8217;t reliable for very short transcripts. The reason is that all the fragments that map to these transcripts come from the &#8220;tail&#8221; of the distribution of library fragment lengths. That is, fragments that map to microRNAs are much, much shorter than most fragments in the library &#8211; by design in the RNA-Seq protocol, which size selects away very short inserts. Thus, <span style="text-decoration: underline;">Cufflinks infers that even though relatively few fragments actually mapped to the microRNAs, there were probably TONS of individual microRNA molecules in the transcriptome before all of the various size selection parts of the protocol kicked in. Cufflinks accordingly increases the FPKM of these short transcripts to compensate for the bias against short fragments in the library.</span>

This compensation was designed to improve accuracy for transcripts that are in the 500bp-1kb range &#8211; for longer transcripts, the &#8220;edge effects&#8221; due to library fragment size aren&#8217;t much of an issue. However, I wouldn&#8217;t trust FPKM values for transcripts shorter than your average fragment length. There&#8217;s really just not enough data in most standard RNA-Seq libraries to say much about small RNA abundance.  
I should also point out that other methods use this same bias correction technique (RSEM for example). As far as I&#8217;m aware, the &#8220;count-based&#8221; methods don&#8217;t, but that doesn&#8217;t mean they shouldn&#8217;t. <span style="text-decoration: underline;">Most of those methods are strictly for differential analysis, where any edge effects are assumed to be affecting each condition the same way. </span>That may or may not be the case in your data.  
In any case, the quick answer to this problem is to simply remove or ignore transcripts shorter than around 300bp from your GTF. In a future version, we will be flagging these transcripts as too short for reliable quantification where appropriate.

## DE analysis pipeline

Steps involved on RNA-seq analysis for detecting differential expression  
• Experimental design  
• Preprocess  
– Split by barcodes  
– Quality control and removal of poor-quality reads  
– Remove adapters and linkers  
• Map the reads  
• Count how many reads fall within each feature of interest  
(gene, transcript, exon etc).  
• Remove absent genes

-Remove absent genes (zero counts in all samples). It reduces the number of tests and the false discovery rate correction.  
•** Add offset (such as 1)**  
**– Prevent dividing by 0**  
**– Moderate fold change of low-count genes**  
• Identify differentially expressed genes.

## Why DeSeq

<http://biostar.stackexchange.com/post/show/10536/human-transcriptome-mapping/#10539>

<table width="100%" border="0">
  <tr>
    <td>
      <div>
        <div>
          <div data-original-title="Click to upvote">
          </div>
          
          <div>
            3
          </div>
          
          <div data-original-title="Click to downvote">
          </div>
          
          <div data-original-title="Click to add bookmark">
          </div>
        </div>
      </div>
    </td>
    
    <td width="100%">
      <div>
        <p>
          For alignment, TopHat is the only one I know of that is intended for spliced reads (transcriptome). You&#8217;ll get poor results with a genomic aligner. Nothing is perfect, even with tophat, I have found several islands of reads that mapped equally well in several places, and tophat was forced to choose one probabilistically, leaving me with some reads that belong to a gene, just floating in the middle of no where.
        </p>
        
        <p>
          For differential expression, the team that made tophat has a continuation tool called CuffLinks that constructions alternate isoforms (multiple transcript variants) and assigns probabilistic expression levels to them quite well. Here you have a choice of supplying it an annotation for exons vs letting it decide blindly. I let it construct novel transcripts because that&#8217;s what we really wanted to see, but found this to be a noisy process (many novel forms that look like mistakes). Then when every gene has three to six transcripts, comparing expression levels across samples is tricky indeed. Cufflinks will do it all for you, but I&#8217;m suspicious of just handing over the p-values to my bosses given they come from such tenuous associations.
        </p>
        
        <p>
          Another tool for differential expression is called DESeq, an R/Bioconductor package that requires a set of read counts per region and just does the math on that. So it doesnt try to construct new transcripts, you just supply it a table of regions (I used the refseq gene list from UCSC) by counts (coverageBED is a tool to count how many reads in a huge BAM file fall onto those locations). DESeq isn&#8217;t trying to make up new transcripts, and doesnt handle overlapping genes so well, (that&#8217;s up to the human preparing the read count table).. but the math is sound and sensible. Simpler tools feel more trustworthy.
        </p>
        
        <p>
          With about any fixed amount of reads, you&#8217;ll see some transcripts quite clearly, and some only roughly. More reads is better, but youre never going to have enough to see the lightest expression. CL sort of hides this from you, but DESeq is clear about their estimations.
        </p>
        
        <p>
          I have found in regions of poor coverage depth, CL can construct incorrect transcripts, (best guess). It shouldnt be expected to be accurate in the lack of data at low coverage genes (most of them!). Since DESeq starts with an annotated set of genes, and simple read counts, the results are more robust in low coverage areas, but I repeat it will not construct novel isoforms or do anything with reads falling outside of known annotated regions!
        </p>
      </div>
    </td>
  </tr>
</table>

**The normalizetion methods used by DESeq **

http://seqanswers.com/forums/showthread.php?p=16468#post16468

## Compare RNA-Seq with microarray results

<http://biostar.stackexchange.com/post/show/46863/how-to-go-about-comparing-rnaseq-with-micro-array-expression-data/>

##  Normalize RPKM

The first and most basic method is to simply divide each transcript’s fragment count from each library by the total number of fragments sequenced from that library [11]. However, expression levels calculated by this method may suffer from bias in some circumstances because RNA-Seq read counts provide only a relative abundance measure. Consider two libraries with an identical number of fragments, and where all genes but one are equally expressed in both libraries. **If the differentially expressed gene is also very highly expressed (and thus generates a large fraction of the fragments in each library), all of the other genes in the experiment will exhibit a change in their fragment count.** Excluding the genes in the **upper quartile** of the fragment count distribution from the total library size reduces this effect [2]. Additional sources of bias stem from differences in the lower tail of the count distribution.

## Visulalization

### IGV

1.igvtools count &#8211;strands first &#8211;includeDuplicates  sample.bam sample.hits.bam.tdf mm9 [for pair-edn data, strand specific data]

.igvtools count &#8211;strands read &#8211;includeDuplicates  sample.bam sample.hits.bam.tdf mm9 [for single-end strand specific data]

这个计算是根据map到的链来算的，如果测到的链确实来源于map到的链(fr-secondstrand)，则按此操作。如果测到的链来源于map的互补连，则需要修改输出文件positive和nagative互换。

2.Import bam file into IGV, and right click, &#8220;Load coverage data&#8221;  【[**seqanswers**.com/forums/showthread.php?t=3870][2]】

3.Right click， ‘autoscale’

<http://genomesavant.com/savant/documentation.php>

http://bioviz.org/igb/index.html

&#8212;&#8212;&#8211;

# Diff

http://seqanswers.com/forums/showthread.php?t=3951  【degseq】

http://seqanswers.com/forums/showthread.php?t=3951  【degseq，deseq，cuffdiff】

http://seqanswers.com/forums/showthread.php?t=4480 【theory】

http://www.biostars.org/post/show/46427/deseq-edger-and-cuffdiff-different-result/

http://seqanswers.com/forums/showthread.php?t=17678 【】

http://seqanswers.com/forums/showthread.php?t=13469

## How to estimate insert size for paired-end RNA-Seq data

http://vinaykmittal.blogspot.com/2012/02/how-to-estimate-insert-size-for-paired.html

Steps:  
1.)Create reference transcriptome index for BowTie (or BWA).  
2.)Align paired-end RNA-Seq data to the reference transcripts using minimum insert-length as zero and maximum insert-length as 500 (or more).  
BowTie: -I 0 -X 500, BWA: -a 500. Set output format as SAM(BowTie) or BAM(BWA).  
3.) Sort resulting SAM/BAM file using Picard&#8217;s SortSam.jar utility as follows: [no sort for tophat output]  
java -Xmx2g -jar picard-tools/SortSam.jar INPUT= OUTPUT= SORT_ORDER=coordinate  
4.) Now run Picard&#8217;s CollectInsertSizeMetrics.jar utility as follows:  
**java -Xmx2g -jar picard-tools/CollectInsertSizeMetrics.jar INPUT=accepted.hits.bam HISTOGRAM_FILE=insertSize.hist.pdf OUTPUT=insertSize.output**  
5.)Insert-size distribution is printed in output\_file while corresponding histogram image file is generated as pdf in histogram\_file.  
6.)Insert-matrix output\_file conain estimated insert-size and corresponding standard deviation. Picard generates two types estimates: &#8220;MEDIAN\_INSERT\_SIZE&#8221; and &#8220;MEAN\_INSERT_SIZE&#8221;. Anyoneone of them can be used but I prefer the second one since it is estmated after trimming off the outliers in from the original insert-size distribution in order to render normal distribution. Also the result will give information for** library-type**.

Note: If you plan to run TopHat on the same data aftrwards, set -r as (**estimated insert-size-2*read_length**) since TopHat requires distance between mate-pairs and not the insert-size.

## Map without genome

Velvet

&#8212;-

##  Tutorial

<http://vallandingham.me/Comparing-RNA-seq-Data.html>

**[http://vallandingham.me/RNA\_seq\_differential_expression.html][3] [Very Nice]**

https://main.g2.bx.psu.edu/u/muehlsch12/w/imported-tophat&#8212;cuffdiff-paired-end-fastq

https://sites.google.com/a/brown.edu/bioinformatics-in-biomed/cufflinks-and-tophat#read

https://docs.google.com/document/d/1t1gi2Djxd0ykMVe2bF8BVOBsOsPngjFh2999u3rZq-A/edit?hl=en&#038;authkey=CKL1i8sD&#038;pli=1

http://regulatorygenomics.upf.edu/Software/RNA-Seq\_and\_splicing/

&#8212;-

&#8212;-

Makefile scripts

Isoform identification tools  
ALEXA-seq  
Scripture  
Trans-ABySS  
Miso  
DEXSeq.

http://flux.sammeth.net/capacitor.html

http://www.biostars.org/p/65617/

http://seqanswers.com/forums/showthread.php?t=11381

1.  **Aligners** capable of identifying splice sites from sequence reads (aka splice aware aligners). These include: [TopHat][4], [MapSplice][5], [SpliceMap][6], [HMMsplicer][7], [GSNAP][8], [STAR][9], [RUM][10], [SoapSplice][11], etc. I saw a nice poster at AGBT13 that indicated that STAR performs very well compared to several competitors.
2.  **Transcriptome assemblers** that either perform de novo assembly of transcripts from sequence reads or do so with the help of a reference assembly (and perhaps even guided by known transcript annotations). These include: [Cufflinks][12], [Scripture][13], [Trinity][14], [Trans-ABySS][15], etc. Of these, Cufflinks is probably the easiest to use while Trinity and Trans ABySS seem to yield impressive results in the hands of certain groups (particularly those that developed them&#8230;).
3.  **Alternative expression** tools that seek to identify isoform expression differences between two or more conditions. These include: [Cuffdiff][16], [ALEXA-seq][17], [MISO][18], [SplicingCompass][19], [Flux Capacitor][20], etc.

There are also many tools that are usually considered for straight differential expression but if run the right way *might* still yield results informative to alternative expression of isoforms. These include: [edgeR][21], [DEseq][22], [htSeq][23], [DEGseq][24], sSeq, etc.

Note that placing each tool in one of three categories is an over-simplification. Some span across the three activities and some are components of a workflow generated by a single research group. Overall the area is a bit of a wild west. More tools are being developed constantly and you will find aspects of all of them that leave you wanting something better. The problem is not a simple one and is an area of active research.

The [intro section][25] of the ALEXA-seq website has a summary of some relevant background reading and also contains a now out-of-date [review of rna splicing tools][26].

Finally here are some relevant posts from BioStar and SeqAnswers:

*   [How are RNAseq Transcripts Assigned][27]
*   [Which program should I test to map RNAseq data?][28]
*   [Is there any other method for isoform-level differential expression analysis except cufflinks/cuffdiff?][29]
*   [Isoform expression quanification from rna seq: flood of tools][30]
*   [Novel isoform identification from RNA-seq][31]
*   [Differentiated expression analysis on isoforms/transcripts level][32]
*   [Alternative splicing in RNA-Seq][33]

2.MATS is a computational tool to detect differential alternative splicing events from RNA-Seq data. The statistical model of MATS calculates the P-value and false discovery rate that the difference in the isoform ratio of a gene between two conditions exceeds a given user-defined threshold. From the RNA-Seq data, MATS can automatically detect and analyze alternative splicing events corresponding to all major types of alternative splicing patterns. MATS handles replicate RNA-Seq data from both paired and unpaired study design.

3.Get rRNA GTF

<pre class="brush: bash; title: get rRNA.gtf file from UCSC Table Browser; notranslate" title="get rRNA.gtf file from UCSC Table Browser">get rRNA.gtf file from UCSC Table Browser

You can get this pretty easily from the UCSC table browser (http://genome.ucsc.edu/cgi-bin/hgTables).

Select "All Tables" from the group drop-down list
Select the "rmsk" table from the table drop-down list
Choose "GTF" as the output format
Type a filename in "output file" so your browser downloads the result
Click "create" next to filter
Next to "repClass," type rRNA
Next to free-form query, select "OR" and type repClass = "tRNA"
Click submit on that page, then get output on the main page
</pre>

 [1]: http://210.75.224.29/wordpress/?p=1580
 [2]: seqanswers.com/forums/showthread.php?t=3870
 [3]: http://vallandingham.me/RNA_seq_differential_expression.html
 [4]: http://tophat.cbcb.umd.edu/
 [5]: http://www.netlab.uky.edu/p/bioinfo/MapSplice
 [6]: http://www.stanford.edu/group/wonglab/SpliceMap/
 [7]: http://derisilab.ucsf.edu/index.php?software=105
 [8]: http://research-pub.gene.com/gmap/
 [9]: https://code.google.com/p/rna-star/
 [10]: http://cbil.upenn.edu/RUM/
 [11]: http://soap.genomics.org.cn/soapsplice.html
 [12]: http://cufflinks.cbcb.umd.edu/
 [13]: http://www.broadinstitute.org/software/scripture/
 [14]: http://trinityrnaseq.sourceforge.net/
 [15]: http://www.bcgsc.ca/platform/bioinfo/software/trans-abyss
 [16]: http://cufflinks.cbcb.umd.edu/manual.html#cuffdiff
 [17]: http://www.alexaplatform.org/alexa_seq/
 [18]: http://genes.mit.edu/burgelab/miso/
 [19]: http://www.ichip.de/software/SplicingCompass.html
 [20]: http://flux.sammeth.net/capacitor.html
 [21]: http://www.bioconductor.org/packages/2.11/bioc/html/edgeR.html
 [22]: http://www-huber.embl.de/users/anders/DESeq/
 [23]: http://www-huber.embl.de/users/anders/HTSeq/doc/count.html
 [24]: http://www.bioconductor.org/packages/2.11/bioc/html/DEGseq.html
 [25]: http://www.alexaplatform.org/alexa_seq/intro.htm
 [26]: http://www.alexaplatform.org/alexa_seq/data/ReviewOfRNA-SeqSplicingTools.xls
 [27]: http://www.biostars.org/p/16649/
 [28]: http://www.biostars.org/p/8067/
 [29]: http://www.biostars.org/p/64541/
 [30]: http://seqanswers.com/forums/showthread.php?t=26043
 [31]: http://seqanswers.com/forums/showthread.php?t=13991
 [32]: http://seqanswers.com/forums/showthread.php?t=16840
 [33]: http://seqanswers.com/forums/showthread.php?t=11381