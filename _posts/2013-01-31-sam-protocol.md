---
title: sam protocol
author: 悟道
layout: post
permalink: /?p=2810
categories:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

# SAM protocol {#firstHeading}

<table id="toc" summary="Contents">
  <tr>
    <td>
      <div id="toctitle">
        <h2>
          Contents
        </h2>
        
        <p>
          [<a id="togglelink"></a>hide]
        </p>
      </div>
      
      <ul>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Abstract">1 Abstract</a>
        </li>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Introduction">2 Introduction</a>
        </li>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Basic_Protocol_1:_The_Sequence_Alignment.2FMap_.28SAM.29_Format">3 Basic Protocol 1: The Sequence Alignment/Map (SAM) Format</a>
        </li>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Basic_Protocol_2:_Generating_Alignments_for_One_Human_Individual">4 Basic Protocol 2: Generating Alignments for One Human Individual</a> <ul>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Necessary_resources">4.1 Necessary resources</a>
            </li>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Procedure">4.2 Procedure</a> <ul>
                <li>
                  <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Install_software">4.2.1 Install software</a>
                </li>
                <li>
                  <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Perform_alignment">4.2.2 Perform alignment</a>
                </li>
                <li>
                  <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Generate_merged_alignment">4.2.3 Generate merged alignment</a>
                </li>
                <li>
                  <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Index_alignment">4.2.4 Index alignment</a>
                </li>
              </ul>
            </li>
          </ul>
        </li>
        
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Basic_Protocol_3:_Variant_Calling_with_SAMtools">5 Basic Protocol 3: Variant Calling with SAMtools</a> <ul>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Necessary_resources_2">5.1 Necessary resources</a>
            </li>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Procedure_2">5.2 Procedure</a>
            </li>
          </ul>
        </li>
        
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Alternative_Protocol:_Variant_Calling_with_GATK">6 Alternative Protocol: Variant Calling with GATK</a> <ul>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Necessary_resources_3">6.1 Necessary resources</a>
            </li>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Procedure_3">6.2 Procedure</a>
            </li>
          </ul>
        </li>
        
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Support_Protocol_1:_Base_Quality_Recalibration">7 Support Protocol 1: Base Quality Recalibration</a>
        </li>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Support_Protocol_2:_Local_Realignment">8 Support Protocol 2: Local Realignment</a>
        </li>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Support_Protocol_3:_Assessing_coverage">9 Support Protocol 3: Assessing coverage</a>
        </li>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Support_Protocol_4:_Viewing_Alignment_with_IGV">10 Support Protocol 4: Viewing Alignment with IGV</a>
        </li>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Support_Protocol_5:_APIs_for_Accessing_Alignments_in_SAM.2FBAM">11 Support Protocol 5: APIs for Accessing Alignments in SAM/BAM</a> <ul>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#C_APIs_.28SAMtools-C.29">11.1 C APIs (SAMtools-C)</a>
            </li>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Java_APIs_.28Picard.29">11.2 Java APIs (Picard)</a>
            </li>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Perl_APIs_.28Bio-SamTools.29">11.3 Perl APIs (Bio-SamTools)</a>
            </li>
            <li>
              <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Python_APIs_.28Pysam.29">11.4 Python APIs (Pysam)</a>
            </li>
          </ul>
        </li>
        
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Commentary">12 Commentary</a>
        </li>
        <li>
          <a href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol#Literature_Cited">13 Literature Cited</a>
        </li>
      </ul>
    </td>
  </tr>
</table>

<a id="Abstract" name="Abstract"></a>

# Abstract

<a id="Introduction" name="Introduction"></a>

# Introduction

<a id="Basic_Protocol_1:_The_Sequence_Alignment.2FMap_.28SAM.29_Format" name="Basic_Protocol_1:_The_Sequence_Alignment.2FMap_.28SAM.29_Format"></a>

# Basic Protocol 1: The Sequence Alignment/Map (SAM) Format

In SAM, each alignment line has 11 mandatory fields and a variable number of optional fields. The mandatory fields must be present but their value can be a <tt>*</tt> or a zero (depending on the field) if the corresponding information is unavailable.

