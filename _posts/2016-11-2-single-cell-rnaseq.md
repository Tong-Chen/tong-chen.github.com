---
title: OrthoMCL installation 
author: ct
layout: post
description:
modified:
image:
  background: triangular.png
  feature: feature.png
categories: [Bioinformatics]
tags: [OrthoMCL]
---


For a start:

The main difference is that you usually have to divide your reads by some sort of barcode to get which reads belong to which cell.  

The barcode will need to be trimmed off before aligning,  but from there the basic alignment and quantification steps are the similar with each cell treated like its own sample.

Also,  each cell is usually sequenced more shallowly than a library because there are fewer molecules in the input,  so you start getting duplicate reads earlier earlier.  You may want to remove duplicates,  like with Picard.

There might be a lot of runs of Ts if they were sequencing into the poly a tail a lot.  It would depend on the protocol.  I do not think it is a problem inherent to the fact that it is single cell.  That happens sometimes with regular libraries.

The downstream analyses are different.  I would look up Rahul Satija's papers.  He has got some analyses he has done and he has a package for single cell stuff.  I do not know how available it is yet.
'


### Reference
* http://pklab.med.harvard.edu/scw2014/
* http://hms-dbmi.github.io/scw/
* Possion model and negative bionomial model <http://hms-dbmi.github.io/scw/page2/>
* Review <http://www.cell.com/cell/abstract/S0092-8674(15)01353-7?elsca1=etoc&elsca2=email&elsca3=0092-8674_20151105_163_4_&elsca4=Cell%20Press)>
* F1000 pipeline <https://f1000research.com/articles/5-2122/v1>
* Full tutorial <http://hemberg-lab.github.io/scRNA.seq.course/introduction-to-single-cell-rna-seq.html>
* https://github.com/seandavi/awesome-single-cell
* http://rstudio-pubs-static.s3.amazonaws.com/115225_2d91e5f14c0144f2af55128bfb2e216b.html#/2
* http://rpubs.com/padpuydt/124509
* https://rstudio-pubs-static.s3.amazonaws.com/115225_2d91e5f14c0144f2af55128bfb2e216b.html#/59
* Seurat <http://satijalab.org/seurat/old-get-started/>
* <http://hms-dbmi.github.io/scde/diffexp.html>
* <https://www.bioconductor.org/help/workflows/simpleSingleCell/>

