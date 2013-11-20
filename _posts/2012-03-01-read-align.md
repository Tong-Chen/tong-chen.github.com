---
title: 'Next Generation Sequencing Analysis &#8211; ChIP-Seq'
author: 悟道
layout: post
permalink: /?p=1580
categories:
  - seq
tags:
  - NGS
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

# 

# Data download

NCBI GEO：用数据集编号GSE或文章名字搜索 ，下载SRA study为一整套数据，数据意义的描述在Series Matrix File。

EBI：用文章名字搜索，得到数据后，选择download text，最后一列为链接，前几列为数据描述。

快速下载参见[aspera。][1]

# Format transition

## sra-fastq

sra files are downloaded from ncbi [www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=announcement][2]

安装：直接make, 会安装在./linux/rel/gcc/x86-64/，需要导出动态链接库可使用

<pre class="brush: bash; title: ; notranslate" title="">export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/sra_sdk-2.1.9/linux/rel/gcc/x86_64/lib

fastq-dump file.sra   #output file.fastq

fastq-dump -O outputdir sradir/ #output fastq
</pre>

#如果出现错误，检查下载的数据是否完整。

# Quality control

## fastQC

下载即可运行，fastqc 【如果不可执行，给予其可执行权限】[安装java见站内][3]。

基本安装使用见：<http://www.bioinformatics.bbsrc.ac.uk/projects/fastqc/INSTALL.txt>

<pre class="brush: bash; title: ; notranslate" title="">fastqc   #initiate a gui

fastqc input.fastq --outdir=./</pre>

Interpret &#8220;[Per Base Sequence Quality][4]&#8221; :

The background of the graph divides the y axis into very good quality calls (green, larger than 28), calls of reasonable quality (orange, larger than 20), and calls of poor quality (red, smaller than 20).

## FATSX tools