<table width="100%" border="2" rules="all" cellspacing="4" cellpadding="3">
  <caption align="top">Mandatory fields in SAM</caption> <caption align="bottom">Modified from Table 1 in Li <i>et al.</i> (2009)</caption> <tr>
    <th>
      Col
    </th>
    
    <th>
      Name
    </th>
    
    <th>
      Description
    </th>
  </tr>
  
  <tr>
    <td>
      1
    </td>
    
    <th>
      <tt>QNAME</tt>
    </th>
    
    <td>
      Query NAME of the read or the read pair
    </td>
  </tr>
  
  <tr>
    <td>
      2
    </td>
    
    <th>
      <tt>FLAG</tt>
    </th>
    
    <td>
      bitwise FLAG (pairing, strand, mate strand, etc.)
    </td>
  </tr>
  
  <tr>
    <td>
      3
    </td>
    
    <th>
      <tt>RNAME</tt>
    </th>
    
    <td>
      Reference sequence NAME
    </td>
  </tr>
  
  <tr>
    <td>
      4
    </td>
    
    <th>
      <tt>POS</tt>
    </th>
    
    <td>
      1-based leftmost POSition of clipped alignment
    </td>
  </tr>
  
  <tr>
    <td>
      5
    </td>
    
    <th>
      <tt>MAPQ</tt>
    </th>
    
    <td>
      MAPping Quality (Phred-scaled)
    </td>
  </tr>
  
  <tr>
    <td>
      6
    </td>
    
    <th>
      <tt>CIGAR</tt>
    </th>
    
    <td>
      extended CIGAR string (operations: <tt>MIDNSHP</tt>)
    </td>
  </tr>
  
  <tr>
    <td>
      7
    </td>
    
    <th>
      <tt>NRNM</tt>
    </th>
    
    <td>
      Mate Reference NaMe (`=&#8217; if same as <tt>RNAME</tt>)
    </td>
  </tr>
  
  <tr>
    <td>
      8
    </td>
    
    <td>
      <tt>MPOS</tt>
    </td>
    
    <td>
      1-based leftmost Mate POSition
    </td>
  </tr>
  
  <tr>
    <td>
      9
    </td>
    
    <th>
      <tt>ISIZE</tt>
    </th>
    
    <td>
      inferred Insert SIZE
    </td>
  </tr>
  
  <tr>
    <td>
      10
    </td>
    
    <th>
      <tt>SEQ</tt>
    </th>
    
    <td>
      query SEQuence on the same strand as the reference
    </td>
  </tr>
  
  <tr>
    <td>
      11
    </td>
    
    <th>
      <tt>QUAL</tt>
    </th>
    
    <td>
      query QUALity (ASCII-33=Phred base quality)
    </td>
  </tr>
</table>

<table width="100%" border="2" rules="all" cellspacing="4" cellpadding="3">
  <caption align="top">Bitwise flags in the <tt>FLAG</tt> field</caption> <tr>
    <th>
      Flag
    </th>
    
    <th>
      Description
    </th>
  </tr>
  
  <tr>
    <td>
      0&#215;0001
    </td>
    
    <td>
      Paired in sequencing
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0002
    </td>
    
    <td>
      Mapped in proper read pair
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0004
    </td>
    
    <td>
      Query unmapped
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0008
    </td>
    
    <td>
      Mate unmapped
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0010
    </td>
    
    <td>
      Strand of the query (1 for reverse)
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0020
    </td>
    
    <td>
      Strand of the mate (1 for reverse)
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0040
    </td>
    
    <td>
      First read in the pair
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0080
    </td>
    
    <td>
      Second read in the pair
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0100
    </td>
    
    <td>
      Secondary alignment
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0200
    </td>
    
    <td>
      QC failure
    </td>
  </tr>
  
  <tr>
    <td>
      0&#215;0400
    </td>
    
    <td>
      Optical or PCR duplicates
    </td>
  </tr>
</table>

<a id="Basic_Protocol_2:_Generating_Alignments_for_One_Human_Individual" name="Basic_Protocol_2:_Generating_Alignments_for_One_Human_Individual"></a>

# Basic Protocol 2: Generating Alignments for One Human Individual

<a id="Necessary_resources" name="Necessary_resources"></a>

## Necessary resources

Hardware
:   A computer with 64-bit CPU, 8GB or more memory and 100GB free disk space.

Software
:   Linux; <a title="http://www.gnu.org/software/wget/" href="http://www.gnu.org/software/wget/" rel="nofollow">wget</a>; C compiler (e.g. <a title="http://gcc.gnu.org/" href="http://gcc.gnu.org/" rel="nofollow">gcc</a>)

Files
:   Human genome sequences in one FASTA file (<tt>hsRef.fa</tt> in this example). Paired-end sequencing reads generated by Illumina GenomeAnalyzer in two FASTQ files, one for each end (<tt>ga1.fq</tt> and <tt>ga2.fq</tt>). Sequencing reads generated by Roche/454 in one FASTQ file (<tt>454.fq</tt>).

<a id="Procedure" name="Procedure"></a>

## Procedure

<a id="Install_software" name="Install_software"></a>

### Install software

<ol start="1">
  <li>
    Install samtools and <a title="http://bio-bwa.sourceforge.net" href="http://bio-bwa.sourceforge.net" rel="nofollow">bwa</a>. Sophisticated Unix users may copy the executables to any directory on the <tt>PATH</tt>. <pre>wget http://sourceforge.net/projects/bio-bwa/files/bwa-0.5.5.tar.bz2/download
wget http://sourceforge.net/projects/samtools/files/samtools/0.1.7/samtools-0.1.7a.tar.bz2/download
tar -jxf bwa-0.5.5.tar.bz2; tar -jxf samtools-0.1.7a.tar.bz2
(cd bwa-0.5.5; make; cp bwa $HOME/bin)
(cd samtools-0.1.7a; make; cp samtools misc/samtools.pl $HOME/bin)
export PATH="$PATH:$HOME/bin" # this is bash only.</pre>
    
    <p>
      Note that this example uses bwa-0.5.5 and samtools-0.1.7a, but latest versions are preferred. In addition, many other aligners also generate alignments in the SAM format (see <a title="http://samtools.sourceforge.net/swlist.shtml" href="http://samtools.sourceforge.net/swlist.shtml" rel="nofollow">this page</a> for a complete list). We only use bwa as an example.</li> </ol> <p>
        <a id="Perform_alignment" name="Perform_alignment"></a>
      </p>
      
      <h3>
        Perform alignment
      </h3>
      
      <ol start="2">
        <li>
          Index the genome. For the human genome, option <tt>-a bwtsw</tt> is required because the default <tt>is</tt> algorithm does not work with genomes longer than 2Gbp. It typically takes three hours for indexing. <pre>bwa index -a bwtsw hsRef.fa</pre>
        </li>
        
        <li>
          Align Illumina short reads to the reference genome, using the bwa-short read algorithm. <pre>bwa aln hsRef.fa ga1.fq &gt; ga1.sai
bwa aln hsRef.fa ga2.fq &gt; ga2.sai
bwa sampe hsref.fa ga1.sai ga2.sai ga1.fq ga2.fq | gzip &gt; ga.sam.gz</pre>
          
          <p>
            The first two command lines generate alignments in the suffix array coordinate for each end. The last command line pairs the two ends and produces the alignment in the compressed SAM format. The <tt>gzip</tt> output saves disk space but is optional. The input FASTQ files can be also compressed. Both <tt>bwa</tt> and <tt>samtools</tt> seamlessly work with uncompressed and gzip&#8217;ed input files.</li> <li>
              Align 454 reads to the reference genome, using the BWA-SW algorithm in bwa. This algorithm works with long reads, but does not support paired-end mapping. <pre>bwa bwasw hsRef.fa 454.fq | gzip &gt; 454.sam.gz</pre>
              
              <p>
                For large-scale data, step 3, 4 and 5 are usually parallelized across a compute cluster.</li> </ol> <p>
                  <a id="Generate_merged_alignment" name="Generate_merged_alignment"></a>
                </p>
                
                <h3>
                  Generate merged alignment
                </h3>
                
                <ol start="5">
                  <li>
                    Convert SAM to BAM and perform sorting. <pre>samtools view -uS ga.sam.gz | samtools sort - ga
samtools calmd -uS 454.sam.gz hsRef.fa | samtools sort - 454</pre>
                    
                    <p>
                      We use the <tt>calmd</tt> command to generate the <tt>NM</tt> and <tt>MD</tt> tags for each alignment which may be potentially useful to downstream analysis. The BWA-short algorithm writes these tags but BWA-SW does not.
                    </p>
                    
                    <p>
                      In both command lines, option <tt>-u</tt> renders samtools to output uncompressed BAM to reduce the computing time. An input file name `<tt>-</tt>&#8216; means the standard input. It is recommended to use samtools on a data stream to reduce disk space usage as well as the overall wall-clock time on processing the alignment.</li> <li>
                        Merge sorted alignments and remove potential PCR/optical duplicates. <pre>perl -e 'print "@RG\tID:ga\tSM:hs\tLB:ga\tPL:Illumina\n@RG\tID:454\tSM:hs\tLB:454\tPL:454\n"' &gt; rg.txt
samtools merge -rh rg.txt - ga.bam 454.bam | samtools rmdup - - | samtools rmdup -s - aln.bam</pre>
                        
                        <p>
                          The library information of each read group is kept in <tt>rg.txt</tt> which will be embedded in the header of <tt>aln.bam</tt>. The <tt>-r</tt> option of <tt>merge</tt> tells samtools to attach `<tt>RG:Z:ga</tt>&#8216; to each alignment in <tt>ga.bam</tt> and `<tt>RG:Z:454</tt>&#8216; to each alignment in <tt>454.bam</tt>.
                        </p>
                        
                        <p>
                          Removing duplicates is optional, but it helps to reduce false positives in SNP calling. However, duplicates removal for single-end reads is not recommended given very deep coverage as this step may discard too many good alignments.</li> </ol> <p>
                            <a id="Index_alignment" name="Index_alignment"></a>
                          </p>
                          
                          <h3>
                            Index alignment
                          </h3>
                          
                          <ol start="7">
                            <li>
                              Index the reference sequences and the alignment to enable fast retrieval of alignment or subsequence in a specified region. <pre>samtools faidx hsRef.fa
samtools index aln.bam</pre>
                              
                              <p>
                                File <tt>hsRef.fa.fai</tt> and <tt>aln.bam.bai</tt> will be created. After this step, alignment can be displayed in terminal with
                              </p>
                              
                              <pre>samtools tview aln.bam hsRef.fa</pre>
                            </li>
                          </ol>
                          
                          <p>
                            <a id="Basic_Protocol_3:_Variant_Calling_with_SAMtools" name="Basic_Protocol_3:_Variant_Calling_with_SAMtools"></a>
                          </p>
                          
                          <h1>
                            Basic Protocol 3: Variant Calling with SAMtools
                          </h1>
                          
                          <p>
                            <a id="Necessary_resources_2" name="Necessary_resources_2"></a>
                          </p>
                          
                          <h2>
                            Necessary resources
                          </h2>
                          
                          <dl>
                            <dt>
                              Hardware
                            </dt>
                            
                            <dd>
                              A computer with 100GB free disk space.
                            </dd>
                            
                            <dt>
                              Software
                            </dt>
                            
                            <dd>
                              Linux; samtools
                            </dd>
                            
                            <dt>
                              Files
                            </dt>
                            
                            <dd>
                              Reference sequences in one FASTA file (hsRef.fa in this example). Position sorted alignment in the BAM format (aln.bam).
                            </dd>
                          </dl>
                          
                          <p>
                            <a id="Procedure_2" name="Procedure_2"></a>
                          </p>
                          
                          <h2>
                            Procedure
                          </h2>
                          
                          <ol>
                            <li>
                              Get the raw variant calls on the X chromosome. Assume X chromosome is named <tt>X</tt> in both hsRef.fa and aln.bam. <pre>samtools view -u aln.bam X | samtools pileup -vcf hsRef.fa - &gt; var-X.raw.txt</pre>
                              
                              <p>
                                A region is specified with <tt>chr</tt>, <tt>chr:begin</tt> or <tt>chr:begin-end</tt>.</li> <li>
                                  Filter the raw variant calls. <pre>samtools.pl varFilter -D100 var-X.raw.txt &gt; var-X.flt.txt</pre>
                                  
                                  <p>
                                    Please remember to set the <tt>-D</tt> to set a maximum read depth according to the average read depth. In whole genome shotgun (WGS) resequencing, SNPs with excessively high read depth are usually caused by structural variations or alignment artifacts and should not be trusted.</li> <li>
                                      Acquire final variant calls by setting a quality threshold. <pre>awk '($3=="*"&&$6&gt;=50)||($3!="*"&&$6&gt;=20)' var-X.flt.txt &gt; var-X.final.txt</pre>
                                      
                                      <p>
                                        Here 50 is the quality threshold for indels and 20 for substitutions.</li> <li>
                                          Get the consensus sequence of chrX: <pre>samtools view -u aln.bam X | samtools pileup -cf hsRef.fa - | samtools.pl pileup2fq -D100 &gt; var-X.fq</pre>
                                          
                                          <p>
                                            File <tt>var-X.fq</tt> is in the multi-line FASTQ format. Bases in lowercase are filtered out due to repeats, being close to indels or insufficient/excessive read depth. The consensus file is essential to the estimate of mutation rate.
                                          </p>
                                          
                                          <p>
                                            The <tt>pileup2fq</tt> command applies fewer filters than <tt>varFilter</tt> and may not give identical results. For variant discovery, <tt>varFilter</tt> is recommended.</li> </ol> <p>
                                              <a id="Alternative_Protocol:_Variant_Calling_with_GATK" name="Alternative_Protocol:_Variant_Calling_with_GATK"></a>
                                            </p>
                                            
                                            <h1>
                                              Alternative Protocol: Variant Calling with GATK
                                            </h1>
                                            
                                            <p>
                                              <a id="Necessary_resources_3" name="Necessary_resources_3"></a>
                                            </p>
                                            
                                            <h2>
                                              Necessary resources
                                            </h2>
                                            
                                            <dl>
                                              <dt>
                                                Hardware
                                              </dt>
                                              
                                              <dd>
                                                A computer with 100GB free disk space.
                                              </dd>
                                              
                                              <dt>
                                                Software
                                              </dt>
                                              
                                              <dd>
                                                Linux; Java runtime; samtools
                                              </dd>
                                              
                                              <dt>
                                                Files
                                              </dt>
                                              
                                              <dd>
                                                Reference sequences in one FASTA file (<tt>hsRef.fa</tt> in this example). Position sorted alignment in the BAM format (<tt>aln.bam</tt>).
                                              </dd>
                                            </dl>
                                            
                                            <p>
                                              <a id="Procedure_3" name="Procedure_3"></a>
                                            </p>
                                            
                                            <h2>
                                              Procedure
                                            </h2>
                                            
                                            <ol>
                                              <li>
                                                Download and install GATK: <pre>wget ftp://ftp.broadinstitute.org/pub/gsa/GenomeAnalysisTK/GenomeAnalysisTK-EarlyAccess.tar.bz2;
tar -jxf GenomeAnalysisTK-EarlyAccess.tar.bz2;
ln -s GenomeAnalysisTK/GenomeAnalysisTK.jar</pre>
                                              </li>
                                              
                                              <li>
                                                Call SNPs:<br /> [Note that multiple -I (input bam) arguments can be specified (or one merged bam used) to make multi-sample-aware calls]</p> <pre>java -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T UnifiedGenotyper \
   -varout snpCalls.vcf -confidence 50.0 -U -S SILENT</pre>
                                              </li>
                                            </ol>
                                            
                                            <p>
                                              <a id="Support_Protocol_1:_Base_Quality_Recalibration" name="Support_Protocol_1:_Base_Quality_Recalibration"></a>
                                            </p>
                                            
                                            <h1>
                                              Support Protocol 1: Base Quality Recalibration
                                            </h1>
                                            
                                            <p>
                                              Base quality recalibration is optional, but it helps to improve the SNP quality and is preferred whenever possible. This tool recalibrates base quality scores of sequencing-by-synthesis reads in an aligned BAM file. Often base quality scores as reported by the sequencing machines can be inaccurate or uninformative. After recalibration, the quality scores in the QUAL field in each read in the output BAM are more accurate in that the reported quality score is much closer to its actual probability of mismatching the reference genome. Moreover, the recalibration tool attempts to correct for variation in quality with machine cycle and sequence context, and by doing so provides not only more accurate quality scores but also more widely dispersed (and thus more informative) ones.
                                            </p>
                                            
                                            <ol>
                                              <li>
                                                Download and install <a title="http://www.broadinstitute.org/gsa/wiki/index.php/The_Genome_Analysis_Toolkit" href="http://www.broadinstitute.org/gsa/wiki/index.php/The_Genome_Analysis_Toolkit" rel="nofollow">GATK</a>: <pre>wget ftp://ftp.broadinstitute.org/pub/gsa/GenomeAnalysisTK/GenomeAnalysisTK-EarlyAccess.tar.bz2;
tar -jxf GenomeAnalysisTK-EarlyAccess.tar.bz2;
ln -s GenomeAnalysisTK/GenomeAnalysisTK.jar</pre>
                                              </li>
                                              
                                              <li>
                                                Generate quality recalibration table: <pre>java -Xmx4g -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T CountCovariates -l INFO \
          -recalFile recal_data.csv -cov ReadGroupCovariate -cov QualityScoreCovariate \
          -cov CycleCovariate -cov DinucCovariate -cov TileCovariate</pre>
                                                
                                                <p>
                                                  Empirical quality is measured as ( # mismatches + 1 ) / ( # observations + 1 ) at all non-variant sites. Therefore it is strongly recommended to also apply &#8220;<tt>-D knownSNP.rod</tt>&#8221; with <tt>CountCovariates</tt>; otherwise base quality will be underestimated because known polymorphic sites will of course mismatch with the reference. CountCovariates also accepts VCF files as a list of known polymorphic sites to skip over. Users may take advantage of this feature by adding &#8220;<tt>-B variants,VCF,knownSNP.vcf</tt>&#8221; to the command.</li> <li>
                                                    After counting covariates in the initial BAM File, we then walk through the BAM file again and rewrite the quality scores (in the QUAL field) using the data in the recal_data.csv file, into a new BAM file: <pre>java -Xmx4g -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T TableRecalibration -l INFO \
          -recalFile recal_data.csv --output_bam alnRecal.bam</pre>
                                                  </li></ol> 
                                                  
                                                  <p>
                                                    There are many advanced options described in detail on the tool&#8217;s wiki page: <a title="http://www.broadinstitute.org/gsa/wiki/index.php/Base_quality_score_recalibration" href="http://www.broadinstitute.org/gsa/wiki/index.php/Base_quality_score_recalibration" rel="nofollow">http://www.broadinstitute.org/gsa/wiki/index.php/Base_quality_score_recalibration</a>
                                                  </p>
                                                  
                                                  <p>
                                                    <a id="Support_Protocol_2:_Local_Realignment" name="Support_Protocol_2:_Local_Realignment"></a>
                                                  </p>
                                                  
                                                  <h1>
                                                    Support Protocol 2: Local Realignment
                                                  </h1>
                                                  
                                                  <p>
                                                    Samtools calls short indels with local realignment, but it does not write a modified BAM file after the realignment. The GATK though provides such a tool that realigns reads in regions with suspected indel artifacts and generates a BAM with cleaned alignments.
                                                  </p>
                                                  
                                                  <ol>
                                                    <li>
                                                      Collect regions around potential indels and clusters of mismatches: <pre>samtools view -H aln.bam | grep ^@SQ &gt; hsRef.dict;
java -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T IndelIntervals -U -S SILENT -o indelIntv.txt;
java -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T MismatchIntervals -U -S SILENT -o mmIntv.txt</pre>
                                                    </li>
                                                    
                                                    <li>
                                                      Merge intervals: <pre>java -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T IntervalMerger -U -S SILENT \
          --intervalsToMerge indelIntv.txt --intervalsToMerge mmIntv.txt -o mergedIntv.txt</pre>
                                                    </li>
                                                    
                                                    <li>
                                                      Realign reads overlapping specified regions: <pre>java -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T IntervalCleaner -L mergedIntv.txt -U -S SILENT \
          --OutputCleanedReadsOnly --OutputCleaned cleaned.bam --OutputIndels rawIndel.txt</pre>
                                                    </li>
                                                    
                                                    <li>
                                                      Write the cleaned alignment file: <pre>java -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T CleanedReadInjector --cleaned_reads cleaned.bam \
          -U -S SILENT --output_bam alnReAln.bam</pre>
                                                    </li>
                                                  </ol>
                                                  
                                                  <p>
                                                    <a id="Support_Protocol_3:_Assessing_coverage" name="Support_Protocol_3:_Assessing_coverage"></a>
                                                  </p>
                                                  
                                                  <h1>
                                                    Support Protocol 3: Assessing coverage
                                                  </h1>
                                                  
                                                  <p>
                                                    The GATK provides a tool to assess the depth of coverage over any number of intervals in a BAM file. The coverage will be displayed in the output for every single position plus as an average over each interval specified.
                                                  </p>
                                                  
                                                  <pre>java -jar GenomeAnalysisTK.jar -I aln.bam -R hsRef.fa -T DepthOfCoverage -L intervals.txt -U -S SILENT</pre>
                                                  
                                                  <p>
                                                    <a id="Support_Protocol_4:_Viewing_Alignment_with_IGV" name="Support_Protocol_4:_Viewing_Alignment_with_IGV"></a>
                                                  </p>
                                                  
                                                  <h1>
                                                    Support Protocol 4: Viewing Alignment with <a title="http://www.broadinstitute.org/igv/" href="http://www.broadinstitute.org/igv/" rel="nofollow">IGV</a>
                                                  </h1>
                                                  
                                                  <p>
                                                    Samtools provides a concise text-based alignment viewer which does not support advanced features such as zooming and annotation tracks. For advanced features, the Integrative Genomics Viewer is more appropriate.
                                                  </p>
                                                  
                                                  <ol>
                                                    <li>
                                                      Launch IGV. IGV can be launched via Java Web Start. The human reference genome and annotation tracks are available from the IGV server. Nonetheless, if you prefer to use your own reference sequences and annotation, you may download IGV and run it locally on your computer. To download and install IGV: <pre>wget http://www.broadinstitute.org/igvdata/downloads/IGV_1.4.04.zip;
unzip IGV_1.4.04.zip;
wget http://www.broadinstitute.org/igvdata/downloads/igvtools.zip;
unzip igvtools.zip IGVTools/igvtools.jar</pre>
                                                      
                                                      <p>
                                                        and to lauch IGV locally:
                                                      </p>
                                                      
                                                      <pre>(cd IGV_1.4.04; sh igv_linux-64.sh)</pre>
                                                      
                                                      <p>
                                                        You should invoke another shell script if you are not using <tt>x86_64-linux</tt>.</li> <li>
                                                          Import the genome sequence. Open the &#8220;<tt>File->Import Genome...</tt>&#8221; menu. Name the reference as &#8220;<tt>hsRef</tt>&#8221; and choose the reference sequence file &#8220;<tt>hsRef.fa</tt>&#8220;. You may also import the gene annotation file if it is available.
                                                        </li>
                                                        <li>
                                                          Generate the coverage information to be displayed in IGV. In a terminal: <pre>java -jar IGVTools/igvtools.jar count aln.bam aln.depth hsRef.genome</pre>
                                                          
                                                          <p>
                                                            where <tt>hsRef.genome</tt> was generated when we imported the genome sequence at the last step.
                                                          </p>
                                                          
                                                          <p>
                                                            This step is optional, but it is essential if you want to see the read depth information in large scale.</li> <li>
                                                              Load the alignment. Come back to the IGV window. Open the &#8220;<tt>File->Load from File...</tt>&#8221; menu, and choose the alignment file &#8220;<tt>aln.bam</tt>&#8220;. Open the &#8220;<tt>File->Load from File...</tt>&#8221; menu again, and choose the depth file &#8220;<tt>aln.depth.tdf</tt>&#8220;.
                                                            </li>
                                                            <li>
                                                              View the alignment. You may not see the alignment immediately when the file is loaded. You need to zoom in to see the details. A typical alignment view looks like:<br /> <a title="Igv.png" href="http://sourceforge.net/apps/mediawiki/samtools/index.php?title=File:Igv.png"><img alt="" src="http://sourceforge.net/apps/mediawiki/samtools/nfs/project/s/sa/samtools/thumb/c/c0/Igv.png/640px-Igv.png" width="640" height="494" border="0" /></a>
                                                            </li></ol> 
                                                            <p>
                                                              <a id="Support_Protocol_5:_APIs_for_Accessing_Alignments_in_SAM.2FBAM" name="Support_Protocol_5:_APIs_for_Accessing_Alignments_in_SAM.2FBAM"></a>
                                                            </p>
                                                            
                                                            <h1>
                                                              Support Protocol 5: APIs for Accessing Alignments in SAM/BAM
                                                            </h1>
                                                            
                                                            <p>
                                                              <a id="C_APIs_.28SAMtools-C.29" name="C_APIs_.28SAMtools-C.29"></a>
                                                            </p>
                                                            
                                                            <h2>
                                                              C APIs (SAMtools-C)
                                                            </h2>
                                                            
                                                            <ol>
                                                              <li>
                                                                Download samtools and compile libbam.a: <pre>wget http://sourceforge.net/projects/samtools/files/samtools/0.1.7/samtools-0.1.7a.tar.bz2/download;
tar -jxf samtools-0.1.7a.tar.bz2;
export SAMTOOLS=`pwd`/samtools-0.1.7a;
(cd $SAMTOOLS; make libbam.a)</pre>
                                                              </li>
                                                              
                                                              <li>
                                                                Create file <tt>bam2bed.c</tt> which is: <pre>#include &lt;stdio.h&gt;
#include "sam.h"
/* callback for bam_fetch() */
static int fetch_func(const bam1_t *b, void *data)
{
    samfile_t *fp = (samfile_t*)data;
    uint32_t *cigar = bam1_cigar(b);
    const bam1_core_t *c = &b-&gt;core;
    int i, l;
    if (c-&gt;flag&BAM_FUNMAP) return 0; /* skip unmapped reads */
    for (i = l = 0; i &lt; c-&gt;n_cigar; ++i) {
        int op = cigar[i]&0xf;
        if (op == BAM_CMATCH || op == BAM_CDEL || op == BAM_CREF_SKIP)
            l += cigar[i]&gt;&gt;4;
    }
    printf("%s\t%d\t%d\t%s\t%d\t%c\n", fp-&gt;header-&gt;target_name[c-&gt;tid],
           c-&gt;pos, c-&gt;pos + l, bam1_qname(b), c-&gt;qual, (c-&gt;flag&BAM_FREVERSE)? '-' : '+');
    return 0;
}
int main(int argc, char *argv[])
{
    samfile_t *fp;
    if (argc == 1) {
        fprintf(stderr, "Usage: bam2bed &lt;in.bam&gt; [region]\n");
        return 1;
    }
    if ((fp = samopen(argv[1], "rb", 0)) == 0) {
        fprintf(stderr, "bam2bed: Fail to open BAM file %s\n", argv[1]);
        return 1;
    }
    if (argc == 2) { /* if a region is not specified */
        bam1_t *b = bam_init1();
        while (samread(fp, b) &gt;= 0) fetch_func(b, fp);
        bam_destroy1(b);
    } else {
        int ref, beg, end;
        bam_index_t *idx;
        if ((idx = bam_index_load(argv[1])) == 0) { /* load BAM index */
            fprintf(stderr, "bam2bed: BAM index file is not available.\n");
            return 1;
        }
        bam_parse_region(fp-&gt;header, argv[2], &ref, &beg, &end); /* parse region */
        if (ref &lt; 0) {
            fprintf(stderr, "bam2bed: Invalid region %s\n", argv[2]);
            return 1;
        }
        bam_fetch(fp-&gt;x.bam, idx, ref, beg, end, fp, fetch_func);
        bam_index_destroy(idx);
    }
    samclose(fp);
    return 0;
}</pre>
                                                              </li>
                                                              
                                                              <li>
                                                                Compile <tt>bam2bed.c</tt>: <pre>gcc -I$SAMTOOLS -g -O2 -Wall bam2bed.c -o bam2bed -lz -L$SAMTOOLS -lbam;</pre>
                                                              </li>
                                                              
                                                              <li>
                                                                Convert BAM to BED with: <pre>./bam2bed aln.bam &gt; aln.bed;
./bam2bed aln.bam X:10,000,000-20,000,000 &gt; aln-partial.bed</pre>
                                                              </li>
                                                            </ol>
                                                            
                                                            <p>
                                                              <a id="Java_APIs_.28Picard.29" name="Java_APIs_.28Picard.29"></a>
                                                            </p>
                                                            
                                                            <h2>
                                                              Java APIs (Picard)
                                                            </h2>
                                                            
                                                            <ol>
                                                              <li>
                                                                Download Picard from <a title="https://sourceforge.net/projects/picard/files/" href="https://sourceforge.net/projects/picard/files/" rel="nofollow">[1]</a>
                                                              </li>
                                                              <li>
                                                                Create file <tt>BamToBed.java</tt> which is: <pre>import net.sf.picard.cmdline.CommandLineProgram;
import net.sf.picard.cmdline.Option;
import net.sf.picard.cmdline.StandardOptionDefinitions;
import net.sf.picard.cmdline.Usage;
import net.sf.picard.io.IoUtil;
import net.sf.samtools.*;

import java.io.File;
import java.util.Iterator;

/**
 * Command-line application for converting bam or sam files to bed files.
 */
public class BamToBed extends CommandLineProgram {

    /* Specify usage string and command-line options. There is annotation-processing code elsewhere that will generate
        command-line parsing code based on these.
     */

    /** Usage string */
    @Usage
    public String USAGE = getStandardUsagePreamble() + "bam or sam file to bed file conversion.\n" +
            "Input and output formats are determined by file extension.";

    /** Command-line args */
    @Option(doc="The BAM or SAM file to convert.", shortName= StandardOptionDefinitions.INPUT_SHORT_NAME) public File INPUT;
    @Option(doc="The sequence name.", shortName="SEQ", optional=true) public String SEQUENCE;
    @Option(doc="The starting index (1-based inclusive).", shortName="S", optional=true) public Integer START;
    @Option(doc="The end index (1-based inclusive).", shortName="E", optional=true) public Integer END;

    /** Whether the user provided sequence, start, and end args on the command line */
    protected boolean rangeArgsProvided = false;

    /** This method contains the main logic of the application */
    protected int doWork() {
        IoUtil.assertFileIsReadable(INPUT);

        final SAMFileReader reader = new SAMFileReader(INPUT);

        Iterator&lt;SAMRecord&gt; iterator = null;
        if(!rangeArgsProvided )
        {
            iterator = reader.iterator();
        }
        else
        {
            iterator = reader.queryOverlapping(SEQUENCE, START, END);
        }

        while (iterator.hasNext()) {
            final SAMRecord record = iterator.next();
            if (record.getReadUnmappedFlag()) {
                continue;
            }

            // Output tab-delimited fields in bed file format
            System.out.println(record.getReferenceName() + "\t" +
                    (record.getAlignmentStart() - 1) + "\t" + //subtract 1 to shift from one-based to zero-based
                    (record.getAlignmentEnd() - 1 + 1) + "\t" + //subtract 1 to shift from one-based to zero-based, and
                                                                // then add 1 to shift from inclusive to exclusive
                    record.getReadName() + "\t" +
                    record.getMappingQuality() + "\t" +
                    (record.getReadNegativeStrandFlag()? "-": "+") );
        }
        reader.close();

        return 0;
    }

    /**
     * Put any custom command-line validation in an override of this method.
     * clp is initialized at this point and can be used to print usage and access argv.
     * Any options set by command-line parser can be validated.
     * @return null if command line is valid.  If command line is invalid, returns an array of error message
     * to be written to the appropriate place.
     */
    protected String[] customCommandLineValidation() {
    	if(SEQUENCE == null && START == null && END == null)
        {
            return null;
        }

        //validate SEQUENCE, START, END args
        if(SEQUENCE == null)
        {
            return new String[] { "Missing the SEQUENCE arg." };
        }

        if(START == null)
        {
            return new String[] { "Missing the START arg." };
        }

        if(END == null) 
        {
            return new String[] { "Missing the END arg." };
        }

        if(START &gt;= END)
        {
            return new String[] { "START arg is &gt;= END arg."};
        }

        rangeArgsProvided = true;
        return null;
    }

    /**
     * Main entry point of the application.
     *
     * @param argv Command line args.
     */
    public static void main(String[] argv) {
        new BamToBed().instanceMainWithExit(argv);
    }

}</pre>
                                                              </li>
                                                              
                                                              <li>
                                                                Compile <tt>BamToBed.java</tt>, putting the <tt>picard-(version).jar</tt> and <tt>sam-(version).jar</tt> on the classpath: <pre>javac -cp picard-(version).jar:sam-(version).jar BamToBed.java</pre>
                                                              </li>
                                                              
                                                              <li>
                                                                Convert BAM to BED by running <tt>BamToBed.class</tt>: <pre>java -cp .:picard-(version).jar:sam-(version).jar BamToBed INPUT=test.bam &gt; test.bed;
java -cp picard-(version).jar:sam-(version).jar BamToBed INPUT=test.bam SEQUENCE=chr1 START=1329545 END=1321000 &gt; test-partial.bed</pre>
                                                              </li>
                                                            </ol>
                                                            
                                                            <p>
                                                              <a id="Perl_APIs_.28Bio-SamTools.29" name="Perl_APIs_.28Bio-SamTools.29"></a>
                                                            </p>
                                                            
                                                            <h2>
                                                              Perl APIs (Bio-SamTools)
                                                            </h2>
                                                            
                                                            <p>
                                                              <a id="Python_APIs_.28Pysam.29" name="Python_APIs_.28Pysam.29"></a>
                                                            </p>
                                                            
                                                            <h2>
                                                              Python APIs (Pysam)
                                                            </h2>
                                                            
                                                            <ol>
                                                              <li>
                                                                Install <a title="http://www.cosc.canterbury.ac.nz/greg.ewing/python/Pyrex/" href="http://www.cosc.canterbury.ac.nz/greg.ewing/python/Pyrex/" rel="nofollow">Pyrex</a> if absent: <pre>export PYTHONPATH="$PYTHONPATH:$HOME/opt/lib/python2.6/site-packages";
wget http://www.cosc.canterbury.ac.nz/greg.ewing/python/Pyrex/Pyrex-0.9.8.5.tar.gz
tar -zxf Pyrex-0.9.8.5.tar.gz;
(cd Pyrex-0.9.8.5; python setup.py install --prefix=$HOME/opt)</pre>
                                                                
                                                                <p>
                                                                  You do not need to set <tt>PYTHONPATH</tt> and <tt>--prefix</tt> if you have the write permission to the system default module search path. Install <a title="http://code.google.com/p/pysam/" href="http://code.google.com/p/pysam/" rel="nofollow">pysam</a>:
                                                                </p>
                                                                
                                                                <pre>wget http://pysam.googlecode.com/files/pysam-0.1.1.tar.gz
tar -zxf pysam-0.1.1.tar.gz;
(cd pysam-0.1.1; python setup.py install --prefix=$HOME/opt)</pre>
                                                              </li>
                                                              
                                                              <li>
                                                                Create script <tt>bam2bed.py</tt>, which is: <pre>#!/bin/env python

import os, sys, re, optparse
import pysam

def main( argv = None ):
    if not argv: argv = sys.argv

    # setup command line parser
    parser = optparse.OptionParser( version = "%prog version: $Id$", 
                                    usage = globals()["__doc__"] )
    parser.add_option("-r", "--region", dest="region", type="string",
                      help="samtools region string [default=%default]."  )
    parser.set_defaults( region = None, )
    (options, args) = parser.parse_args( argv[1:] )
    if len(args) != 1:
        raise ValueError( "no samfile specified - see --help for usage" )

    # open BAM and get the iterator
    samfile = pysam.Samfile( args[0], "rb" )
    if options.region != None:
        it = samfile.fetch( region=options.region )
    else:
        it = samfile.fetch()

    # calculate the end position and print out BED
    take = (0, 2, 3) # CIGAR operation (M/match, D/del, N/ref_skip)
    outfile = sys.stdout
    for read in it:
        if read.is_unmapped: continue
        # compute total length on reference
        t = sum([ l for op,l in read.cigar if op in take ])
        if read.is_reverse: strand = "-"
        else: strand = "+"
        outfile.write("%s\t%d\t%d\t%s\t%d\t%c\n" %\
                          ( samfile.getrname( read.rname ),
                            read.pos, read.pos+t, read.qname,
                            read.mapq, strand) )            

if __name__ == "__main__":
    sys.exit( main( sys.argv) )</pre>
                                                              </li>
                                                              
                                                              <li>
                                                                Convert BAM to BED with: <pre>python bam2bed.py aln.bam &gt; aln.bed;
python bam2bed.py -r X:10,000,000-20,000,000 aln.bam &gt; aln-partial.bed</pre>
                                                              </li>
                                                            </ol>
                                                            
                                                            <p>
                                                              <a id="Commentary" name="Commentary"></a>
                                                            </p>
                                                            
                                                            <h1>
                                                              Commentary
                                                            </h1>
                                                            
                                                            <p>
                                                              <a id="Literature_Cited" name="Literature_Cited"></a>
                                                            </p>
                                                            
                                                            <h1>
                                                              Literature Cited
                                                            </h1>
                                                            
                                                            <ul>
                                                              <li>
                                                                Li H. and Durbin R. (2009) Fast and accurate short read alignment with Burrows-Wheeler Transform. Bioinformatics, 25:1754-60. [PMID: <a title="http://www.ncbi.nlm.nih.gov/pubmed/19451168" href="http://www.ncbi.nlm.nih.gov/pubmed/19451168" rel="nofollow">19451168</a>]
                                                              </li>
                                                              <li>
                                                                Li H. and Durbin R. (2009) Fast and accurate long read alignment with Burrows-Wheeler Transform. Bioinformatics, accepted.
                                                              </li>
                                                              <li>
                                                                Li H.*, Handsaker B.*, Wysoker A., Fennell T., Ruan J., Homer N., Marth G., Abecasis G., Durbin R. and 1000 Genome Project Data Processing Subgroup (2009) The Sequence alignment/map format and SAMtools. Bioinformatics, 25:2078-9. [PMID: <a title="http://www.ncbi.nlm.nih.gov/pubmed/19505943" href="http://www.ncbi.nlm.nih.gov/pubmed/19505943" rel="nofollow">19505943</a>]
                                                              </li>
                                                            </ul>
                                                            
                                                            <p>
                                                              http://sourceforge.net/apps/mediawiki/samtools/index.php?title=SAM_protocol
                                                            </p>