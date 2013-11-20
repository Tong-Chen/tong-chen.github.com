---
title: ENCODE standard for NGS
author: 悟道
layout: post
permalink: /?p=2484
categories:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.Chip-Seq

1. Read depth and sequencing quality  
a. At least **10** million **uniquely** mapped reads/replicate are required for mammalian samples, and  
at least 2 million for worms or flies. For broad chromatin marks (e.g. H3K27me3) **20 million**  
uniquely mapped reads/replicate are recommended.  
b. The number of reads for biological replicates should be within a factor of **2**.  
2. Controls  
a. Either input DNA (sonicated, reverse crosslinked DNA that has not been immunoprecipitated) or  
IgG (DNA obtained by immunoprecipitation with a non-specific antibody fraction) may be used  
as a scoring control;  
b. Control DNA must be amplified identically to experimental material;  
c. A separate control is required for each cell type, cell treatment, or developmental stage being  
studied  
d. Controls must be sequenced to same read depth as experimental samples.  
3. Number of replicates  
a. Two biological replicates are required for each dataset;  
b. For each replicate, targets are identified (see below) and 80% of the top 40% of peaks that  
exceed a given threshold (usually a false discovery rate of .01) must be present in the list of  
identified peaks for the other replicate;  
c. The number of targets identified for each replicate cannot differ by more than a factor of 2;  
d. Reads from replicates which meet these criteria are usually combined and the data rescored.  
4. Scoring  
Any scoring algorithm that accounts for control signals is acceptable for peak-calling. PeakSeq and  
MACS are commonly used by ENCODE.

http://www.google.com.hk/url?sa=t&#038;source=web&#038;cd=4&#038;cad=rja&#038;ved=0CEcQFjAD&#038;url=http%3A%2F%2Fwww.betacell.org%2Fdocuments%2Fadministered%2Fabout%2Fguidelines%2FENCODE\_BCBC\_ChIP-Seq\_Standards\_V01_20110503.pdf&#038;ei=JepPUPL-KIORigfepID4Cw&#038;usg=AFQjCNG1KHmlxsMuq-v6w0NociOYMlWlnw

&nbsp;

2.RNA-Seq

<p align="left">
  “Experiments whose purpose is to evaluate the similarity between the transcriptional profiles of two polyA+ samples may require only modest depths of sequencing (e.g. 30M pair-end reads of length > 30NT, of which 20-25M are mappable to the genome or known transcriptome.”
</p>

<p align="left">
  and for
</p>

<p align="left">
  “Experiments whose purpose is discovery of novel transcribed elements and strong quantification of known transcript isoforms… a minimum depth of 100-200 M 2 x 76 bp or longer reads is currently recommended.”
</p>

<p align="left">
  http://www.rna-seqblog.com/information/how-many-reads-are-enough/
</p>

<p align="left">
  http://encodeproject.org/ENCODE/protocols/dataStandards/ENCODE_RNAseq_Standards_V1.0.pdf
</p>

&nbsp;