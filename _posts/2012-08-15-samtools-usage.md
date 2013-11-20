---
title: SAMTools usage
author: 悟道
layout: post
permalink: /?p=2379
categories:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

# **<a accesskey="2" title="refresh" href="http://davetang.org/wiki/tiki-index.php?page=SAMTools">SAMTools</a>**

SAMTools provides various tools for manipulating alignments in the SAM format. The SAM (Sequence Alignment/Map) format is currently the *de facto* standard for storing large nucleotide sequence alignments. If you are dealing with high-throughput genomics or transcriptomics data, at some point you will probably have to deal with SAM files.

Here I just list some basic commands to get your started; to see an example of using SAMTools have a look at [this page][1].

<div id="toc">
  <div id="toctitle">
    <h3>
      Table of contents
    </h3>
  </div>
  
  <ul>
    <ul>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Basic_usage">Basic usage</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Converting_a_SAM_file_to_a_BAM_file">Converting a SAM file to a BAM file</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Sorting_a_BAM_file">Sorting a BAM file</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#SAM_directly_to_a_sorted_BAM_file">SAM directly to a sorted BAM file</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Creating_a_BAM_index_file">Creating a BAM index file</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Converting_a_BAM_file_to_a_SAM_file">Converting a BAM file to a SAM file</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Extracting_SAM_entries_mapping_to_a_specific_loci">Extracting SAM entries mapping to a specific loci</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Simple_stats_using_samtools_flagstat">Simple stats using samtools flagstat</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Interpreting_the_BAM_flags">Interpreting the BAM flags</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Extracting_only_the_first_read_from_paired_end_BAM_files">Extracting only the first read from paired end BAM files</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Filtering_out_unmapped_reads_in_BAM_files">Filtering out unmapped reads in BAM files</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#Creating_FASTQ_files_from_a_BAM_file">Creating FASTQ files from a BAM file</a>
      </li>
      <li>
        <a href="http://davetang.org/wiki/tiki-index.php?page=SAMTools#More_information">More information</a>
      </li>
    </ul>
  </ul>
</div>

### Basic usage {#Basic_usage}

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox">samtools &lt;command&gt; [options]</pre>
</div>

If you run samtools without any commands, all the available utilities are listed:

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox1">Program: samtools (Tools for alignments in the SAM format)
Version: 0.1.18 (r982:295)

Usage:   samtools &lt;command&gt; [options]

Command: view        SAM&lt;-&gt;BAM conversion
         sort        sort alignment file
         mpileup     multi-way pileup
         depth       compute the depth
         faidx       index/extract FASTA
         tview       text alignment viewer
         index       index alignment
         idxstats    BAM index stats (r595 or later)
         fixmate     fix mate information
         flagstat    simple stats
         calmd       recalculate MD/NM tags and '=' bases
         merge       merge sorted alignments
         rmdup       remove PCR duplicates
         reheader    replace BAM header
         cat         concatenate BAMs
         targetcut   cut fosmid regions (for fosmid pool only)
         phase       phase heterozygotes</pre>
</div>

Most of the times I just use view, sort, index and flagstats.

### Converting a SAM file to a BAM file {#Converting_a_SAM_file_to_a_BAM_file}

A BAM file is just a SAM file but stored in binary; you should always convert your SAM files into BAM to save storage space and BAM files are faster to manipulate.

To get started, take a peak at your SAM file by typing on the terminal/command prompt:

<div>
  <div>
    shell
  </div>
  
  <pre dir="ltr" id="codebox2">head test.sam</pre>
</div>

The first 10 lines on your terminal after typing &#8220;head test.sam&#8221;, should be lines starting with the &#8220;@&#8221; sign, which is an indicator for a header line. If you don&#8217;t see lines starting with the &#8220;@&#8221; sign, the header information is most likely missing.

If the header information is absent from the SAM file use the command below, where reference.fa is the reference fasta file used to map the reads:

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox3">samtools view -bT reference.fa test.sam &gt; test.bam</pre>
</div>

If the header information is available:

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox4">samtools view -bS test.sam &gt; test.bam</pre>
</div>

### Sorting a BAM file {#Sorting_a_BAM_file}