[http://hannonlab.cshl.edu/fastx\_toolkit/commandline.html#fastx\_collapser_usage][5]

## **Printseq**

<http://prinseq.sourceforge.net/>

## Solexa

<http://sourceforge.net/projects/solexaqa/>

# 接头序列去除

http://www.biostars.org/post/show/12858/cutadapt-or-fastx-clipper/

https://code.google.com/p/cutadapt/

seqanswers.com/forums/showthread.php?t=1159

# Reads mapping

## Bowtie

下载二进制版本即可使用，默认BOWTIE_INDEXES是安装目录下的indexes文件夹，可以自己修改指定自己的index路径。

基本使用见：<http://bowtie-bio.sourceforge.net/tutorial.shtml>

<http://bowtie-bio.sourceforge.net/manual.shtml>

<pre class="brush: bash; title: ; notranslate" title="">bowtie  -p 8 -S -M 1 --best &lt;human.ebwt&gt; &lt;reads.fastq&gt; &lt;outpu.sam&gt; #随机返回一个最好的匹配

bowtie  -p 8 -S -k 1 -n 2 --best &lt;human.ebwt&gt; &lt;reads.fastq&gt; &lt;outpu.sam&gt;  #随机返回一个最好的匹配, get from a protocol

bowtie -p 8 -S -m 1 -n 0 &lt;human.ebwt&gt; &lt;reads.fastq&gt; &lt;output.sam&gt;  #返回完全匹配，并且只匹配到基因组上单一位点的序列。

bowtie -a --best --strata -n 1 -l 28  e_coli -c&lt;code&gt; ATGCATCATGCGCCAT  #设定较小的错配，返回一批最好的匹配位点。可能可以消除随机返回一个位点的偏见。&lt;/code&gt;

bowtie -n2 -l28 -e70 --chunkmbs 300 -a -m1 -S --best --strata -p6 &lt;human.ebwt&gt; read.fastq output.sam

bowtie -n2 -l28 -e70 --chunkmbs 300 -a -m10 -S --best --strata -p6 -M2 &lt;human.ebwt&gt; read.fastq output.sam  #多于10(-m10)个匹配位点的扔掉，多于2个位点(-M2)随即返回一个

bowtie -n2 -l28 -e70 --chunkmbs 300 -a -m10 -S --best --strata -p6 -M3 &lt;human.ebwt&gt; read.fastq output.sam #多于10(-m10)个匹配位点的扔掉，多于3个位点(-M3)随即返回一个</pre>

解释： -p 8 使用并行8个线程

-S 输出sam格式

-M 1 &#8211;best 返回一个随机hit

其它参数：

-n N (N取值为0-3，默认是2. 表示种子序列中所能允许的最大错配数目。

-l L (L取值大于等于5， 指定左数L个残基为高质量的种子序列

&#8211;best

-a 报告所有有效的比对 （与&#8211;best 同用时输出从最好到最坏排序）

-k int 最多报告k个有效的比对（默认为1，报告bowtie遇到的第一个有效的比对）

&#8211;suppress int1,int2 不输出第int1和int2列

<pre class="brush: bash; title: ; notranslate" title="">bowtie -a --best --strata -v 2 e_coli -c&lt;code&gt; ATGCATCATGCGCCAT&lt;/code&gt;

只报告最好的比对的那些，如果有完全匹配的，报告所有完全匹配的。如果有一个错配的，报告所有一个错配的。</pre>

-m 2 如果比对位置多于两个，则不报告这个reads的比对。-m 1 只输出uniq map的reads

<pre class="brush: bash; title: ; notranslate" title="">bowtie -a -m 3 --best --strata -v 2 e_coli -c &lt;code&gt;ATGCATCATGCGCCAT&lt;/code&gt;

-a --best --strata的优先级高于-m, 因此当符合条件的read的map位点</pre>

[Fastq quality][6]:

&#8211; phred33-quals [default on] {sanger, illumina 1.8+}

<pre class="brush: bash; title: ; notranslate" title="">&lt;pre&gt;!"#$%&'()*+,-./0123456789:;&lt;=&gt;?@ABCDEFGHIJ&lt;/pre&gt;
</pre>

&#8211;phred64-quals [default off] {illumina 1.3+, illumina 1.5+, }

<pre class="brush: bash; title: ; notranslate" title="">&lt;pre&gt;@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefgh&lt;/pre&gt;
</pre>

&#8211;solexa-quals [default off] {solexa, prior GA Pipeline version 1.3}

<pre class="brush: bash; title: ; notranslate" title="">&lt;pre&gt;;&lt;=&gt;?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefgh&lt;/pre&gt;
</pre>

&#8211;solexia1.3-quals [default off] {same as &#8211;phred64_quals, GA Pipeline version 1.3 or later}

## BOWTIE2

bowtie2 -x <human>.1.bt2 -u reads.fastq -S reads.sam &#8211;phred33

## BWA

下载后，直接make即可安装.【查看参数时，除了看manual还要去自己输入以下，看看对应当前版本的参数是否有变】

<pre class="brush: bash; title: ; notranslate" title="">bwa index -a bwtsw database.fasta   [when database larger than 2GB or your memory less than 5.37 multiply N (N Gb is dtabase size]

bwa aln database.fasta short_read.fastq &gt;aln_sa.sai

bwa aln -n 0 -t 8 database.fasta short_read.fastq &gt;aln_sa.sai #perfect match, 8 threads

-l set the seed length [25-35, default 32] [version 0.6.1-r104]

-k set the mismatch of seeds[default 2]

-I illumina 1.3+ read format

bwa samse database.fasta aln_sa.sai short_read.fastq &gt;aln.sam  #aln.sam中序列的总数是用来map的原始序列总数。</pre>

XT:A:U => unique alignment

XT:R => repeat

XT:N => not mapped

XT:M => Mate-sw

<table cellspacing="1">
  <tr valign="top">
    <td align="center">
      <strong>NM</strong>
    </td>
    
    <td>
      Edit distance
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>MD</strong>
    </td>
    
    <td>
      Mismatching positions/bases
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>AS</strong>
    </td>
    
    <td>
      Alignment score
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>BC</strong>
    </td>
    
    <td>
      Barcode sequence
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>X0</strong>
    </td>
    
    <td>
      Number of best hits
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>X1</strong>
    </td>
    
    <td>
      Number of suboptimal hits found by BWA
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XN</strong>
    </td>
    
    <td>
      Number of ambiguous bases in the referenece
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XM</strong>
    </td>
    
    <td>
      Number of mismatches in the alignment
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XO</strong>
    </td>
    
    <td>
      Number of gap opens
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XG</strong>
    </td>
    
    <td>
      Number of gap extentions
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XT</strong>
    </td>
    
    <td>
      Type: Unique/Repeat/N/Mate-sw
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XA</strong>
    </td>
    
    <td>
      Alternative hits; format: (chr,pos,CIGAR,NM;)*
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XS</strong>
    </td>
    
    <td>
      Suboptimal alignment score
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XF</strong>
    </td>
    
    <td>
      Support from forward/reverse alignment
    </td>
  </tr>
  
  <tr valign="top">
    <td align="center">
      <strong>XE</strong>
    </td>
    
    <td>
      Number of supporting seeds
    </td>
  </tr>
</table>

基本使用参见：<http://bio-bwa.sourceforge.net/bwa.shtml>

NOtes: Pay attention to NM to make sure the mismatch is no larger than the value you set. If the seed region is set, the mismatch value is the sum of the value after -n and -k.

## Filter Mapped Reads

1. Only using unique mapped and perfect mapped reads.

ref:Connecting microRNA Genes to the Core Transcriptional Regulatory Circuitry of Embryonic Stem Cells

cmd:

<pre class="brush: bash; title: ; notranslate" title="">bowtie -p 8 -S -m 1 -n 0 -l 28&lt;human.ebwt&gt; &lt;reads.fastq&gt; &lt;output.sam&gt; --phred33-quals [种子序列无错配, -v 整个序列无错配]

bwa aln -t 8 -n 0 #perfect match, unique match need to be filtered by XT and XOor Reads were filtered by removing those with a BWA alignment quality score less than 15.</pre>

## Filter Redundant reads

In ChIP-seq, it&#8217;s almost a standard procedure to **remove those redundant reads that map to the same location with the same orientation**. It&#8217;s reasonable because by chance it&#8217;s very unlikely for the sonication to break the genomic sequence at the same location for more than twice during sample preparation. So, if we see the redundant reads, they are most likely PCR amplifications.

However, it seems NOT to be a standard to remove those redundant reads for RNA-seq. My understanding is that the total coding sequence length is much shorter than the genomic sequence length, which significantly increase the chance for the same location to be selected for sequencing.

<pre class="brush: bash; title: ; notranslate" title="">samtools rmdup -s input.sort.bam input.sort.rmdup.bam  [suitable for single-end reads, picard for paired-end reads]

map rmdup

java -Xmx2g -jar ~/picard-tools-1.21/MarkDuplicates.jar INPUT=test_sorted.bam OUTPUT=test_rmdup.bam METRICS_FILE=PCR_duplicates REMOVE_DUPLICATES=true  [http://seqanswers.com/forums/showthread.php?t=5494]</pre>

## SAMtools

同样make安装，不知道开发者怎么想的，连安装指南都懒得写

基本使用：<http://samtools.sourceforge.net/samtools.shtml>

samtools protocol: <http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol>

<http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_FAQ>

samtools view -X #查看flag

Add NM and MD tags for paired-end reads mapped with BWA-SW

<pre class="brush: bash; title: ; notranslate" title="">samtools calmd -uS input.sam.gz ref.fa | samtools sort - input  [-u means no compress, it is fast when using pipeline, the '-' after pipeline referes to the output file of the pre-command, the last 'input' represents the prefix of the output sorted bam file 'input.bam']</pre>

转换SAM为BAM，并排序，去除unmapped reads

<pre class="brush: bash; title: ; notranslate" title="">samtools view -ubS -F 4 input.sam | samtools sort - input.sort  [if there are @SQ headers in your sam file]

samtools faidx ref.fa && samtools view -ubtS ref.fa.fai input.sam | samtools sort - input.sort [no matter whether @SQ headers exist or not]</pre>

BAM只保留uniq mapped reads

BAM去除PCR扩增

<pre class="brush: bash; title: ; notranslate" title="">samtools rmdup -s input.sort.bam input.sort.rmdup.bam  [suitable for single-end reads, picard for paired-end reads]

命令行输出为[bam_rmdupse_core] 6 / 5343462 = 0.0000 in library '    ', 6 means the number of deleted duplicate reads, 5343462 represents the number of remaining mapped reads.

&lt;strong&gt;TIPs:&lt;/strong&gt;input.bam must to be sorted. It can not filter out different flags, such as forward and reverse strand even for single-end reads. It only considers the highest mapq, but not NM.

samtools view -c input.bam (samtools view input.bam | wc -l) gives all the reads in bam file

samtools view -f4 -c input.bam gives unmapped reads in bam file</pre>

BAM根据MAPQ筛选质量高的reads

<pre class="brush: bash; title: ; notranslate" title="">samtools view -bq 1 aln.bam &gt;aln-reliable.bam [-q specifies the mapq value, all reads with value larger than it will be output]</pre>

BAM排序

<pre class="brush: bash; title: ; notranslate" title="">samtools sort input.bam output.prefix  [The result will be saved into output.prefix.bam unlesss -o is specified.  Using -n can sort by read names rather than by chromosomal coordinates.]</pre>

BAM索引

<pre class="brush: bash; title: ; notranslate" title="">samtools index output.prefix.bam [index file output.prefix.bam.bai will be created]</pre>

## Picard

http://picard.sourceforge.net/

## maq

安装： ./configure &#8211;prefix=~/mapq; make; make install

基本使用：未使用

## 

## Chip-seq normalize

http://www.biostars.org/post/show/42291/how-to-do-normalization-of-two-chip-seq-data/

Most likely they simply divided the number of reads in larger sample with the number of reads in the smaller sample. Then they used this factor to divide whatever read count they got per each peak for the larger sample.

Imagine that they had 1000 total reads for sample1 and 5000 total reads for sample2. The ratio relative to the smaller number is 5000/1000 = 5 so we expect on average that the peaks in sample2 to contain five times as many reads than in in sample1. To allow for direct comparison between sample1 and sample2 they divide the read counts for peaks in sample2 by 5.

The reason to average to smaller factor is to reduce more data to less rather then boost less data to be more.

# Values to be computed

The quality of the reads.

No. of Total reads, mapped reads, unique mapped reads, unmapped reads, duplicate reads, reads mapped to forward strand and reverse strand

the mapq distribution of mapping result

# Get gene structure from ucsc

## 全基因组注释

<pre>The best way to download the USCS genes table in GTF format would be to
use the table browser(
<a href="http://www.genome.ucsc.edu/cgi-bin/hgTables?hgsid=247205831&clade=mammal&org=&db=hg18&hgta_group=genes&hgta_track=knownGene&hgta_table=knownGene&hgta_regionType=genome&position=&hgta_outputType=primaryTable&hgta_outFileName=). ">http://www.genome.ucsc.edu/cgi-bin/hgTables?hgsid=247205831&clade=mammal&org=&db=hg18&hgta_group=genes&hgta_track=knownGene&hgta_table=knownGene&hgta_regionType=genome&position=&hgta_outputType=primaryTable&hgta_outFileName=). </a>After selecting your assembly of interest select:

     group: Genes and Gene Prediction Tracks
     track: UCSC Genes  refgene
     table: knownGene   refflat
     output format: "GTF - gene transfer format"

Then select "gzip compressed" and make sure you enter a name for the
output file (note that if you leave this field blank the browser will
try to return all of this information in your browser window and it may
stall or crash).</pre>

## TSS位点获得

<pre>The best way to download the USCS genes TSS table would be to
use the table browser(
<a href="http://www.genome.ucsc.edu/cgi-bin/hgTables?hgsid=247205831&clade=mammal&org=&db=hg18&hgta_group=genes&hgta_track=knownGene&hgta_table=knownGene&hgta_regionType=genome&position=&hgta_outputType=primaryTable&hgta_outFileName=). ">http://www.genome.ucsc.edu/cgi-bin/hgTables?hgsid=247205831&clade=mammal&org=&db=hg18&hgta_group=genes&hgta_track=knownGene&hgta_table=knownGene&hgta_regionType=genome&position=&hgta_outputType=primaryTable&hgta_outFileName=). </a>After selecting your assembly of interest select:

     group: Genes and Gene Prediction Tracks
     track: UCSC Genes
     table: knownGene
     output format: "Select fields from primary anr related tables"
     output file : filename   #if not given, table will be opened in browser.

 点击“getoutput”,选择name, chrom, strand, txStart, txEnd, 点击"get output".
 If id transfer wanted, keep selecting 'proteinID', 'geneSymbol', 'refseq', 'description'
 Then click 'get output'

UCSC ID 转换
<a href="https://lists.soe.ucsc.edu/pipermail/genome/2010-March/021453.html">Use the Table browser or also download these associated tables</a>.

knownToEnsembl
kgProtAlias

To see all linked tables (and which keys they are linked on), open the
UCSC Genes track in the Table browser and click into "describe table
schema". Linked files can be merged and downloaded here with output
format "selected fields from primary and related tables". For these
tables, this is the specific path to link the data:

knownGene.name -&gt; knownToEnsembl.name
knownToEnsembl.value = Ensembl Id

knownGene.name -&gt; kgProtAlias.kgID
kgProtAlias.alias = protein aliases from several sources, including HUGO

<a href="http://genome.ucsc.edu/cgi-bin/hgTables">http://genome.ucsc.edu/cgi-bin/hgTables</a></pre>

Table Browser : Group: genes and gene prediction tracks Track: ucsc geens table: kgProtAlias outputformat: selected fields from primary and related tables <get output> hg18.kgProtAlias&#8212;->kgID hg18.kgXref&#8212;&#8212;&#8212;>geneSymbol, refseq linkedtables&#8212;&#8212;&#8211;>proteome.hgnc&#8212;&#8212;&#8212;>Allow selection from checked tables proteome.hgnc&#8212;&#8212;->hgncid, symbol <get output> Note:hgnc.symbol和geneSymbol几乎一样

获得各个基因组元件见讨论http://seqanswers.com/forums/showthread.php?t=7113

http://www.oreganno.org/oregano/

# Bin Genome

<pre class="brush: bash; title: ; notranslate" title="">awk 'BEGIN{OFS="\t";FS="\t"}{for(i=0;i&lt;$2;i+=200) {j=i+200; if(j&gt;$2) j=$2;print $1,i,j, "mm9_"$1"_"i}}' tmp.1</pre>

# ** Get constitutive exon and spliced exon**

<table>
  <tr>
    <th>
      AS Pattern Type
    </th>
    
    <th>
      Acronym
    </th>
    
    <th>
      Definition
    </th>
  </tr>
  
  <tr>
    <td>
      Cassette exon (skipped exon)
    </td>
    
    <td>
      CE
    </td>
    
    <td>
      One exon is spliced out of the primary transcript together with its flanking introns.
    </td>
  </tr>
  
  <tr>
    <td>
      Intron retention
    </td>
    
    <td>
      IR
    </td>
    
    <td>
      A sequence is spliced out as an intron or remains in the mature mRNA transcript.
    </td>
  </tr>
  
  <tr>
    <td>
      Mutually exclusive exons
    </td>
    
    <td>
      MXE
    </td>
    
    <td>
      Refer to a case in which multiple cassette exons are used in a mutually exclusive manner. In the simplest case: two consecutive exons that are never both included in the mature mRNA transcript.
    </td>
  </tr>
  
  <tr>
    <td>
      Alternative 3&#8242; sites
    </td>
    
    <td>
      A3SS
    </td>
    
    <td>
      Also called alternatively acceptor sites. Two or more splice sites are recognized at the 5&#8242; end of an exon. An alternative 3&#8242; splice junction (acceptor site) is used, changing the 5&#8242; boundary of the downstream exon.
    </td>
  </tr>
  
  <tr>
    <td>
      Alternative 5&#8242; sites
    </td>
    
    <td>
      A5SS
    </td>
    
    <td>
      Also called alternative donor sites. Two or more splice sites are recognized at the 3&#8242; end of an exon. An alternative 5&#8242; splice junction (donor site) is used, changing the 3&#8242; boundary of the upstream exon.
    </td>
  </tr>
  
  <tr>
    <td>
      Alternative first exon
    </td>
    
    <td>
      AFE
    </td>
    
    <td>
      Second exons of each variant have identical boundaries, but first exons are mutually exclusive. This is to annotate possible alternative promoter usage*.
    </td>
  </tr>
  
  <tr>
    <td>
      Alternative last exon
    </td>
    
    <td>
      ALE
    </td>
    
    <td>
      Penultimate exons of each splice variant have identical boundaries, but last exons are mutually exclusive. This is to allow annotation of possible alternative polyadenylation usage
    </td>
  </tr>
</table>

1.http://www.biostars.org/post/show/4959/datasource-for-human-generic-exons/

2.http://www.ebi.ac.uk/asd/index.html [not update any more]

3.http://www.ensembl.org/info/docs/genebuild/ase_annotation.html

4.ensembl-biomart-attribute-structure-exon start, exon end, constitutive exon, exon rank, ensembl exon

# Format Transition

## bed format

<genome.ucsc.edu/FAQ/FAQformat#format1>

6-columns: chrom, chromStart, chromEnd, name, score, strand

chromstart: The first base in a chromosome is numbered 0.

chromEnd: The chromEnd base is not included in the display of the feature. For example, the first 100 bases of a chromosome are defined as chromStart=0, chromEnd=100, and span the bases numbered 0-99.

## bedtools

下载：<http://code.google.com/p/bedtools/>

安装：make clean && make all， 安装之后文件在./bin 里面

使用：

### 转换bam文件为bed文件

<pre class="brush: bash; title: ; notranslate" title="">bamToBed -i input.bam &gt;input.bed  #6-column bed file, score is mpq, it will add /1 and 2 to paired-end files &lt;strong&gt;bam file must be sorted.&lt;/strong&gt;

-bed12  #output bloacked bed, bed12, with -split as default

-ed # use NM, edit distance as the score, or using -tag NM

-bedpe  #another way of output paired-end reads</pre>

### Pair-end special reds

当处理DNA的pair-end数据时，需要两条mapped reads所代表的的片段用来计算区域的coverage。  
&#8216;fill in the interval between two reads that are properly paired when generating a coverage (wig,bedgraph) file from ChIP-seq data.&#8217;

<pre class="brush: bash; title: ; notranslate" title="">1. Use "bedtools bamtobed -bedpe" to convert paired-end reads from a BAM file into a non-standard BED-PE file.
Each line will contain two reads (the paired reads).

2. Use an AWK script to take the start of one read and the end of the other, and construct a new standard BED file.
This assumes the reads represent genomic/DNA data (ie no splicing consideration).
The strand of the combined fragment is the same as the first mate.

3. Use "bedtools genomecov" to calculate the coverage on the new BED file. 
</pre>

<https://groups.google.com/forum/?fromgroups=#!topic/bedtools-discuss/oDpz8q0zFWM>

### Bed文件排序

<pre class="brush: bash; title: ; notranslate" title="">sortBed -i filein.bed &gt;filein.sort.bed</pre>

### 计算基因组覆盖度

<pre class="brush: bash; title: ; notranslate" title="">genomeCovergeBed -i input.bed -g genome</pre>

The genome file should be tab delimited and structured as <chromName><TAB><chromSize>, this can be got from UCSC genome browser&#8217;s mysql database.

<pre class="brush: bash; title: ; notranslate" title="">mysql --user=genome --host=genome-mysql.cse.ucsc.edu -A -e "select chrom, size from hg19.chromInfo" &gt;hg19.genome</pre>

输出文件格式为：染色体名字，覆盖深度，覆盖深度为第二列数值的碱基数目，染色体的碱基总数，覆盖度为第二列数值的碱基在整个染色体的比例。

chr10 0 48114320 135374737 0.355416  
chr10 1 36043456 135374737 0.26625  
chr10 2 24108025 135374737 0.178084  
chr10 3 13655388 135374737 0.100871

利用命令可以得到reads在基因组的覆盖度：(tips4)

<pre class="brush: bash; title: ; notranslate" title="">awk '$2==0{a[3]+=$3;a[4]+=$4}END{print 1-a[3]/a[4]}' genomecovResult

awk '$1=="genome"&amp;&amp;$2==0{print 1-$5}' genomecovResult</pre>

利用下面的命令可以得到在基因租的覆盖深度

<pre class="brush: bash; title: ; notranslate" title="">awk 'NR==1{sum=0}$1=="genome"{sum += $2 * $3;totel=$4}END{print sum/total}' genomecovResult</pre>

### 报告两个bed文件中有碱基对重叠的特征

<pre class="brush: bash; title: ; notranslate" title="">intersectBed -a reads.bed -b genes.bed</pre>

### 报告两个bed文件中没有碱基对重叠的特征

<pre class="brush: bash; title: ; notranslate" title="">interactBed -a reads.bed -b genes.bed -v</pre>

### 查找每个基因距离最近的alu

<pre class="brush: bash; title: ; notranslate" title="">closestBed -a genes.bed -b alus.bed</pre>

### 合并重叠的特征为一项

<pre class="brush: bash; title: ; notranslate" title="">mergeBed -i features.bed</pre>

### 合并临近的特征为一项, -d指定距离

<pre class="brush: bash; title: ; notranslate" title="">mergeBed -i fratures.bed -d 1000</pre>

### 转换bed为wig/bedgraph,参考[1][7]，[2][8] [macs会输出整个的样品wig]

<pre class="brush: bash; title: ; notranslate" title="">genomeCoverageBed -bg -i input.sort.bed -g genome &gt;fileoutput.bdg

wigToBigWig -clip fileoutput.bdg genome fileout.bw

sortBed -i filein.bed | slopBed -i stdin -s -r XXX -l YYY -g genome | genomeCoverageBed -bg -i stdin -g chromsizes.tab &gt; fileout.bdg

XXX and YYY are sizes you should extend each interval to cover the fragment you sequenced (i.e. if you use Illumina and fragmented 200bp and read 36bp you should set XXX=180 YYY=0

bamToBed -i input.bam | sortBed -i stdin | slopBed -i stdin -s -r xxx -l yyy -g genome | genomeCoverageBed -bg -i stdin -g genome &gt;fileout.bdg

bedGraphToBigWig fileout.bdg chrom.sizes fileout.bw

bigWigToWig fileoutin.bigWig fileout.wig</pre>

### 转换wig为bed

<pre class="brush: bash; title: ; notranslate" title="">wigToBed:
for i in *.data; do \
nohup awk 'BEGIN{OFS="\t"}{if(match($$0, /^fixed/)) {split($$0, array, " "); chr=substr(array[2],7); start=substr(array[3], 7); step=substr(array[4],6); } else {end=start+step; print chr, start, end, $$0; start=end} }' $$i &gt;$$i.bed & done

wig format

fixedStep chrom=chr10 start=3009320 step=1
0.037
0.065
0.085
0.099
0.137
0.165
0.184</pre>

### bedToIGV

<pre class="brush: bash; title: ; notranslate" title="">bedToIgv -i data/rmsk.hg18.chr21.bed &gt; rmsk.igv.batch</pre>

## UCSC tools

<http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/>

bedGraphToBigWig

bigWigToWig

fetchChromSizes hg18 > hg18.chrom.sizes

liftover : converts genome coordinates and genome annotation files between assemblies. **<http://hgdownload.cse.ucsc.edu/admin/exe/> The *over.chain* liftOver conversion files are located in the individual assembly download sections**

# **Visulization Software**

## IGV

igvtools tile $(basename $@).wig $(basename $@).tdf hg18

# Peak-caling

## Tools comparision

<http://biostar.stackexchange.com/questions/726/which-chip-seq-peak-callers-do-you-use>

## Common things

*   Choose the shift distance. Select a peak and check how far the summits of the same peak on the 5&#8242; and the 3&#8242; strands are. Verify that this value is the same on other peaks. When you&#8217;re sure about the value, divide it by two and note this result. [macs will auto model this value, one can change it by setting --nomodel --shiftsize=100]
*   Normalize :RPKM/RPM

## MACS

下载，python setup.py install &#8211;prefix=~/macs， 根据安装包里的INSTALL文件设置环境变量

基本使用：<http://liulab.dfci.harvard.edu/MACS/> <http://ged.msu.edu/angus/tutorials-2011/chipseq-peakcalling-tutorial.html>

<pre class="brush: bash; title: ; notranslate" title="">mouse: macs14 -t sample.sam -c control.sam --name=sample-test --format=SAM -g mm --wig -t 100 -bw 200 -S

human:macs14 -t sample.sam -c control.sam --name=sample-test --format=SAM -g hs --wig

mouse: macs14 -t sample.bam --name=sample-test --format=BAM -g mm --wig

human:macs14 -t sample.bam --name=sample-test --format=BAM -g hs --wig

-w/--wig 为每条染色体输出一个单独的wiggle文件,

-w --single-profile 整个基因组输出一个wig文件

-g/--gsize map上的基因组的大小

Other usage:

&lt;strong&gt;python macs -t xxx.bed --tsize=50 --format=BED --nomodel --name xxx --bw=100 --control=control.bed&lt;/strong&gt;

--tsize/-s Tag size. This will override the auto detected tag size,&lt;strong&gt; this is the read size&lt;/strong&gt;

--bw=BW Band width. This value is only used while building the shifting model. &lt;strong&gt; estimated soniation size, default 300&lt;/strong&gt;

--diag generate the table to evaluate sequence saturation

For histone modification ，参考&lt;a href="http://onlinelibrary.wiley.com/doi/10.1002/0471250953.bi0214s34/full#bi0214-prot-0002"&gt;http://onlinelibrary.wiley.com/doi/10.1002/0471250953.bi0214s34/full#bi0214-prot-0002&lt;/a&gt;

macs for 5hmc

Parameters were as follows: effective genome size = 2.72e+09; tag size = 38; band width = 100; model fold = 10; &lt;em&gt;P&lt;/em&gt; value cutoff = 1.00e-05; ranges for calculating regional lambda are: peak_region, 1,000, 5,000, 10,000.  &lt;a href="http://www.nature.com/nbt/journal/v29/n1/full/nbt.1732.html"&gt;http://www.nature.com/nbt/journal/v29/n1/full/nbt.1732.html&lt;/a&gt;</pre>

Notes:

<pre class="brush: bash; title: ; notranslate" title="">1.macs will auto model shiftsize, one can change it by setting --nomodel --shiftsize=100【shiftsize is the half of the sequenced reads】

2.FDR is defined as number of control peaks / Number of ChIP peaks.

3.fold enrichment : the ratio between the ChIP-Seq tag count and lambdalocal

4.--bw sets the ‘bandwidth’, which is half of the sliding window size used in the model-building step. Usually same as or a little larger than sheared chromatin size

5.Warning 'unbalanced reads between treatment and control’ means that the FDR of  the resulting peaks will be &lt;strong&gt;overestimated when the control sample has more read&lt;/strong&gt;s and will be underestimated when the ChIP-seq sample is sequenced more deeply

6. The message ‘missing chromosome X data’ might suggest that the raw input file for that chromosome is incomplete.

7.--shiftsize half of fragment size.  The fragment size is set to 146 because a nucleosome is wrapped in a DNA sequence that is ~146 bp in length, extending reads mapped to either DNA strand in the 3 ′ direction by 146 bp. users can also specify the fragment size according to their sequencing library preparation, often in the range of 150–300 bp.

8.For H3K36me3, command sets a less stringent P value cutoff ( --pvalue ?1e-3) than the default ( 1e-5). Because H3K36me3 ChIP-seq data often form broader but less-enriched regions, the parameters --nomodel and --shiftsize ?73 are preferred.

macs14?-t?BROAD_GM12878_H3K36me3.bam?-c?BROAD_GM12878_H3K36me3_Control.bam?-g?hs?-n?BROAD_GM12878_H3K36me3?--nomodel?--shiftsize?73?-B?-S?--pvalue ?1e-3?--call-subpeaks</pre>

Output:

<pre class="brush: bash; title: ; notranslate" title="">1.The outputted wig files  include entire genome, not just peak regions.

2.</pre>

## CEAS

北大镜像：<http://ceas.cbi.pku.edu.cn/index.html> <http://ged.msu.edu/angus/tutorials-2011/chipseq-peakcalling-tutorial.html>

下载<http://liulab.dfci.harvard.edu/CEAS/download.html>，安装python setup.py install &#8211;prefic=~/ceas

<pre class="brush: bash; title: ; notranslate" title="">export PYTHONPATH=$PYTHONPATH:~/ceas/lib/python2.6/site-packages  #官方文档有些错误，第一个PYTHONPATH不应有$符号</pre>

使用：<http://ged.msu.edu/angus/tutorials-2011/chipseq-peakcalling-tutorial.html>

<pre class="brush: bash; title: ; notranslate" title="">ceas -g ../../ceas/hg18.refGene -b SRR408156_peaks.bed -w SRR408156_MACS_wiggle/SRR408156_treat_afterfiting_genome.wig --name=SRR408156.ceas

#hg18.refGene在ceas官网下载，bed文件是macs输出的bed peak，wig文件是合并macs输出的wig文件

&lt;code&gt;ceas --name=SDC3_ceas --bg --gname2 --pf-res=86 --gn-groups=ce_top10.txt,ce_middle10.txt,ce_bottom10.txt --gn-group-names='Top 10%,Middle 10%,Bottom 10%' -g ./ce4/refGene -b SDC3_MA2C_peaks.bed -w SDC3_MA2Cscore.wig -e nc_regions.bed --dump&lt;/code&gt;

In this case, we decided to re-annotate the genome background (--bg) based on SDC3_MA2Cscore.wig file because the input WIG file contains all tiled locations. The option, --gname2, was set since gene IDs instead of RefSeq IDs were used in the gene group files (ce_top10.txt,ce_middle10.txt,ce_bottom10.txt after --gn-groups). It should be noted that a wrong choice of profiling resolution (--pf-res) causes artifacts in average gene profiling. In this example, the WIG file resolution (tiling space) is 86 bp while the default is 50 bp. An extra BED file, nc_regions.bed, is also given after -e (or --ebed) to perform ChIP region annotation on non-coding regions of C. elegans. --dump 输出profile</pre>

### Ceas 原理<http://groups.google.com/group/ceas-announcement/browse_thread/thread/68ef5cacd80845cc>

CEAS bins every gene by a user specific &#8211;pf-res (default = 50 bp).  
Then, it calculates the representative signal value of each bin.

For example, suppose the wig file is as follow.

1 20  
26 30  
51 25  
76 15

CEAS makes two bins [1, 50) and [51, 100) when --pf-res = 50bp. and  
then calculates the representative signal values, 25 and 20 when  
median is used.

Then, CEAS decimates or interpolates the signal according to the ratio  
between the gene length and the reference gene length, 3000bp. For  
example, when a gene length is 6000 bp, CEAS merges two bins to be  
one, making the total bin number be 60. (a total of 60 bins when  
3000bp and --pf-res=50). When a gene length is 1500bp, CEAS does zero-  
hold interpolation, making the total bin number be 60 as well. (before  
interpolation, the total bin number is 30 when the gene length 1500bp  
and --pf-res=50)

Finally, CEAS takes the average of length-normalized profiles.

## HCP, ICP, LCP

Promoters containing a 500-bp interval within -0.5?kb to +2?kb with a (G+C)-fraction?≥0.55 and a CpG observed to expected ratio (O/E)?≥0.6 were classified as HCPs. Promoters containing no 500-bp interval with CpG O/E?≥0.4 were classified as LCPs. The remainder were classified as ICPs.

## SISSRS

下载，[ http://sissrs.rajajothi.com][9]，解压之后直接运行。需要bed格式的文件。

基本使用见网站的手册

<pre class="brush: bash; title: ; notranslate" title="">scissrs.pl -i input.bed -o output input.scissrs -s genome_size

hg18:308ooooooo

-F The average length of the seq picked by gel after sonication to be sequenced

-L The maximum length of the seq picked by gel after sonication to be sequenced

-m Fraction of genome mapped by reads [default 0.8]. This can be got by analyzing the result of genomeCovergeBed.

-E Number of directional reads required within F base pairs on either side of the inferred binding site. The higher the E, more specific. Default 2 for 2-5 million reads

-a Only one read per genomic position is kept [remove duplicates, if it has been done before, no need here]

-q ignore.3col.bed  忽略文件中的区域,文件格式chrom1 start end

&lt;strong&gt;perl sissrs.pl -i xxx.bed -o sissrs.bed -s 3080000000 -F 50 -L 100 -w 50 -b control.bed&lt;/strong&gt;</pre>

why background control data is more reliable?[sissr manual]

These are several open chromatin regions in the genome that bind many proteins in a non-specific manner.

## CCAT

### http://cmb.gis.a-star.edu.sg/ChIPSeq/paperCCAT.htm

histone modification

## FindPeaks

http://sourceforge.net/apps/mediawiki/vancouvershortr/index.php?title=VSRAPBuilding

# Annotation

## ChIPpeakAnno

http://www.bioconductor.org/packages/2.5/bioc/html/ChIPpeakAnno.html

安装：

<pre class="brush: bash; title: ; notranslate" title="">source("http://bioconductor.org/biocLite.R")
biocLite("ChIPpeakAnno")</pre>

Great

http://great.stanford.edu/

# Homer

Install:

download\-----configure.pl\--- configure.pl list\---\-----configure.pl -install mm9

annotatePeaks.pl bed mm9 [The name column aka the 4th column can not start with numbers]

homer heatmap http://biowhat.ucsd.edu/homer/chipseq/heatmap.html

# Normalize by input

http://www.biostars.org/p/49775/#50320

# Diff-comp

## DiffBind

http://www.bioconductor.org/packages/devel/bioc/html/DiffBind.html

1.Detection of OSKM Differentially Bound Regions  
A sliding window (size 1Mb, step size 10kb) was used to assess the genome-wide distribution of OSKM enrichment at 48 hr. For each  
window, the number of tags of Oct4, Sox2, Klf4, and c-Myc was normalized for sequencing and sonication efficiency biases as  
described elsewhere. Windows were scored with the maximum normalized tag count out of the four factors. If a window’s score  
was beneath the fifteenth percentile value for all window scores, it was considered OSKM-depleted, and overlapping depleted  
windows were merged. A similar procedure was performed for OSKM enrichment in ES cells (Lister et al., 2009), and regions depleted  
for OSKM in both ES cells and at 48hrs were removed from consideration. The remaining regions were design ated ‘‘OSKM-Differ-entially Bound Regions’’ or OSKM-DBRs. Sixty additional DBRs curated by visual inspection were added to this initial set. 

2.Merge peaks called by MACS

3.http://seqanswers.com/forums/showthread.php?t=17175

## chip-diff

http://cmb.gis.a-star.edu.sg/ChIPSeq/tools.htm

Profile

1.HTSseq: <http://www-huber.embl.de/users/anders/HTSeq/doc/install.html>

安装Numpy:<http://www.scipy.org/Installing_SciPy/Linux>

python setup.py install --user #安装在自己的家目录，并且可以直接使用

安装HTSeq

python setup.py install --user

# Pipeline Software

## ChIP-seq processing pipeline

http://compbio.med.harvard.edu/Supplements/ChIP-seq/

## CISGENOME

## Seqminer

http://sourceforge.net/projects/seqminer/

## Another heatmap profile tools

<a href="http://code.google.com/p/ibm-cbc-genomic-tools/" target="_blank">http://code.google.com/p/ibm-cbc-genomic-tools/</a>

http://rsat.ulb.ac.be/~sylvain/binding\_profiles/binding\_profiles_form.php?demo=1

## GALAXY

安装见说明

使用： sh run.sh --reload

# Assist Software

## Mercurial， hg

安装见软件包内说明

用途：下载最新的软件包

# SAM文件解析

1.Reads with flag 0 are mapped to the forward strand and the reads with flag are mapped to the reverse strand. The reads with flag 4 are unmapped. [[Detail][10]] I understand that the FLAG of 4, with aligned chromosomal coordinates indicates an alignment possibly spanning across multiple chromosomes. One can compute the end position of that mapped reads to see id it is larger than the length of the chromosome.

2.MAPQ, the probability of the wrong mapping is 10 ** (-mapq/10) [[DEATIL][11]] A mapping quality of 10 or less indicates that there is at least a 1 in 10 chance that the read truly originated elsewhere. [Bowtie 2 manual] MAPQ == 0 indicates the read could not be mapped unambiguously to the ref genome.

3.In the context of SAM/BAM, and "pair" is two reads from either end of the same fragment of DNA; the "mate" is the partner read in a pair of reads. Thus if you are looking at the forward or /1 read, the mate is the reverse or /2 read, and vice versa). The pair is the combination of the forward and reverse reads (or the /1 and /2 reads depending on your naming convention).

4.I ran some simulations with bwa in Single End Mapping and it really depends on the read length and the number of mismatches. Also the mapq value of BWA ALN (the short aligner) you should use MapQ > 30 anything less than that you pretty much cannot trust. If you use bwasw you can use a MapQ of 10. These 2 settings should give you >99% accuracy in the mapping, specially if you increase the sensitivity in BWASW (Z > 100). This however is for Single End mapping not Paired End mapping. More simulations [here（http://lh3lh3.users.sourceforge.net/alnROC.shtml][12]）。

Data Source:

<http://www.roadmapepigenomics.org/data>

# TIPs

1.在后台运行多个map操作或其它有输出日志的文件时，最好使用错误重定向建立运行日志文件，来记录运行状态。

2.编写的程序最好可以自己把运行的参数，开始时间，结束时间，文件是否成功生成记录进入结果文件。更多见[程序编写规范记录][13]

3.程序运行时间较长，且运行时会输出东西，最好可以记录程序的输出，保存有用信息。

4.看结果文件要看全，仔细检查命令的输出。

Questions：

1.The cross-linked DNA fragments are sequenced from the end while the actual binding site might be anywhere within the immuno-precipitated fragments。

2.Coverage

Unfortunately, it does depend. It depends at least on the enrichment of the antibody over background and on the binding pattern of the TF across the genome. Antibodies with lower (only a few fold) enrichment or TFs with a promiscuous binding pattern (bind all over the place) will require more reads. However, without any other information, a few million reads (a lane, for example) is a place to start. From there, you can do some virtual experiments to look at the added benefit of more reads by subsampling your data at various levels and observing the increase in numbers of sites picked up with increased coverage. If you see a plateau in the sites versus reads, then you are probably close to the number of reads that you need. <http://biostar.stackexchange.com/questions/3711/what-coverage-is-required-for-chip-seq-experiments>

3.extend

Transcription factor binding sites are located somewhere on original DNA fragment .

# Experiment Design

*   Try to use pair-end reads (if possible at least 70bp). It helps estimating the fragment size. The size you cut the gel is one parameter. But there are some biases in other steps of the process (e.g. when fragment are amplified for sequencing). As a result you have a 'convolution' of several probability distribution functions and the true average fragment length may be different from the size you selected. If single end reads are provided, the algorithm tries to determine the fragment size by using reads mapped to positive and negative strands. If you have pair-ends, then the fragment was sequenced from both ends, so you know the fragment size..

*   Have one 'control' per experiment (i.e. one sample that skips the IP part and it's sequenced).
*   If you don't blindly trust your antibody, perform biological replicates (yes, I know it costs twice as much).
*   Filter out low quality mapped reads (e.g mapq < 20)
*   Make sure your algorithm treats multiple mapping reads properly, or filter them out.
*   If you use MACS, make sure you run it multiple times using different min\_fold parameters (and sometimes you must tune max\_fold as well). Once you tunes MACS, you can sub-sample your data and re-run MACS (e.g. sub sample 60%, 65%, 70%,..., 95%). If you see that the number of peaks is constantly increasing, this may give you a hint that you need more sequencing. On the other hand, if you see a 'plateau', this means that you may have found "all the peaks".
*   Perform saturation plots to see if you need more sequencing. [ref <http://biostar.stackexchange.com/questions/11240/are-chip-seq-replicate-data-used-as-controls>]

Mononucleosomal sized DNA works fine for ChIP-Seq. You have to remember that you add about 70bp to the DNA size with the adaptor ligation. Mononucleosome DNA is 147bp + aprox. 70 bp (Illumina adaptors - check this I'm not sure exactly) gives you about 220 bp of DNA which is exactly what is optimal for Illumina sequencing. [<http://seqanswers.com/forums/showthread.php?t=9929>]

\---\---\---Untested tools and docs \---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---\---

[This software is designed to analyze and compare ChIP-Seq data][14]  
**Sole-Search tool**: Determines **statistically significant peaks** from ChIP experiments sequenced by an Illumina Genome Analyzer (ChIP-Seq). This analysis software includes several secondary background models from which to choose or an option to enter your own input file, for determining significance over a cell type-specific background. It <span style="color: #ff6600;">determines duplication and deletion events</span> within the cell type of interest, as well as regions of sequence bias, and normalized the ChIP-seq sample. <span style="color: #ff6600;">Peak height cutoff is determined based on a user-defined FDR</span>. A new option allows the user to more easily and accurately determine regions of <span style="color: #ff00ff;">histone modifications</span>. Output from the Illumina Genome Analyzer is processed. Software produces run statistics, visualization files of raw data, and a significant peaks file.

**GFF-Overlap tool**: Determines overlap of binding sites between two data sets. User can compare two peak files in GFF format from either ChIP-Chip arrays, ChIP-Seq experiments or a combination of the two. The software determines the overlap between the two files with allotted gap; peaks can overlap completely, or overlap can be determined based on a user-defined gap between peaks. Output is an overlap file, a no overlap file, and a union file, in GFF format.

**Location-Analysis tool**: Determines location of a binding site, from a peak file in GFF format, with respect to the nearest gene. Output of the software gives the name and coordinates of the gene nearest the binding site, distance from TSS, gene annotation where applicable, etc.

**GFF-to-FASTA tool**: Gives the user sequence information in FASTA format for any file in GFF format. FASTA file can then be used in an external motif-calling program.

[<span style="text-decoration: underline;"><strong>Genplay</strong></span>][15]

<span style="text-decoration: underline;"><strong>http://genplay.einstein.yu.edu/wiki/index.php/ChIP-Seq_Tutorial</strong></span>

## <span style="text-decoration: underline;"><strong><br /> </strong></span>

## Tutorial

http://ged.msu.edu/angus/

## Other tools

http://www.icanplot.org/

\---\---\---\---\---\---

ref:

http://www.biostat.jhsph.edu/~lichen1/hmChIP/ChIP-seq.html

http://regulatorygenomics.upf.edu/group/media/pyicos_docs/command.html#convert

<a href="http://www.biostars.org/post/show/2699/how-can-i-convert-bamsam-to-wiggle/" target="_blank">http://www.biostars.org/post/show/2699/how-can-i-convert-bamsam-to-wiggle/</a>

https://bitbucket.org/cistrome/cistrome-harvard/wiki/Tutorial\_for\_Cistrome\_AP\_installation

http://sourceforge.net/apps/mediawiki/vancouvershortr/index.php?title=Main_Page

 [1]: http://210.75.224.29/wordpress/?p=1556 "使用Aspera从EBI或NCBI下载基因组数据"
 [2]: www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=announcement "www.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=announcement"
 [3]: http://210.75.224.29/wordpress/?p=1558 "Ubuntu 11.10 下安装 JDK_6_27"
 [4]: http://www.bioinformatics.bbsrc.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/2%20Per%20Base%20Sequence%20Quality.html
 [5]: http://hannonlab.cshl.edu/fastx_toolkit/commandline.html#fastx_collapser_usage
 [6]: en.wikipedia.org/wiki/FASTQ_format
 [7]: http://seqanswers.com/forums/showthread.php?t=4731
 [8]: http://groups.google.com/group/bedtools-discuss/browse_thread/thread/dc289b9a5a887560
 [9]: http://sissrs.rajajothi.com
 [10]: http://www.bits.vib.be/wiki/index.php/.sam
 [11]: http://biostar.stackexchange.com/questions/15217/how-mapq-in-bwa-is-calculated
 [12]: http://lh3lh3.users.sourceforge.net/alnROC.shtml
 [13]: http://210.75.224.29/wordpress/?p=1705 "程序编写规范记录"
 [14]: http://havoc.genomecenter.ucdavis.edu/cgi-bin/chipseq.cgi
 [15]: http://genplay.einstein.yu.edu/wiki/index.php/ChIP-Seq_Tutorial