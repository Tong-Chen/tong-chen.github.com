---
title: GSEA usages
layout: post
categories:
    - gsea
    - letter
tags:
    - gsea
---

#### Overview of GSEA
Gene set enrichment analysis ([gsea](http://www.broadinstitute.org/gsea/index.jsp)) is a computational method that determines whether an a priori defined set of genes shows statistically 
significant, concordant differences between two biological states 
(e.g. phenotypes). 

![gsea main pic]({{ site.img_url }}/GSEA.gif)

#### Input files preparation

##### Fast preparation

Normally we would have gene expression matrix like the file listed below:

```
#test.a
gene	kdctcf_1	kdctcf_2	kdctcf_3	ctl_1	ctl_2	ctl_3
a	1	2	3	4	5	6
b	1	2	3	4	5	6
c	1	2	3	4	5	6
d	1	2	3	4	5	6
```
```
#test.b
gene	kdctcf	kdctcf	kdctcf	ctl	ctl	ctl
a	1	2	3	4	5	6
b	1	2	3	4	5	6
c	1	2	3	4	5	6
d	1	2	3	4	5	6
```

The program [transfernormalexprmatrixforgsea.py](https://github.com/tong-chen/ngs/blob/master/transfernormalexprmatrixforgsea.py) will help to transfer expression matrix to generate `gct` and `cls` file for gsea usages. 

Run this script using sample data as showed below (Please refer to the program for deatiled description of input and output files.):

```bash
#transfer test.a
transfernormalexprmatrixforgsea.py -i test.a
#transfer test.b
transfernormalexprmatrixforgsea.py -i test.b -u 0
#<-u 0> indicates there are duplicates in sample names
```

Both commands creat same output (test.a.gct, test.a.cls, test.b.gct, test.b.cls), here only lists the first two of them:

`test.a.gct`

```
#1.2
4	6
gene	description	kdctcf_1	kdctcf_2	kdctcf_3	ctl_1	ctl_2	ctl_3
a	a	1	2	3	4	5	6
b	b	1	2	3	4	5	6
c	c	1	2	3	4	5	6
d	d	1	2	3	4	5	6
```
`test.a.cls`

```
6 2 1
# kdctcf ctl
kdctcf kdctcf kdctcf ctl ctl ctl
```

For huamn and mouse dataset, `gmt` files can be downloaded from [gsea](http://www.broadinstitute.org/gsea/downloads.jsp) and [enrichmentmap](http://download.baderlab.org/EM_Genesets/current_release/).

Now, we have got all required files for GSEA analysis.

##### Detailed description for each file

* gct fileformat

![gct format]({{ site.img_url }}/gct.gif)

    * The first line should always be `#1.2`.
	* The second line contains tow columns, `(# of genes)<tab>(# of samples)`.
	* The first two columns of data lines are `gene name` (should be unique) and `gene description` (which will not be used in gsea, usually it can be the same as gene name).

* cls format
    
![cls format]({{ site.img_url }}/cls.png)

	* The first line contains `(# of damples)<space>(# of classes)<space>1`.
	* The second line contains `#<space>(class 0 name)<space>(class 1 name)...`.
	* The third line contains `(class1-samp1)<space>(class1-samp2)<space>(class2-samp1)...`.

* gmt format

The `GMT` file format is a tab delimited file format that describes gene sets. In the GMT format, each row represents a `gene set`; in the GMX format, each column represents a gene set. The GMT file format is organized as follows:

![gmt format]({{ site.img_url }}/gmt.gif)

Each gene set is described by a `name`, a `description`, and `the genes in the gene set`. GSEA uses the description field to determine what hyperlink to provide in the report for the gene set description: if the description is "na", GSEA provides a link to the named gene set in MSigDB; if the description is a URL, GSEA provides a link to that URL.

Since I can directly download `gmt` files from [gsea](http://www.broadinstitute.org/gsea/downloads.jsp) and [enrichmentmap](http://download.baderlab.org/EM_Genesets/current_release/), I have not tried to generate `gmt` files.

#### Run gsea

Below steps are borrowed from [http://www.baderlab.org/Software/EnrichmentMap/Tutorial](http://www.baderlab.org/Software/EnrichmentMap/Tutorial). There is also `sample data` in their web sites for testing this tutorial.

* GO to GSEA website - [http://www.broadinstitute.org/gsea/](http://www.broadinstitute.org/gsea/).
* Click on [Downloads](http://www.broadinstitute.org/gsea/downloads.jsp) in the page header.
    * From the *javaGSEA Desktop Application* right click on Launch with 1 Gb memory.
    * Click on "Save Target as…" and save shortcut to your desktop or your folder of choice so you can launch GSEA for your analysis without having to navigate to it through your web browser.
* Double click on GSEA icon you created.
    * Specially, runing `javaws gsea.jnlp` to start GSEA in linux. 
* Click on **Load data** in left panel.
* Click on *Browse for files* in newly opened *Load data panel*.
* Navigate to directory where you stored tutorial test set files. Select all raw expression (`.gct`) file, sample class file(`.cls`) and gene set (`.gmt`) file. Click on *Open*.
* **Wait** until confirmation box appears indicating that all files loaded successfully. Click on Ok.
* Click on **Run GSEA** in left panel.
* Select the Expression dataset:
    * Click on the arrow next to the Expression dataset text box.
    * Select the expression set you wish to run the analysis on (MCF7_ExprMx_v2_names.gct).
* Select the Gene Set Database:
    * Click on `… ` next to the text box of Gene Set Database.
    * Click on Gene Matrix (`local gmx/gmt`) tab.
    * Select gmt file `Human_GO_AllPathways_no_GO_iea_April_15_2013_symbo.gmt` and click on Ok.
* Select the Phenotype labels file
    * Click on `… ` next to the text box of Phenotype labels.
    * Make sure Select source file is set to `ES_NT.cls`.
    * Select `ES12_versus_NT12` and click on Ok.
* Click on the down arrow next to the text box for `Collapse dataset to gene symbols`, select `false`.
* Click on the down arrow next to the text box for `Permutation type`, select `gene_set`.
* Click on `Show` next to Basic fields.
* Click in text box next to `Analysis name and rename` (example:estrogen_treatment_12hr_gsea_enrichment_results).
* Click on `… ` next to "Save results" in this folder text box. Navigate to the folder where you wish to save the results (preferably the same directory where all the input files have been saved).
* Click on Run in the bottom right corner.
* Wait untial the `status` in left panel is `success`. The output will be saved in input folder.

![GSEA run]({{ site.img_url }}/GSEA_tutorial.png)

#### Reference

* [http://www.broadinstitute.org/cancer/software/gsea/wiki/index.php/Data_formats](http://www.broadinstitute.org/cancer/software/gsea/wiki/index.php/Data_formats#Expression_Data_Formats)
* [http://www.broadinstitute.org/gsea/downloads.jsp](http://www.broadinstitute.org/gsea/downloads.jsp)
* [http://www.baderlab.org/Software/EnrichmentMap/Tutorial](http://www.baderlab.org/Software/EnrichmentMap/Tutorial)
