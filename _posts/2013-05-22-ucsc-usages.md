---
title: UCSC usages
author: 悟道
layout: post
categories:
  - seq
  - NGS
  - letter
---

1.Get the type of each transcripts

<pre class="brush: bash; title: ; notranslate" title="">--#Refseq genes
--From table refSeqStatus
--Status
    'Unknown', 'Reviewed', 'Validated', 'Provisional', 'Predicted', 'Inferred'
--Molecular type
    'DNA', 'RNA', 'ds-RNA', 'ds-mRNA', 'ds-rRNA', 'mRNA', 'ms-DNA', 'ms-RNA', 'rRNA', 'scRNA',
    'snRNA', 'snoRNA', 'ss-DNA', 'ss-RNA', 'ss-snoRNA', 'tRNA', 'cRNA', 'ss-cRNA', 'ds-cRNA', 'ms-rRNA'
-------------------------------------------------------------------------------------------------------
--#Ensemble gene
--From table ensemblSource
--name	source
   ENSMUST00000160944	transcribed_unprocessed_pseudogene
   ENSMUST00000082908	snRNA
   ENSMUST00000162897	processed_transcript
   ENSMUST00000159265	processed_transcript
   ENSMUST00000070533	protein_coding
   ENSMUST00000161581	antisense
   ENSMUST00000157765	snRNA
[http://asia.ensembl.org/info/docs/genebuild/ncrna.html

http://redmine.soe.ucsc.edu/forum/index.php?t=msg&#038;goto=12047&#038;S=03eba72760c0c4d83c9a2327810936cb]

</pre>

2.Get pseudogene GTF

<pre class="brush: bash; title: ; notranslate" title="">UCSC table browser
group: alltables
table:pseudoYale60

http://genome.ucsc.edu/cgi-bin/hgTables?hgsid=336807659&#038;clade=mammal&#038;org=Mouse&#038;db=mm9&#038;hgta_group=allTables&#038;hgta_track=mm9&#038;hgta_table=pseudoYale60&#038;hgta_regionType=genome&#038;position=chr16%3A17222428-17222755&#038;hgta_outputType=selectedFields&#038;hgta_outFileName=mm9.rmsk.gtf

</pre>

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

4.Get and use Phastcon  
1) Get PhastCons scores from UCSC:

There are various phastCons score files, depending on the genomes in the pileup. E.g.

http://hgdownload.cse.ucsc.edu/goldenPath/mm9/phastCons30way/

You can get them by ftp:

<pre class="brush: bash; title: ; notranslate" title="">wget ftp://hgdownload.cse.ucsc.edu/goldenPath/mm9/phastCons30way/vertebrate/chr*
</pre>

2) Convert wig to bigWig:

Each chromosome file of scores (wig files) can be converted into bigWig files. 64-bit binaries come from:

http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/

The fetchChromSizes script is required to get the chromosome length for the &#8216;wigToBigWig&#8217; script:

<pre class="brush: bash; title: ; notranslate" title="">fetchChromSizes mm9 &gt; mm9.chrom.sizes
</pre>

Run wigToBigWig on each chromosome file, e.g:

<pre class="brush: bash; title: ; notranslate" title="">wigToBigWig -clip chr1.data mm9.chrom.sizes chr1.bw
</pre>

3) Calculate mean phastCons score for the coordinates of interest:

Another script called bigWigSummary can be obtained from UCSC, using the link above. It takes in a set of genome coordinate and will spit out the max or mean of values contained in the bigWig file, in our case phastCons scores.

4) Get repeat elements and their class and family information

<pre class="brush: bash; title: ; notranslate" title="">1.UCSC table browser --- mammal -- mouse --- mm9 -variation and repeats -- repeatmarsker --- rmsk -- selected fields from primary and related tables
</pre>

[<img class="aligncenter size-full wp-image-3200" alt="rmsk" src="http://210.75.224.29/wordpress/wp-content/uploads/2013/05/rmsk.png" width="719" height="341" />][1]

 [1]: http://210.75.224.29/wordpress/wp-content/uploads/2013/05/rmsk.png
