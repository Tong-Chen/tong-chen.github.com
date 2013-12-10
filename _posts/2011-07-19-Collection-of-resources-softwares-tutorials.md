---
title: Collection of softwares and tutorials
layout: post
categories:
  - bioinformatics
  - biology
  - software
  - letter
  - tutorial
tags:
  - bioinformatics
  - tutorial
  - software
  - resource
---
####Biology

#####Sequence alignment
* [emboss][1]

* [clustawl2][2]
* [seqAN](URL:http://www.seqan.de/)

Description:SeqAn is an open source C++ library of efficient algorithms and data structures for the analysis of sequences with the focus on biological data. Our library applies a unique generic design that guarantees high performance, generality, extensibility, and integration with other libraries. SeqAn is easy to use and simplifies the development of new software tools with a minimal loss of performance.

#####Pathway analysis
* The<a href="http://solcyc.solgenomics.net/" target="_blank"> SolCyc</a> databases are [Pathway Tools][3]-based PGDBs for tomato, potato, tobacco, pepper and petunia that were created at the [Sol Genomics Network][4], and describe the small molecule metabolism of these plants.

* <a href="http://bioinformatics.ai.sri.com/ptools/" target="_blank">Pathway Tools</a>。

##### Protein attribute and protein-protein interactions

* [PredictProtein](http://www.predictprotein.org/)

Description: PredictProtein integrates feature prediction for secondary structure, solvent accessibility, transmembrane helices, globular regions, coiled-coil regions ,structural switch regions, B-values, disorder regions, intra-residue contacts, protein-protein and protein-DNA binding sites, sub-cellular localization, domain boundaries, beta-barrels, cysteine bonds, metal binding sites and disulphide bridge

<span style="color: #ff00ff;">Evaluation</span>:  Not done yet.

<span style="color: #ff00ff;">Usage</span>: Web server and Debian package

<span style="color: #ff00ff;">Pros</span>: see mirror

<span style="color: #ff00ff;">Cons</span>: see mirror

<span style="color: #ff00ff;">Publication</span>:http://www.ncbi.nlm.nih.gov/pubmed/15215403[ref:718, 20111127]

<span style="color: #ff00ff;">Demands</span>: Academic users can get 3 free times in one year.

<span style="color: #ff00ff;">Mirror</span>:http://hpdb.hbu.cn/thesis/2005/jy/index.asp

&nbsp;

6.GenomeTools

URL:http://genometools.org/

Description: The *GenomeTools* genome analysis system is a  free collection of bioinformatics tools (in the realm of genome informatics[visualization, mapping, repeat, genomebrowser ]) combined into a single binary named <tt>gt</tt>. It is based on a C library named “libgenometools” which consists of several modules.

&nbsp;

7.*GenomeThreader*

URL:http://genomethreader.org/

Description:*GenomeThreader* is a software tool to compute gene structure predictions. The gene structure predictions are calculated using a similarity-based approach where additional cDNA/EST and/or protein sequences are used to predict gene structures via spliced alignments. *GenomeThreader* was motivated by disabling limitations in [ *GeneSeqer*][5], a popular gene prediction program which is widely used for plant genome annotation.

Evaluation: Plant prediction, plantGDB usage.

Usage: Free of charge for non-commercial usage.

Publication: http://dl.acm.org/citation.cfm?id=1709691.1709739[ref:47, 20111127]

&nbsp;

&nbsp;

&nbsp;


&nbsp;

9.Mobyle

URL:https://projets.pasteur.fr/wiki/mobyle

Description:Mobyle is a framework and web portal specifically aimed at the integration of bioinformatics software and databanks. An integrative platform can do many things.

Publication:http://dx.doi.org/10.1093/bioinformatics/btp493[ref:44, 20111125]

&nbsp;

10.FunNet

URL:http://www.funnet.info/

Description:FunNet is an original integrative tool for exploring transcriptional interactions in microarray gene expression datasets. The analytical approach implemented in FunNet relies on knowledge extracted from public annotation databases to improve the biological relevance of the modular interaction patterns identified in co-expression networks.

Evaluation: worth a try

&nbsp;

11.Expression Profiler at the EBI

URL:http://www.ebi.ac.uk/expressionprofiler/

Description:Expression Profiler: Next Generation is an open, extensible web-based collaborative platform for microarray gene expression, sequence and PPI data analysis, exposing distinct chainable components for clustering, pattern discovery, statistics (thru R), machine-learning algorithms and visualization.

Publication:<cite>nar.oxfordjournals.org/content/32/suppl_2/W465.full[ref:96, 20111125]</cite>

Evalution: great

&nbsp;

12.**EGAN: Exploratory Gene Association Networks**

URL:http://akt.ucsf.edu/EGAN/

Description:**EGAN** is a software tool that allows a **bench biologist** to visualize and interpret the results of high-throughput exploratory assays in an interactive hypergraph of **genes**, **relationships** (*protein-protein interactions, literature co-occurrence, etc.*) and **meta-data** (*annotation, signaling pathways, etc.*). EGAN provides comprehensive, automated calculation of **meta-data coincidence** (*over-representation, enrichment*) for user- and assay-defined **gene lists**, and provides direct links to **web resources and literature** (*NCBI Entrez Gene, PubMed, KEGG, Gene Ontology, iHOP, Google, etc.*).

Publication:http://bioinformatics.oxfordjournals.org/cgi/pmidlookup?view=long&pmid=19933825[ref:9, 20111125]

Evaluation: interesting****

&nbsp;

#####Genome browser
* IGV

URL:http://www.broadinstitute.org/igv/

Description:The **Integrative Genomics Viewer (IGV)** is a high-performance visualization tool for interactive exploration of large, integrated datasets. It supports a wide variety of data types including sequence alignments, microarrays, and genomic annotations.

Evaluation: Very well.

* [genoPlotR](http://genoplotr.r-forge.r-project.org/)

14.Pathway Commons

URL:http://www.pathwaycommons.org/pc/home.do

Description: Browse and search pathways across multiple valuable public pathway databases.**** Download an integrated set of pathways in BioPAX format for global analysis.

Evaluation:Looks great, but no graphical output. It has API and can work as a plugin of Cytoscape

Publication:http://nar.oxfordjournals.org/content/early/2010/11/10/nar.gkq1039.abstract[ref:19, 20111125]

&nbsp;

15.QuickGO

URL:http://www.ebi.ac.uk/QuickGO/

Description:<a href="http://www.ebi.ac.uk/QuickGO/" rel="external">QuickGO</a> is a web-based tool that allows easy browsing of the Gene Ontology (GO) and all associated electronic and manual GO annotations provided by the GO Consortium annotation groups. QuickGO offers a range of facilities including bulk downloads of GO annotation data which can be extensively filtered by a range of different parameters and GO slim set generation.

Feature: farther term, child term, co-occuring terms.

Evaluation: Very good

&nbsp;

16.<a href="http://cgap.nci.nih.gov/Genes/GOBrowser" rel="external">CGAP GO browser</a>

URL:http://cgap.nci.nih.gov/Genes/GOBrowser

Description:With the <a href="http://cgap.nci.nih.gov/Genes/GOBrowser" rel="external">CGAP GO browser</a>, you can browse through the GO vocabularies, and find human and mouse genes assigned to each term.

Evaluation: maybe useful.

&nbsp;

17.STRAP

URL:http://www.bumc.bu.edu/cardiovascularproteomics/cpctools/strap/

Description:STRAP, the Software Tool for Rapid Annotation of Proteins, saves you time by automatically annotating a protein list with information that helps you meaningfully interpret your mass spectrometry data.

Publication:<cite>pubs.acs.org/doi/abs/10.1021/ac901335x[ref:19, 20111125]</cite>

&nbsp;

18.Manatee

<cite></cite>URL:http://manatee.sourceforge.net/

Description:Manatee is a web-based tool used to perform manual functional annotation. It has been specifically designed to optimize the ability of curators to evaluate all available sequence-based and experimental data to assign the best possible annotation to a given gene product.  
Manatee allows users to view, modify, and store annotation through interactions with an underlying relational database where all of the information is stored. Manatee supports the storage of multiple types of functional annotation including protein names, gene symbols, EC numbers, Gene Ontology terms, and associated supporting evidence. In addition, Manatee provides summary views of statistics and information from the genome as a whole.

Evaluation: Jcvi and Tiger

&nbsp;

19.PINGO

URL:http://www.psb.ugent.be/esb/PiNGO/Home.html

Description:PiNGO is a Java-based tool to easily find unknown genes in a network that are significantly associated with user-defined target [Gene Ontology][6] (GO) categories. PiNGO is implemented as a plugin for [Cytoscape][7], a popular open source software platform for visualizing and integrating molecular interaction networks. PiNGO predicts the categorization of a gene based on the annotations of its neighbors, using the enrichment statistics of its sister tool [BiNGO][8]. Networks can either be selected from the Cytoscape interface or uploaded from file. The main advantage of PiNGO is its flexibility. PiNGO also takes full advantage of Cytoscape&#8217;s versatile visualization environment.

&nbsp;

20.LEMONE

URL:http://bioinformatics.psb.ugent.be/software/details/LeMoNe

Description:LeMoNe is a software package for Learning Module Networks from gene expression data.

Evaluation: Not known

21.ENIGMA

URL:http://bioinformatics.psb.ugent.be/ENIGMA/

Description: <span style="font-family: Arial; font-size: medium;"><em>ENIGMA </em></span> <span style="font-family: Arial; font-size: small;">is a software tool to extract gene expression modules from perturbational microarray data, based on the use of combinatorial statistics and graph-based clustering. The modules are further characterized by incorporating other data types, e.g. GO annotation, protein interactions and transcription factor binding information, and by suggesting regulators that might have an effect on the expression of (some of) the genes in the module.</span>

Feature: A little old.

&nbsp;

22.G-SESAME

URL:http://bioinformatics.clemson.edu/G-SESAME/index.php

Description:*Gene Semantic Similarity Analysis and Measurement Tools. *

Feature: Compare two genes or go terms for their semantics similarity.**  Very slow.

&nbsp;

23.ToppGene suit

URL:http://toppgene.cchmc.org/

Description:A one-stop portal for gene list enrichment analysis and candidate gene prioritization  
based on functional annotations and protein interactions network .

Feature: qi

&nbsp;

24. TXTGate

URL:http://tomcat.esat.kuleuven.be/txtgate/

Description:TXTGate is a literature index database and is part of an experimental platform to evaluate (combinations of) information extraction and indexing from a variety of biological annotation databases. It is designed towards the summarization and analysis of groups of genes based on text.

Feature:

Publication: http://genomebiology.com/2004/5/6/R43[ref:64, 20111125]

&nbsp;

&nbsp;

25. DAVID

URL:http://david.abcc.ncifcrf.gov/

Description:

![][9]  Identify enriched biological themes, particularly GO terms  
![][9]  Discover enriched functional-related gene groups  
![][9]  Cluster redundant annotation terms  
![][9]  Visualize genes on BioCarta & KEGG pathway maps  
![][9]  Display related many-genes-to-many-terms on 2-D view.  
![][9]  Search for other functionally related genes not in the list  
![][9]  List interacting proteins  
![][9]  Explore gene names in batch  
![][9]  Link gene-disease associations  
![][9]  Highlight protein functional domains and motifs  
![][9]  Redirect to related literatures  
![][9]  Convert gene identifiers from one type to another.  
![][9]  And more

Feature:

Evaluation: great

&nbsp;

26.FunSpec

URL:http://funspec.med.utoronto.ca/

Description:FunSpec (an acronym for &#8220;Functional Specification&#8221;) inputs a list of yeast gene names, and outputs a summary of functional classes, cellular localizations, protein complexes, etc. that are enriched in the list.

&nbsp;

27.FunCluster

URL:http://corneliu.henegar.info/FunCluster.htm

Description:&#8221;FunCluster&#8221; is a genomic data analysis algorithm which performs functional analysis of  gene expression data obtained from cDNA microarray experiments. Besides automated functional annotation of gene expression data, FunCluster functional analysis aims to detect co-regulated biological processes through a specially designed clustering procedure involving biological annotations and gene expression data.

Feature: Algorithm may be useful.

&nbsp;

28.FuncAssociate 2.0

URL:http://llama.med.harvard.edu/cgi/func/funcassociate

Description:<a href="http://llama.med.harvard.edu/cgi/func/funcassociate" rel="external">FuncAssociate</a> is a web-based tool that accepts as input a list of genes, and returns a list of GO attributes that are over- (or under-) represented among the genes in the input list.

&nbsp;

29.BLAST2GO

URL:http://www.blast2go.com/b2ghome

Description:An ALL in ONE tool for functional annotation of (novel) sequences and the analysis of annotation data.

&nbsp;

30.immport

URL:https://www.immport.org/immportWeb/home/home.do?loginType=full

Description:ImmPort, the Immunology Database and Analysis Portal, is a one stop shop to access reference and experiment data for immunologists. ImmPort provides advanced information technology support in the production, analysis, archiving, and exchange of scientific data for the diverse community of life science researchers supported by NIAID/DAIT.

Feature:

&nbsp;

31.<span style="color: #004444;">STEM</span>

URL:http://gene.ml.cmu.edu/stem/

Description:The Short Time-series Expression Miner (STEM) is a Java program for clustering, comparing, and visualizing short time series gene expression data from microarray experiments (~8 time points or fewer). STEM allows researchers to identify significant temporal expression profiles and the genes associated with these profiles and to compare the behavior of these genes across multiple conditions.

Feature: Less than 8 time points.

Evaluation: looks good

&nbsp;

32.GeneMANIA

URL:http://www.genemania.org/

Description:GeneMANIA finds other genes that are related to a set of input genes, using a very large set of functional association data. Association data include protein and genetic interactions, pathways, co-expression, co-localization and protein domain similarity. You can use GeneMANIA to find new members of a pathway or complex, find additional genes you may have missed in your screen or find new genes with a specific function, such as protein kinases. Your question is defined by the set of genes you input.

Feature:cytoscape plugin or web server

Evalutaion: Openhelix tutorial. The results are much different with Pathway studio.

&nbsp;

&nbsp;

33.BLIP

URL:http://www.blipkit.org/

Description:Blip is a collection of logic programming modules intended primarily for bioinformatics and biomedical applications, although it contains some modules which may be of more general interest. Blip is intended to be both an application library, and a deductive database/query system. Blip is written in [SWI-Prolog][10], a fast, robust and scalable implementation of ISO Prolog.

Feature:

Evaluation:

&nbsp;

34.Graphweb

URL:http://biit.cs.ut.ee/graphweb/index.cgi

Description:**GraphWeb**is a public web server for graph-based analysis of biological networks that:

*   analyses directed and undirected, weighted and unweighted heterogeneous networks of genes, proteins and microarray probesets for many eukaryotic genomes;
*   integrates multiple diverse datasets into global networks;
*   incorporates multispecies data using gene orthology mapping;
*   filters nodes and edges based on dataset support, edge weight and node annotation;
*   detects gene modules from networks using a collection of algorithms;
*   interprets discovered modules using Gene Ontology, pathways, and cis-regulatory motifs.

Publication:http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2447774/[ref；27， 20111125】

&nbsp;

35.AVIDAS

URL:http://www.strandls.com/Avadis

Description:The collection of algorithms and visualizations in AVADIS<sup>®</sup> grows as new applications using the platform are developed. Currently, the algorithms that AVADIS® platform contains range from general purpose statistical mining and modelling algorithms, to text mining algorithms, to very application-specific algorithms for microarray/NGS data analysis, QSAR modelling and biological networks analysis. AVADIS<sup>®</sup> has a collection of powerful mining algorithms like PCA, ANOVA, T-test, clustering, classification and regression methods.

Feature:

&nbsp;

&nbsp;

36.BGI WEGO

URL:http://wego.genomics.org.cn/cgi-bin/wego/index.pl

Description:Web Gene Ontology Annotation Plotting. It has become one of the daily tools for downstream gene annotation analysis, especially when performing comparative genomics tasks.

Feature: It can compare annotation of several gene lists.

&nbsp;

37.Whatizit

URL:http://www.ebi.ac.uk/webservices/whatizit/info.jsf

Description: Whatizit is a text processing system that allows you to do textmining tasks on text. The tasks come defined by the pipelines in the drop down list of the above window and the text can be pasted in the text area. The description of each individual task/pipeline can be found following the link next to the submit button. Whatizit is also a Medline abstracts retrieval/search engine. Instead of providing the text by Copy&Paste, you can launch a Medline search. The abstracts that match your search critetia are retrieved and processed by a pipeline of your choice.

&nbsp;

38.G2D

URL:http://www.ogic.ca/projects/g2d_2/

Description:<span style="font-family: helvetica;">Welcome to G2D, a database of candidate genes for mapped inherited human diseases. Candidate priorities are automatically established by a data mining algorithm that extracts putative genes in the chromosomal region where the disease is mapped, and evaluates their possible relation to the disease based on the phenotype of the disorder</span>

&nbsp;

39. Sequence Format conversion

http://sequenceconversion.bugaco.com/converter/biology/sequences/

http://www.agapow.net/software/bioscripts.convert

http://biowiki.org/StockholmTools

40. VISTA

URL:http://genome.lbl.gov/vista/index.shtml

Description:VISTA is a comprehensive suite of programs and databases for comparative analysis of genomic sequences. There are two ways of using VISTA - you can submit your own sequences and alignments for analysis (VISTA servers) or examine pre-computed whole-genome alignments of different species.

&nbsp;

41.Expasy

URL:http://www.expasy.org/

42.EBI

&nbsp;

43.Anno-J

URL:http://www.annoj.org/

Description:Anno-J is a Web 2.0 application designed for visualizing deep sequencing data and other genome annotation data. It is intended to run in modern W3C compliant browsers*, and allows flexible configuration of plugins and data streams from providers located anywhere on the internet.

&nbsp;

&nbsp;

44.JMP life science

URL:http://www.jmp.com/support/downloads/life\_sciences\_documentation/documentation.shtml

Description:Welcome to JMP Life Sciences, a powerful desktop software system for integrated statistical analysis of clinical, genetic marker, microarray, and spectral (proteomics and metabolomics, for example) data. JMP Life Sciences software consists of more than 200 independent analytical procedures (APs). The purpose of this manual is to provide you with informative examples of how to use JMP Life Sciences software to extract the maximum amount of useful information from your data.

&nbsp;

45.Mahout

URL:http://mahout.apache.org/

Description:The Apache Mahout™ machine learning library's goal is to build scalable machine learning libraries.

&nbsp;

&nbsp;

46.MATLAb Mathworks

URL:http://www.mathworks.cn/index.html

&nbsp;

47.TINKER

URL:http://dasher.wustl.edu/ffe/

Description:The TINKER molecular modeling software is a complete and general package for molecular mechanics and dynamics, with some special features for biopolymers. TINKER has the ability to use any of several common parameter sets, such as Amber (ff94, ff96, ff98, ff99, ff99SB), CHARMM (19, 22, 22/CMAP), Allinger MM (MM2-1991 and MM3-2000), OPLS (OPLS-UA, OPLS-AA), Merck Molecular Force Field (MMFF), Liam Dang's polarizable model, and the AMOEBA (2004, 2009) polarizable atomic multipole force field. Parameter sets for other widely-used force fields are under consideration for future releases.

&nbsp;

48.vigyaan

URL:http://www.vigyaancd.org/

Description:At present the following ready to use software comes on VigyaanCD: Arka/GP, Artemis, Bioperl, BLAST (NCBI-tools), ClustalW/ClustalX, Cn3D, EMBOSS tools, Garlic, Glimmer, GROMACS, Ghemical, GNU R, Gnuplot, GIMP, ImageMagick, Jmol, MPQC, MUMer, NJPlot, Open Babel, Octave, PSI3, PyMOL, Ramachandran plot viewer, Rasmol, Raster3D, Seaview, TINKER, XDrawChem, Xmgr and Xfig. GNU C/C++/Fortran compilers and additional Linux tools (such as ps2pdf) are also available.

&nbsp;

49.ghemical

URl:http://www.bioinformatics.org/ghemical/ghemical/index.html

Description:Ghemical is computational chemistry package

&nbsp;

50.MPQC

URL:http://www.mpqc.org/

Description:The Massively Parallel Quantum Chemistry Program MPQC is the Massively Parallel Quantum Chemistry Program. It computes properties of atoms and molecules from first principles using the time independent Schrödinger equation. It runs on a wide range of architectures ranging from individual workstations to symmetric multiprocessors to massively parallel computers.

&nbsp;

51.GLIMMER

URl:http://www.cbcb.umd.edu/software/glimmer/

Description:Glimmer is a system for finding genes in microbial DNA, especially the genomes of bacteria, archaea, and viruses. Glimmer (Gene Locator and Interpolated Markov ModelER) uses interpolated Markov models (IMMs) to identify the coding regions and distinguish them from noncoding DNA.

&nbsp;

52.STADEN

URL:http://staden.sourceforge.net/

DEscription:This is a free to academics (charge for commercial users) package including sequence assemble, trace viewing/editing and sequence analysis tools. It also includes a GUI to the free EMBOSS suite.

&nbsp;

53.[NetSurfP][11] -

Description:Protein Surface Accessibility and Secondary Structure Predictions

&nbsp;

54.[NetTurnP][12]

Description: Prediction of Beta-turn regions in protein sequences

&nbsp;

55.[MODELLER][13]

Description: Used for homology or comparative modeling of protein three-dimensional structures

&nbsp;

56.<a href="http://autodock.scripps.edu/" rel="nofollow">AutoDock</a>

Description:Suite of Automated Docking Tools

<a href="http://www.gromacs.org/" rel="nofollow">57.Gromacs</a>

URL:http://www.gromacs.org

Description: A molecular dynamics package primarily designed for biomolecular systems such as proteins and lipids. GROMACS is a versatile package to perform molecular dynamics, i.e. simulate the Newtonian equations of motion for systems with hundreds to millions of particles.

&nbsp;

58.Pymol

URl:http://en.wikipedia.org/wiki/Pymol

Description:**yMOL** is an open-source, user-sponsored, molecular visualization system created by [Warren Lyford DeLano][14] and commercialized by DeLano Scientific LLC, which is a private software company dedicated to creating useful tools that become universally accessible to scientific and educational communities. It can produce high quality 3D images of small [molecules][15] and biological [macromolecules][16], such as [proteins][17]. According to the author, almost a quarter of all published images of 3D protein structures in the scientific literature were made<sup>[<em><a title="Wikipedia:Manual of Style (dates and numbers)" href="http://en.wikipedia.org/wiki/Wikipedia:Manual_of_Style_%28dates_and_numbers%29#Chronological_items">when?</a></em>]</sup> using PyMOL.

&nbsp;

59.STING

URL:http://www.cbi.cnptia.embrapa.br/SMS

Description:STING (**S**equence **T**o and with**IN** **G**raphics) is a free Web-based suite of programs for a comprehensive analysis of the relationship between protein sequence, structure, function, and stability.

&nbsp;

60.MEME

URL:http://meme.nbcr.net

Description:Motif-based sequence analysis tools

&nbsp;

61.Cluster

URL:http://www.rocksclusters.org/wordpress/

&nbsp;

62.Geneinfo

URL:http://code.google.com/p/geneinfo/

Description:Application to retrieve gene information from various sources

&nbsp;

63.ProtFun

URL:http://www.cbs.dtu.dk/services/ProtFun/

Description:The ProtFun 2.2 server produces * ab initio * predictions of protein function from sequence. The method queries a large number of other feature prediction servers to obtain information on various post-translational and localizational aspects of the protein, which are integrated into final predictions of the cellular role, enzyme class (if any), and selected Gene Ontology categories of the submitted sequence.

&nbsp;

64.Annotea

URL:http://www.w3.org/2001/Annotea/

Description:Annotea is a W3C <acronym title="Live Early Adoption and Demonstration"><a href="http://www.w3.org/DesignIssues/Architecture.html#Collaboration">LEAD</a></acronym> (Live Early Adoption and Demonstration) project under [Semantic Web Advanced Development][18] (SWAD).

&nbsp;

65.Protein structure

URL:http://predictioncenter.org/

&nbsp;

&nbsp;

66.BWA

&nbsp;

67.BOWTIE

&nbsp;

68.KAKS

&nbsp;

69.Phostcon

&nbsp;

70.EBI的基因全局搜索，关键词全局搜索，特定基因及其家族。

&nbsp;

71.UGENE

URL:http://ugene.unipro.ru/

Description:

*   New tools: MrBayes, BWA (all platforms), update of Bowtie and BLAST tools
*   Short reads assembly viewer: performance and reads coloring improvements
*   Work with large data sets: open, view and annotate huge DNA files on a usual desktop
*   Workflow designer: new data filtering elements
*   Sequence viewer: new DNA flexibility and GC Frame Plot graphs
*   All in one package: download UGENE, documentation and external tools in a single file!

72.Phobos

URL:http://www.ruhr-uni-bochum.de/spezzoo/cm/cm_phobos.htm

Description:**a tandem repeat search tool for complete genomes**

&nbsp;

73.TRedD

URL:http://tandem.sci.brooklyn.cuny.edu/

Description:TANDEm repeats databse and finding software

&nbsp;

74.CREAD

URL:http://rulai.cshl.edu/cread/index.shtml

Description:Comprehensive Regulatory Element Analysis and Discovery

&nbsp;

75.miRfocus

URL:http://www.mirfocus.org

76.mummer

URL:http://mummer.sourceforge.net/

77.Pathway related  
URL:http://www.genecloud.org/#1098693  
Gene Cloud (genecloud.org) is a novel tool presenting gene-gene associations based on the scientific literature. It was developed by the Knockout Mouse Repository (www.komp.org) to help our customers find products related to other products they chose. We have built a detailed graph model of gene-gene associations based on how many times two genes are cited in the same article. If two genes are cited in many papers together, they are considered strongly connected.

&nbsp;

78.

###  Pathway.Enrichment Analysis Tools

<div>
</div>

<div id="post-body-7540133092384063804">
  <a href="http://www.broud.mit.edu/gsea/">GSEA</a><br /> <a href="http://www.david.niaid.nih.gov/">DAVID</a><br /> <a href="http://discover.nci.nih.gov/gominer">GOMiner</a><br /> <a href="http://www.babelomics.org/">Babelomics</a><br /> <a href="http://www.genmapp.org/">MAPPFinder</a><a href="http://gostat.wehi.edu.au/">GOStats</a><br /> <a href="http://vortex.cs.wayne.edu/ontoexpress/">Ontotools</a><br /> <a href="http://genereg.ornl.gov/gotm/">GOTM</a><br /> <a href="http://funspec.med.utoronto.ca/">FunSpec</a><br /> <a href="http://www.oeb.harvard.edu/hartl/lab/publications/GeneMerge.html">GeneMerge</a><a href="http://llama.med.harvard.edu/Software.html">FuncAssociate</a><br /> <a href="http://gin.univ-mrs.fr/GOToolBox">GOToolBox</a><br /> <a href="http://www.medinfopoli.polimi.it/GFINDer/">GFINDer</a><br /> <a href="http://bioinfo.vanderbilt.edu/webgestalt/">WebGestalt</a><br /> <a href="http://microarraysunife.it/">GOAL</a><a href="http://pathwayexplorer.genome.tugraz.at/">Pathway Explorer</a><br /> <a href="http://dulci.biostat.duke.edu/pathways/">PLAGE</a><br /> <a href="http://www.t-profiler.org/">t-profiler</a><br /> <a href="http://blasto.iq.usp.br/~tkoide/BayGO/">WebBayGO</a><br /> <a href="http://www.jprogo.de/">JProGO</a><a href="http://array.kobic.re.kr/ADGO">ADGO</a><br /> <a href="http://genetrail.bioinf.uni-sb.de/">GeneTrail</a><br /> <a href="http://integromics.kobic.re.kr/GAzer/index.faces">GAZER</a><br /> <a href="http://bioinfoserver.rsbs.anu.edu.au/utils/PathExpress">PathExpress</a>&nbsp;</p> <p>
    Picture related tools:
  </p>
  
  <p>
    1.protein domain
  </p>
  
  <p>
    http://prosite.expasy.org/cgi-bin/prosite/mydomains/
  </p>
  
  <p>
    2.Exon-intron
  </p>
  
  <p>
    http://wormweb.org/exonintron
  </p>
  
  <p>
    3.Map protein domain to gene exon and get record from NCBI
  </p>
  
  <p>
    http://code.google.com/p/variationtoolkit/
  </p>
  
  <p>
    4.bioGPS
  </p>
  
  <p>
    5.bioGraph
  </p>
  
  <p>
    &nbsp;
  </p>
</div>

* [Drugable](http://drugable.com/)


##### Network
1.Pajek

http://vlado.fmf.uni-lj.si/pub/networks/pajek/

 [1]: http://emboss.sourceforge.net/docs/emboss_tutorial/emboss_tutorial.html
 [2]: ftp://ftp.ebi.ac.uk/pub/software/clustalw2/
 [3]: http://bioinformatics.ai.sri.com/ptools/
 [4]: http://solgenomics.net/
 [5]: http://bioinformatics.iastate.edu/cgi-bin/gs.cgi
 [6]: http://www.geneontology.org/ "http://www.geneontology.org/"
 [7]: http://www.cytoscape.org/ "http://www.cytoscape.org/"
 [8]: http://www.psb.ugent.be/cbd/papers/BiNGO "http://www.psb.ugent.be/cbd/papers/BiNGO"
 [9]: http://david.abcc.ncifcrf.gov/images/check.gif
 [10]: http://www.swi-prolog.org/
 [11]: http://bioinformatics.org/w/index.php?title=NetSurfP&action=edit&redlink=1 "NetSurfP (page does not exist)"
 [12]: http://bioinformatics.org/wiki/NetTurnP "NetTurnP"
 [13]: http://bioinformatics.org/wiki/MODELLER "MODELLER"
 [14]: http://en.wikipedia.org/wiki/Warren_Lyford_DeLano "Warren Lyford DeLano"
 [15]: http://en.wikipedia.org/wiki/Molecule "Molecule"
 [16]: http://en.wikipedia.org/wiki/Macromolecule "Macromolecule"
 [17]: http://en.wikipedia.org/wiki/Protein "Protein"
 [18]: http://www.w3.org/2000/01/sw/