Always sort your BAM files; many downstream programs only take sorted BAM files.

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox5">samtools sort test.bam test_sorted</pre>
</div>

### SAM directly to a sorted BAM file {#SAM_directly_to_a_sorted_BAM_file}

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox6">samtools view -bS file.sam | samtools sort - file_sorted</pre>
</div>

### Creating a BAM index file {#Creating_a_BAM_index_file}

A BAM index file is usually needed when visualising a BAM file.

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox7">samtools index test_sorted.bam test_sorted.bai</pre>
</div>

### Converting a BAM file to a SAM file {#Converting_a_BAM_file_to_a_SAM_file}

Note: remember to use -h to ensure the converted SAM file contains the header information. Generally, I suggest storing only sorted BAM files as they use much less disk space and are faster to process.

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox8">samtools view -h NA06984.chrom16.ILLUMINA.bwa.CEU.low_coverage.20100517.bam &gt; NA06984.chrom16.ILLUMINA.bwa.CEU.low_coverage.20100517.sam</pre>
</div>

### Extracting SAM entries mapping to a specific loci {#Extracting_SAM_entries_mapping_to_a_specific_loci}

Quite commonly, we want to extract all reads that map within a specific genomic loci.

First make a BED file, which in its simplest form is a tab-delimited file with 3 columns. Say you want to extract reads mapping within the genomic coordinates 250,000 to 260,000 on chromosome 1. Then your BED file (which I will call test.bed) will be:

<table>
  <tr>
    <td>
      chr1
    </td>
    
    <td>
      250000
    </td>
    
    <td>
      260000
    </td>
  </tr>
</table>

Then run samtools as such:

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox9">samtools view -L test.bed test.bam | awk '$2 != 4 {print}'
OR
samtools view -S -L test.bed test.sam | awk '$2 != 4 {print}'</pre>
</div>

Note: even if you put strand information into your BED file, the above command ignores strandedness, so you get all reads mapping within the region specified by the BED file, regardless of whether it maps to the positive or negative strand. The AWK line above is to remove unmapped reads, which also get returned.

### Simple stats using samtools flagstat {#Simple_stats_using_samtools_flagstat}

I downloaded a test BAM file from <a href="ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/data/NA06984/alignment/NA06984.chrom20.ILLUMINA.bwa.CEU.low_coverage.20111114.bam" target="_blank">ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/data/NA06984/alignment/NA06984.chrom20.ILLUMINA.bwa.CEU.low_coverage.20111114.bam<img title="(external link)" alt="(external link)" src="http://davetang.org/wiki/styles/strasa/img/icons/external_link.gif" width="15" height="14" /></a>

<div>
  <div>
    samtools flagstat
  </div>
  
  <pre dir="ltr" id="codebox10">samtools flagstat NA06984.chrom20.ILLUMINA.bwa.CEU.low_coverage.20111114.bam</pre>
</div>

6874858 in total  
0 QC failure  
90281 duplicates  
6683299 mapped (97.21%)  
6816083 paired in sequencing  
3408650 read1  
3407433 read2  
6348470 properly paired (93.14%)  
6432965 with itself and mate mapped  
191559 singletons (2.81%)  
57057 with mate mapped to a different chr  
45762 with mate mapped to a different chr (mapQ>=5)

Here&#8217;s a paired entry for a proper pair:

SRR035022.16660180 163 20 59993 29 51S25M = 60065 147 TCCCACTTTGAACAGAATTTTTAAGAGAAAAAACTGAAAGTTAATAGAGAGGTGACTCAGATCCAGAGGTGGAAGA @EFEB@E@@FEHFHGGJIDDEDHKIIIHKKKGFDKJIKKIIEDKHGJFGBIJGKIILIJIIJIJIFDHGCECBC@? MD:Z:0N0N0N0N0N0N0N0N17 RG:Z:SRR035022 AM:i:29 NM:i:8 SM:i:29 XN:i:8MQ:i:29 XT:A:M BQ:Z:@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@URUSRTPOJ@@@@@@@@@@@@@@@@  
SRR035022.16660180 83 20 60065 29 76M = 59993 -147 TCCTGGCCCTAAACAGGTGGTAAGGAAGGAGAGAGTGAAGGAACTGCCAGGTGACACACTCCCACCATGGACCTCT ;>=BFEG?<BDBFIKLEKKJHFKKJDMKJIJLJMIKAFJKJFIIJJK?KKIHGIJIJIIIHJJHJJEIJHHIEDDB X0:i:1 X1:i:0 MD:Z:76 RG:Z:SRR035022 AM:i:29 NM:i:0 SM:i:29 MQ:i:29  
XT:A:U BQ:Z:@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

