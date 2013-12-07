---
title: IGV and IGVtools usage
author: 悟道
layout: post
categories:
  - seq
  - NGS
  - letter
tags:
  - igv
---

1.Create your own .genome file

.genome file is a zipped file containing three files

**Step-by-step:**

1.  Click *Genomes>Create .genome File*. IGV displays the a window where you enter the information.
2.  Enter an ID and a descriptive name for the genome.
3.  Enter the path on your file system or a web URL to the FASTA file for the genome.  If the FASTA file has not already been indexed, an index will be created during the import process. This will generate a file with a &#8220;.fai&#8221; extension which must be in the same directory as the FASTA file; thus it is necessary that the directory containing the file be writable. [<span style="color: #ff0000;">FATSA should be the genome you used for mapping</span>]
4.  Optionally, specify the cytoband file and the annotation (gene) file. [<span style="color: #ff0000;">cytoband can be downloaded from UCSC like http://hgdownload.cse.ucsc.edu/goldenPath/mm9/database/, change mm9 to your version of genome. Annotation file can be GTF which is also the file you used for RNA-Seq mapping or got from UCSC Table Browser</span>]
5.  If the sequence (chromosome) names differ between your FASTA and annotation files, you might need to create [an alias file][1] to provide a mapping between the different names. Certain well-known aliases are built into IGV and do not require an alias file. These include mappings that involve adding or removing the prefix &#8220;chr&#8221; to the name, for example  1 > chr1 and chr1 > 1.  Also, NCBI identifiers of the form  **gi|125745044|ref|NC_002229.3| **in a FASTA file will be mapped to names of the form** NC_002229.3** in the corresponding GFF file.  [<span style="color: #ff0000;">Unneeded for me</span>]
6.  Click *Save*. IGV displays the Genome Archive window.
7.  Select the directory in which to save the genome archive (*.genome) file and click *Save*. IGV saves the genome and loads it into IGV.

2.Transfer BAM file to tdf or wig (Index BAM first)

<pre class="brush: bash; title: ; notranslate" title="">igvtools count --strands first --includeDuplicates rnaseq.bam rnaseq.tdf,rnaseq.wig mm9
igvtools count --strands first --includeDuplicates --pairs -w 1 rnaseq.bam rnaseq.tdf,rnaseq.wig mm9
</pre>

3. 截图时包含红色标记区域  
自动截图前，先把要截图的区域导入，然后再运行batch script

 [1]: http://www.broadinstitute.org/software/igv/LoadData/#aliasfile
