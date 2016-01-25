---
title: Tips for KEGG usage
author: 悟道
layout: post
categories:
  - KEGG
  - letter
tags:
  - KEGG
---

### Get full list of KEGG pathways and orthologs

<http://www.genome.jp/kegg-bin/download_htext?htext=br08901.keg&format=htext&filedir=>
<http://www.genome.jp/kegg-bin/download_htext?htext=ko00001.keg&format=htext&filedir=>

### Get the orthologs of one pathway

```
http://togows.org/entry/kegg-pathway/ko00010/orthologs.json
```

will return

```
[
  {
  "K00844": "hexokinase [EC:2.7.1.1]", 
  "K12407": "glucokinase [EC:2.7.1.2]", 
  "K00845": "glucokinase [EC:2.7.1.2]", 
  "K01810": "glucose-6-phosphate isomerase [EC:5.3.1.9]",
  "K00001": "alcohol dehydrogenase [EC:1.1.1.1]",
  .
  .
  .
  }
]
```

### Get the genes of one ortholog

```
http://togows.org/entry/kegg-orthology/K00001/genes.json
```

will return 

```
[
  {
    "dme": [
		"Dmel_CG3481"
	], 
    "dpo": [
		"Dpse_GA17214"
	], 
    "dan": [
		"Dana_GF14888"
	], 
	"der": [
		"Dere_GG25120"
	]
	.
	.
	.
  }
]
```


### Get the amino sequence of one gene

```
http://togows.org/entry/kegg-genes/dme:Dmel_CG3481,dpo:Dpse_GA17214/aafasta.json
```

will return 

```
[
  ">Dmel_CG3481 (RefSeq) Alcohol dehydrogenase (EC:1.1.1.1
1.2.1.10)\nMSFTLTNKNVIFVAGLGGIGLDTSKELLKRDLKNLVILDRIENPAAIAELKAINPKVTVTFYPYDVTVPIAETTKLLKTIFAQLKTVDVLINGAGILDDHQIERTIAVNYTGLVNTTTAILDFWDKRKGGPGGIICNIGSVTGFNAIYQVPVYSGTKAAVVNFTSSLAKLAPITGVTAYTVNPGITRTTLVHTFNSWLDVEPQVAEKLLAHPTQPSLACAENFVKAIELNQNGAIWKLDLGTLEAIQWTKHWDSGI"
  , 
  ">Dpse_GA17214 (RefSeq) GA17214 gene product from transcript GA17214-RA
(EC:1.1.1.1)\nMSLTNKNVVFVAGLGGIGLDTSRELVKRNLKNLVILDRIDNPAAIAELKAINPKVTITFYPYDVTVPVAETTKLLKTIFAQVKTIDVLINGAGILDDHQIERTIAVNYTGLVNTTTAILDFWDKRKGGPGGIICNIGSVTGFNAIYQVPVYSGSKAAVVNFTSSLAKLAPITGVTAYTVNPGITKTTLVHKFNSWLDVEPRVAEKLLEHPTQTSQQCAENFVKAIELNKNGAIWKLDLGTLEPITWTQHWDSGI" 
]
```


### Get the compounds of one pathway

```
http://togows.org/entry/kegg-pathway/ko00010/compounds.json
```

will return

```
[
  {
      "C00022": "Pyruvate", 
	  "C00024": "Acetyl-CoA", 
	  "C00031": "D-Glucose", 
	  "C00033": "Acetate", 
	  "C00036": "Oxaloacetate",
  }
]
```

### Get the names of one compound

```
http://togows.org/entry/kegg-compound/C00003/names.json
```

will return

```
[
  [
      " NAD+" , 
	  " NAD" , 
	  " Nicotinamide adenine dinucleotide" , 
	  " DPN" , 
	  " Diphosphopyridine nucleotide" , 
	  " Nadide" , 
	  " beta-NAD+" 
  ]
]
```