Here&#8217;s an entry without a proper pair, i.e. no corresponding pair:

SRR035025.11029198 145 20 60018 37 76M hs37d5 17693629 0 GGAAGGAAGCTTGGAACCCTATAGAGTTGCTGAGTGCCAGGACCAGATCCTGGCCCTAAACAGGTGGTAAGGAAGG 5>;>B<?A=>;GHCCGH>IHIHKHKHJHIIKHKHJJJKLJIEJJLIIIJIJJIJDIHDDHIJHFGFDD@DA@?GF@ X0:i:1 X1:i:0 MD:Z:76 RG:Z:SRR035025 AM:i:37 NM:i:0 SM:i:37  
XT:A:U BQ:Z:@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@A@

See below for how to interpret BAM flags

For more statistics of SAM or BAM files have a look at the [SAMStat][2] program.

### Interpreting the BAM flags {#Interpreting_the_BAM_flags}

The second column in a SAM/BAM file is the flag column. They may seem confusing at first but the encoding allows details about a read to be stored by just using a few digits. The trick is to convert the numerical digit into binary, and then use the table to interpret the binary numbers, where 1 = true and 0 = false.

Here are some common BAM flags:

163: 10100011 in binary  
147: 10010011 in binary  
99: 1100011 in binary  
83: 1010011 in binary

Interpretation of 10100011 (reading the binary from left to right):

<table>
  <tr>
    <td>
      1
    </td>
    
    <td colspan="2">
      the read is paired in sequencing, no matter whether it is mapped in a pair
    </td>
  </tr>
  
  <tr>
    <td>
      1
    </td>
    
    <td colspan="2">
      the read is mapped in a proper pair (depends on the protocol, normally inferred during alignment)
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td colspan="2">
      the query sequence itself is unmapped
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td colspan="2">
      the mate is unmapped
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td colspan="2">
      strand of the query (0 for forward; 1 for reverse strand)
    </td>
  </tr>
  
  <tr>
    <td>
      1
    </td>
    
    <td colspan="2">
      strand of the mate
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td colspan="2">
      the read is the first read in a pair
    </td>
  </tr>
  
  <tr>
    <td>
      1
    </td>
    
    <td colspan="2">
      the read is the second read in a pair
    </td>
  </tr>
</table>

163 second read of a pair on the positive strand with negative strand mate  
147 second read of a pair on the negative strand with positive strand mate  
99 first read of a pair on the forward strand with negative strand mate  
83 first read of a pair on the reverse strand with positive strand mate

