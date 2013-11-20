---
title: Alternative splicing
author: 悟道
layout: post
permalink: /?p=2965
categories:
  - bioinformatics
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

Alternative Splicing Event Set

Introduction

Alternative splicing is a widespread mechanism for generating protein diversity and regulating protein expression. The term alternative splicing is used in biology to describe any case in which a primary transcript can be spliced in more than one pattern to generate multiple, distinct mRNAs.

The set of alternative splicing events (AS events) is derived from Ensembl gene annotation. The Ensembl gene set includes both automatic and manual annotation, with all transcripts based on experimental evidence.

Alternatively spliced transcripts from any given Ensembl gene are compared to provide a comprehensive list of elementary alternative splicing events. These data can be found on the website in the gene and/or transcript tab, and can be accessed by BioMart, or programmatically from the core database using the Perl API.

AS events are available for the following model organisms:

Caenorhabditis elegans  
Danio rerio  
Drosophila melanogaster  
Homo sapiens  
Mus musculus  
Rattus norvegicus  
Alternative Spliced Patterns

Seven common patterns of alternatively spliced exonic regions are automatically annotated in Ensembl for the species mentioned.

AS Pattern Type Acronym Definition  
Cassette exon (skipped exon) CE One exon is spliced out of the primary transcript together with its flanking introns.  
Intron retention IR A sequence is spliced out as an intron or remains in the mature mRNA transcript.  
Mutually exclusive exons MXE Refer to a case in which multiple cassette exons are used in a mutually exclusive manner. In the simplest case: two consecutive exons that are never both included in the mature mRNA transcript.  
Alternative 3&#8242; sites A3SS Also called alternatively acceptor sites. Two or more splice sites are recognized at the 5&#8242; end of an exon. An alternative 3&#8242; splice junction (acceptor site) is used, changing the 5&#8242; boundary of the downstream exon.  
Alternative 5&#8242; sites A5SS Also called alternative donor sites. Two or more splice sites are recognized at the 3&#8242; end of an exon. An alternative 5&#8242; splice junction (donor site) is used, changing the 3&#8242; boundary of the upstream exon.  
Alternative first exon AFE Second exons of each variant have identical boundaries, but first exons are mutually exclusive. This is to annotate possible alternative promoter usage*.  
Alternative last exon ALE Penultimate exons of each splice variant have identical boundaries, but last exons are mutually exclusive. This is to allow annotation of possible alternative polyadenylation usage*.  
* AFE and ALE event types are difficult to interpret and additional biological evidence is needed to support alternative promoter or polyadenylation usage, respectively.

Ensembl adds two types of AS events defined by the ASTD project [1].

AS Pattern Type Acronym Definition  
Intron isoform II Alternative donor or acceptor splice sites lead to truncation or extension of introns, respectively. This is for introns with truncation and/or extension on both splice sites.  
Exon isoform EI Alternative donor or acceptor splice sites leads to truncation or extension of exons, respectively. This is for exons with truncation and/or extension on both splice sites. First and last exons are not considered in this computation. Flanking exons accross splice variants must overlap.  
Different acronyms for the same type of AS event can be found in the scientific literature and in several online related resources. Ensembl uses CE, IR, MXE, A3SS, A5SS, AFE, ALE, II, EI as standard acronyms. Similar acronyms can be found in [1] and [2].

References

1. Koscielny G, Le Texier V, Gopalakrishnan C, Kumanduri V, Riethoven JJ, Nardone F, Stanley E, Fallsehr C, Hofmann O, Kull M, Harrington E, Boué S, Eyras E, Plass M, Lopez F, Ritchie W, Moucadel V, Ara T, Pospisil H, Herrmann A, G Reich J, Guigó R, Bork P, Doeberitz MK, Vilo J, Hide W, Apweiler R, Thanaraj TA, Gautheret D.  
ASTD: The Alternative Splicing and Transcript Diversity database.  
Genomics. 2009 Mar;93(3):213-20.  
10.1016/j.ygeno.2008.11.003

2. Wang ET, Sandberg R, Luo S, Khrebtukova I, Zhang L, Mayr C, Kingsmore SF, Schroth GP, Burge CB.  
Alternative Isoform Regulation in Human Tissue Transcriptomes.  
Nature 456, 470-476.  
doi:10.1038/nature07509

http://www.ensembl.org/info/docs/genebuild/ase_annotation.html