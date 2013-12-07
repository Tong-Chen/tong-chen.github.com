---
title: How to tell which library type to use (fr-firststrand or fr-secondstrand)
author: 悟道
layout: post
categories:
  - seq
  - letter
  - NGS
tags:
  - bioinformatics
  - rna-seq
---

<div>
</div>

<div>
  First of all, as a bioinformatian, you should ask the data producer (e.g. the one who prepared the RNAseq library) which protocol they used to generate the data.Tophat manual page has listed the general strand-specific protocol:</p> <table cellspacing="15">
    <tr>
      <td valign="top" nowrap="nowrap">
        <strong>Library Type</strong>
      </td>
      
      <td valign="top" nowrap="nowrap">
        <strong>Examples</strong>
      </td>
      
      <td valign="top">
        <strong>Description</strong>
      </td>
    </tr>
    
    <tr>
      <td valign="top" nowrap="nowrap">
        fr-unstranded
      </td>
      
      <td valign="top" nowrap="nowrap">
        <tt>Standard Illumina</tt>
      </td>
      
      <td valign="top">
        Reads from the left-most end of the fragment (in transcript coordinates) map to the transcript strand, and the right-most end maps to the opposite strand.
      </td>
    </tr>
    
    <tr>
      <td valign="top" nowrap="nowrap">
        fr-firststrand
      </td>
      
      <td valign="top" nowrap="nowrap">
        <tt>dUTP, NSR, NNSR</tt>
      </td>
      
      <td valign="top">
        Same as above except we enforce the rule that the right-most end of the fragment (in transcript coordinates) is the first sequenced (or only sequenced for single-end reads). Equivalently, it is assumed that only the strand generated during first strand synthesis is sequenced.
      </td>
    </tr>
    
    <tr>
      <td valign="top" nowrap="nowrap">
        fr-secondstrand
      </td>
      
      <td valign="top" nowrap="nowrap">
        <tt>Ligation, Standard SOLiD</tt>
      </td>
      
      <td valign="top">
        Same as above except we enforce the rule that the left-most end of the fragment (in transcript coordinates) is the first sequenced (or only sequenced for single-end reads). Equivalently, it is assumed that only the strand generated during second strand synthesis is sequenced.
      </td>
    </tr>
  </table>
  
  <p>
    In case you don&#8217;t know the library-type, you can still figure it out by yourself. Tophat FAQ page provided a solution for that (http://tophat.cbcb.umd.edu/faq.html#library_type). But more simply (comparing to running 1M reads first), you can choose few reads and BLAT to genome and infer the library-type from the mapping result.
  </p>
  
  <p>
    Generally, reads from the left-most end of RNA fragment (always from 5´ to 3´) are always mapped to transcript-strand, and (for pair-end sequencing) reads from the right-most end are always mapped to the opposite strand. See the arrows direction in the below schema. This is because the sequencer always read from 5´ to 3´.
  </p>
  
  <div>
  </div>
  
  <div>
    <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/project+log+bu_hd+1.png"><img class="aligncenter size-thumbnail wp-image-2578" title="project+log+(bu_hd)+(1)" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/project+log+bu_hd+1-150x150.png" alt="" width="150" height="150" /></a>
  </div>
  
  <table cellspacing="0" cellpadding="0" align="center">
    <tr>
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        <table cellspacing="0" cellpadding="0" align="center">
          <tr>
            <td>
              Summary of library type protocols (for Tophat/Bowtie)
            </td>
          </tr>
        </table>
      </td>
    </tr>
  </table>
  
  <p style="text-align: center;">
    But regarding to which strand the RNA fragment is synthesized from, this involves different strand-specific protocols. Thanks to the illustration figure (see below) from Zhao Zhang, we could see that for example dUTP method is to only sequence the strand from the first strand synthesis (the original RNA strand is  degradated due to the dUTP incorporated), so the /2 read is from the original RNA strand.<br /> <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/strand.png"><img class="aligncenter size-thumbnail wp-image-2579" title="strand" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/strand-150x150.png" alt="" width="150" height="150" /></a>
  </p>
  
  <table cellspacing="0" cellpadding="0" align="center">
    <tr>
      <td>
      </td>
    </tr>
    
    <tr>
      <td>
        Strand-specific library protocols (Credit: Zhao Zhang)
      </td>
    </tr>
  </table>
  
  <p>
    Taking a real example, first getting some reads (in fasta format) from the paired-end sequencing fastq file using command like:
  </p>
  
  <p>
    $ zcat ~/nearline/rnaseq/BU/Jul2012/Sample_3576_H_01.R1.fastq.gz | sed &#8216;s/@//g;s/ /_/g&#8217; | awk &#8216;{if(NR%4==1)print &#8220;>&#8221;$0;if(NR%4==2) print $0;}&#8217; | head
  </p>
  
  <p>
    $ zcat ~/nearline/rnaseq/BU/Jul2012/Sample_3576_H_01.R2.fastq.gz | sed &#8216;s/@//g;s/ /_/g&#8217; | awk &#8216;{if(NR%4==1)print &#8220;>&#8221;$0;if(NR%4==2) print $0;}&#8217; | head
  </p>
  
  <p>
    Blatting them in UCSC Genome Browser
  </p>
  
  <div>
  </div>
</div>

<div>
</div>

<div>
  <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/screen+shot+2012-07-30+at+4.27.10+pm.png"><img class="aligncenter size-thumbnail wp-image-2580" title="screen+shot+2012-07-30+at+4.27.10+pm" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/screen+shot+2012-07-30+at+4.27.10+pm-150x150.png" alt="" width="150" height="150" /></a>
</div>

<div>
  Below is screenshot for top hits of one pair of reads. They mapped to exons of OS9 genes (the left one is /1 and right one is /2, with opposite direction). We see that /1 mapped to transcript direction, /2 mapped to opposite direction, which means it can only be fr-secondstrand or fr-unstrand (cannot be fr-firststrand).</p> <div>
  </div>
  
  <div>
  </div>
  
  <div>
     <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/1.png"><img class="aligncenter size-thumbnail wp-image-2581" title="1" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/1-150x131.png" alt="" width="150" height="131" /></a>
  </div>
  
  <div>
  </div>
  
  <div>
  </div>
  
  <p>
    Continuing to look at other reads in the file, we can find examples like these:
  </p>
  
  <div>
  </div>
  
  <div>
     <a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/21.png"><img class="aligncenter size-thumbnail wp-image-2583" title="2" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/21-150x111.png" alt="" width="150" height="111" /></a><a href="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/3.png"><img class="aligncenter size-thumbnail wp-image-2584" title="3" src="http://210.75.224.29/wordpress/wp-content/uploads/2012/10/3-150x91.png" alt="" width="150" height="91" /></a>
  </div>
  
  <div>
  </div>
</div>

<div>
</div>

<div>
  where /2 mapped to transcript strand and /1 mapped to the opposite strand. Combining with the observation from above, we can conclude that this is a fr-unstrand library.
</div>