IF you observe a BAM flag of 512 (0&#215;200), it indicates a read that did not pass quality control.

Below is a very raw Perl script that may help interpret BAM flags. I make the assumption that when a read or its mate is not flagged as unmapped (i.e. having a 0 value), there is information regarding its strandedness. Also if a read is flagged as not having a proper pair, I ignore the flags that store information for the mate.

<div>
  <div>
    bam_flag.pl
  </div>
  
  <pre dir="ltr" id="codebox11">#!/usr/bin/perl

use strict;
use warnings;

my $usage = "Usage: $0 &lt;bam_flag&gt;\n";
my $bam_flag = shift or die $usage;

my $binary = dec2bin($bam_flag);
$binary = reverse($binary);

#163 -&gt; 10100011

my @desc = (
'The read is paired in sequencing',
'The read is mapped in a proper pair',
'The query sequence itself is unmapped',
'The mate is unmapped',
'strand of the query',
'strand of the mate',
'The read is the first read in a pair',
'The read is the second read in a pair',
'The alignment is not primery (a read having split hits may have multiple primary alignment records)',
'The read fails quality checks',
'The read is either a PCR duplicate or an optical duplicate',
);

my $query_mapped = '0';
my $mate_mapped = '0';
my $proper_pair = '0';

print "$binary\n";

for (my $i=0; $i&lt; length($binary); ++$i){
   my $flag = substr($binary,$i,1);
   #print "\$i = $i and \$flag = $flag\n";
   if ($i == 1){
      if ($flag == 1){
         $proper_pair = '1';
      }
   }
   if ($i == 2){
      if ($flag == 0){
         $query_mapped = '1';
      }
   }
   if ($i == 3){
      if ($flag == 0){
         $mate_mapped = '1';
      }
   }
   if ($i == 4){
      next if $query_mapped == 0;
      if ($flag == 0){
         print "The read is mapped on the forward strand\n";
      } else {
         print "The read is mapped on the reverse strand\n";
      }
   } elsif ($i == 5){
      next if $mate_mapped == 0;
      next if $proper_pair == 0;
      if ($flag == 0){
         print "The mate is mapped on the forward strand\n";
      } else {
         print "The mate is mapped on the reverse strand\n";
      }
   } else {
      if ($flag == 1){
         print "$desc[$i]\n";
      }
   }
}

exit(0);

#from The Perl Cookbook
sub dec2bin {
   my $str = unpack("B32", pack("N", shift));
   $str =~ s/^0+(?=\d)//;   # otherwise you'll get leading zeros
   return $str;
}

__END__</pre>
</div>

### Extracting only the first read from paired end BAM files {#Extracting_only_the_first_read_from_paired_end_BAM_files}

Sometimes you only want the first pair of a mate

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox12">samtools view -h -f 0x0040 test.bam &gt; test_first_pair.sam</pre>
</div>

0&#215;0040 is hexadecimal for 64 (i.e. 16 * 4), which is binary for 1000000, corresponding to the read in the first read pair.

### Filtering out unmapped reads in BAM files {#Filtering_out_unmapped_reads_in_BAM_files}

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox13">samtools view -h -F 4 blah.bam &gt; blah_only_mapped.sam</pre>
</div>

### Creating FASTQ files from a BAM file {#Creating_FASTQ_files_from_a_BAM_file}

I found this great tool at <a href="http://www.hudsonalpha.org/gsl/software/bam2fastq.php" target="_blank">http://www.hudsonalpha.org/gsl/software/bam2fastq.php<img title="(external link)" alt="(external link)" src="http://davetang.org/wiki/styles/strasa/img/icons/external_link.gif" width="15" height="14" /></a>

For example to extract ONLY unaligned from a bam file:

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox14">bam2fastq -o blah_unaligned.fastq --no-aligned blah.bam</pre>
</div>

To extract ONLY aligned reads from a bam file:

<div>
  <div>
    samtools
  </div>
  
  <pre dir="ltr" id="codebox15">bam2fastq -o blah_aligned.fastq --no-unaligned blah.bam</pre>
</div>

### More information {#More_information}

<a href="http://samtools.sourceforge.net/" target="_blank">http://samtools.sourceforge.net/<img title="(external link)" alt="(external link)" src="http://davetang.org/wiki/styles/strasa/img/icons/external_link.gif" width="15" height="14" /></a>

<a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_FAQ" target="_blank">http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_FAQ<img title="(external link)" alt="(external link)" src="http://davetang.org/wiki/styles/strasa/img/icons/external_link.gif" width="15" height="14" /></a>

http://davetang.org/wiki/tiki-index.php?page=SAMTools

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

&nbsp;

&nbsp;

1.Sort big BAM files

<pre class="brush: bash; title: ; notranslate" title="">A utility from novocraft is the best, but its license expires in 15 days, if I remember correctly. There is a multithreaded sort I implemented as a weekend project (in the "mt" branch), but it is not as efficient because fully parallelizing needs a reimplementation, while I only have the time for small modifications. With the samtools-mt, you can:

samtools sort -@ 8 -m 4G

Note that each thread will use about 4-4.5GB of memory in this setting, so make sure you have enough memory when pushing up "-m" and "-@".

Sorting a 100GB BAM takes a little more than 1 day as I remember. Multithreaded samtools saves you about half a day with 4-8 cores. Novocraft is even better.
</pre>

 [1]: http://davetang.org/wiki/tiki-index.php?page=SAM "SAM"
 [2]: http://davetang.org/wiki/tiki-index.php?page=SAMStat "SAMStat"