---
title: Record of kegg usage 
layout: post
categories:
  - kegg
  - letter
tags:
  - kegg
---

#### KAAS annotate genes

* Map gene sequences or protein sequences to kegg orthologs using [kaas](http://www.genome.jp/tools/kaas/)

#### KEGG ID trnasfer

* [ToGoWs](http://togows.dbcls.jp/site/en/rest.html): various types of KEGG IDs to NCBI and UniProt IDs.
```
$ curl -s http://togows.dbcls.jp/entry/orthology/K08452,K13751/name
GPR97
SLC24A3, NCKX3
$ for i in `cat ko.list`; do echo $i, \
  `curl -s http://togows.dbcls.jp/entry/orthology/$i/name`; done \
  >ko.list2name
```

* Bioconductor packages
```
library(org.Hs.eg.db)

##Toy example symbols:
sym = c("AKT3","CDH1")

##Get the Entrez gene IDs associated with those symbols
EG_IDs = mget(sym, revmap(org.Hs.egSYMBOL),ifnotfound=NA)

##Then get the KEGG IDs associated with those entrez genes.
KEGG_IDs = mget(as.character(EG_IDs), org.Hs.egPATH,ifnotfound=NA)
```
 
