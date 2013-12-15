---
title: Documents for using parseGTF.py
layout: post
categories:
  - python
  - scripts
tags:
  - python
---

#####Introduction

This post describes the usage of program [`parseGTF.py`][3] as well as [`sortGTF.py`][4].

The [GTF(General Transfer Format)][1] file save a subset of biological sequence also known as a feature in one line to faciliate adding and computing. 

Here GTF file mainly refers to gene annotation file got from UCSC. Please check [UCSC usage][2] to see how to get RefSeq gene or UCSC gene annotation file in GTF format or other format. Besides, you can also get gene annotation file as well as sub-gene regions like 5' UTR, 3'UTR and coding exons in `bed` format simultaneously. 

But what would you do if you want to extract the above mentioned sub-gene regions when you already have a GTF file. It may be very hard to extract the sub-gene regions from UCSC since the version of GTF file in UCSC is updated since you last access. If you remember the version number of your GTF annotation, there may be a way to get the sub-gene regions corresponding to that version. But I did not try it. Besides, what would you do if the GTF file is got from other place, or you want to get other sub-regions which can not be got from UCSC directly like the mRNA regions flanking start codon and stop codon? 

The script `parseGTF.py` is designed to solve this problem. It takes a sorted GTF and a chromosome-size file as input and outputs all regions mentioned above as showed below. 

#####Evaluation
I have tested this script for various gene structures in mouse RefSeq gene annotation and all works well. Besides, the output result of this script matches very well with sub-regions directly got from UCSC. However, there may still contain other bugs that I have not noticed. If you found one, please let me know.

#####Usage
* Require two files, one is GTF file, the other is chromsome-size file. Please also check [UCSC usage][2] to see how to get this file. 
* Sort GTF file using `sortGTF.py`.
{% highlight bash %}
sortGTF.py mm9.gene.refgene.gtf > mm9.gene.refgene.sorted.gtf
{% endhighlight %}
* Parse GTF file using `parseGTF.py`
{% highlight bash %}
parseGTF.py mm9.gene.refgene.sorted.gtf mm9.chrom.sizes >mm9.gene.refgene.gtf.bed
{% endhighlight %}


#####File formats

* Output file format
  * TSS represents transcription start site while TTS represents translation terminal site. TSS500 represents 500 nt regions centered by TSS. TSS-UP0-500 represents the upstream 500 nt regions of TSS. TSS-DW0-500 represents the downstream 500 nt regions of TSS.

> chr17	25377309	25377388	NM\_026676\_11.Intron.1	0	+

> chr17	25377197	25377309	NM\_026676\_11.Coding\_exon.1	0	+

> chr17	25377608	25378008	NM\_026676\_11.Intron.2	0	+

> chr17	25378202	25378632	NM\_026676\_11.Intron.3	0	+

> chr17	25378806	25379103	NM\_026676\_11.Intron.4	0	+

> chr17	25379167	25379398	NM\_026676\_11.Intron.5	0	+

> chr17	25377388	25377608	NM\_026676\_11.Coding\_exon.2	0	+

> chr17	25378008	25378202	NM\_026676\_11.Coding\_exon.3	0	+

> chr17	25378632	25378806	NM\_026676\_11.Coding\_exon.4	0	+

> chr17	25379103	25379167	NM\_026676\_11.Coding\_exon.5	0	+

> chr17	25379398	25379606	NM\_026676\_11.Coding\_exon.6	0	+

> chr17	25377114	25379744	NM\_026676\_11	0610007P22Rik	+

> chr17	25376864	25377364	NM\_026676\_11.TSS500	0	+

> chr17	25379493	25379993	NM\_026676\_11.TTS500	0	+

> chr17	25376614	25377614	NM\_026676\_11.TSS1000	0	+

> chr17	25379243	25380243	NM\_026676\_11.TTS1000	0	+

> chr17	25376114	25378114	NM\_026676\_11.TSS2000	0	+

> chr17	25378743	25380743	NM\_026676\_11.TTS2000	0	+

> chr17	25374614	25379614	NM\_026676\_11.TSS5000	0	+

> chr17	25377243	25382243	NM\_026676\_11.TTS5000	0	+

> chr17	25376614	25377114	NM\_026676\_11.TSS-UP0-500	0	+

> chr17	25379743	25380243	NM\_026676\_11.TTS-DW0-500	0	+

> chr17	25376114	25376614	NM\_026676\_11.TSS-UP500-1000	0	+

> chr17	25380243	25380743	NM\_026676\_11.TTS-DW500-1000	0	+

> chr17	25375114	25376114	NM\_026676\_11.TSS-UP1000-2000	0	+

> chr17	25380743	25381743	NM\_026676\_11.TTS-DW1000-2000	0	+

> chr17	25372114	25375114	NM\_026676\_11.TSS-UP2000-5000	0	+

> chr17	25381743	25384743	NM\_026676\_11.TTS-DW2000-5000	0	+

> chr17	25377114	25377197	NM\_026676\_11.UTR5	0	+

> chr17	25379606	25379744	NM\_026676\_11.UTR3	0	+

* Input file format
    * All types of special GTF structures processed during writing scripts

> chr2	refGene	stop\_codon	176083705	176083707	.	-	0	gene\_id "100043387"; transcript\_id "NM\_001099327"; exon\_number "1"; exon\_id "NM\_001099327.1"; gene\_name "100043387";

> chr2	refGene	exon	176083705	176085010	.	-	.	gene\_id "100043387"; transcript\_id "NM\_001099327"; exon\_number "1"; exon\_id "NM\_001099327.1"; gene\_name "100043387";

> chr2	refGene	exon	176086169	176086229	.	-	.	gene\_id "100043387"; transcript\_id "NM\_001099327"; exon\_number "2"; exon\_id "NM\_001099327.2"; gene\_name "100043387";

> chr2	refGene	exon	176086435	176086561	.	-	.	gene\_id "100043387"; transcript\_id "NM\_001099327"; exon\_number "3"; exon\_id "NM\_001099327.3"; gene\_name "100043387";

> chr2	refGene	start\_codon	176093582	176093584	.	-	0	gene\_id "100043387"; transcript\_id "NM\_001099327"; exon\_number "1"; exon\_id "NM\_001099327.1"; gene\_name "100043387";

> chr2	refGene	exon	176093582	176093636	.	-	.	gene\_id "100043387"; transcript\_id "NM\_001099327"; exon\_number "4"; exon\_id "NM\_001099327.4"; gene\_name "100043387";

> chr2	refGene	exon	176097100	176097171	.	-	.	gene\_id "100043387"; transcript\_id "NM\_001099327"; exon\_number "5"; exon\_id "NM\_001099327.5"; gene\_name "100043387";

> chr4	refGene	exon	41452042	41452201	.	-	.	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "1"; exon\_id "NM\_001048005.1"; gene\_name "1110017D15Rik";

> chr4	refGene	stop\_codon	41452601	41452603	.	-	0	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "1"; exon\_id "NM\_001048005.1"; gene\_name "1110017D15Rik";

> chr4	refGene	exon	41452601	41452687	.	-	.	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "2"; exon\_id "NM\_001048005.2"; gene\_name "1110017D15Rik";

> chr4	refGene	exon	41454132	41454361	.	-	.	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "3"; exon\_id "NM\_001048005.3"; gene\_name "1110017D15Rik";

> chr4	refGene	exon	41454554	41454626	.	-	.	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "4"; exon\_id "NM\_001048005.4"; gene\_name "1110017D15Rik";

> chr4	refGene	exon	41455550	41455662	.	-	.	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "5"; exon\_id "NM\_001048005.5"; gene\_name "1110017D15Rik";

> chr4	refGene	exon	41458465	41458609	.	-	.	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "6"; exon\_id "NM\_001048005.6"; gene\_name "1110017D15Rik";

> chr4	refGene	exon	41464061	41464366	.	-	.	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "7"; exon\_id "NM\_001048005.7"; gene\_name "1110017D15Rik";

> chr4	refGene	start\_codon	41464193	41464195	.	-	0	gene\_id "1110017D15Rik"; transcript\_id "NM\_001048005"; exon\_number "1"; exon\_id "NM\_001048005.1"; gene\_name "1110017D15Rik";

> chr10	refGene	exon	79635689	79635919	.	+	.	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "1"; exon\_id "NM\_027207.1"; gene\_name "1600002K03Rik";

> chr10	refGene	start\_codon	79635711	79635713	.	+	0	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "1"; exon\_id "NM\_027207.1"; gene\_name "1600002K03Rik";

> chr10	refGene	exon	79636954	79637070	.	+	.	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "2"; exon\_id "NM\_027207.2"; gene\_name "1600002K03Rik";

> chr10	refGene	stop\_codon	79637069	79637070	.	+	0	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "1"; exon\_id "NM\_027207.1"; gene\_name "1600002K03Rik";

> chr10	refGene	stop\_codon	79637562	79637562	.	+	1	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "1"; exon\_id "NM\_027207.1"; gene\_name "1600002K03Rik";

> chr10	refGene	exon	79637562	79637864	.	+	.	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "3"; exon\_id "NM\_027207.3"; gene\_name "1600002K03Rik";

> chr7	refGene	exon	97273346	97273542	.	-	.	gene\_id "2310010J17Rik"; transcript\_id "NR\_046007"; exon\_number "1"; exon\_id "NR\_046007.1"; gene\_name "2310010J17Rik";

> chr7	refGene	exon	97275438	97275554	.	-	.	gene\_id "2310010J17Rik"; transcript\_id "NR\_046007"; exon\_number "2"; exon\_id "NR\_046007.2"; gene\_name "2310010J17Rik";

> chr7	refGene	exon	97278382	97278446	.	-	.	gene\_id "2310010J17Rik"; transcript\_id "NR\_046007"; exon\_number "3"; exon\_id "NR\_046007.3"; gene\_name "2310010J17Rik";

> chr16	refGene	start\_codon	32271695	32271697	.	+	0	gene\_id "2310010M20Rik"; transcript\_id "NM\_183283"; exon\_number "1"; exon\_id "NM\_183283.1"; gene\_name "2310010M20Rik";

> chr16	refGene	exon	32271695	32271744	.	+	.	gene\_id "2310010M20Rik"; transcript\_id "NM\_183283"; exon\_number "1"; exon\_id "NM\_183283.1"; gene\_name "2310010M20Rik";

> chr16	refGene	exon	32273242	32273391	.	+	.	gene\_id "2310010M20Rik"; transcript\_id "NM\_183283"; exon\_number "2"; exon\_id "NM\_183283.2"; gene\_name "2310010M20Rik";

> chr16	refGene	exon	32273799	32274865	.	+	.	gene\_id "2310010M20Rik"; transcript\_id "NM\_183283"; exon\_number "3"; exon\_id "NM\_183283.3"; gene\_name "2310010M20Rik";

> chr16	refGene	stop\_codon	32274241	32274243	.	+	0	gene\_id "2310010M20Rik"; transcript\_id "NM\_183283"; exon\_number "1"; exon\_id "NM\_183283.1"; gene\_name "2310010M20Rik";



> chr7	mm9\_refGene	exon	147995576	147999213	0.000000	-	.	gene\_id "NM\_001001180"; transcript\_id "NM\_001001180"; 

> chr7	mm9\_refGene	stop\_codon	147997328	147997330	0.000000	-	.	gene\_id "NM\_001001180"; transcript\_id "NM\_001001180"; 

> chr7	mm9\_refGene	exon	148004487	148004613	0.000000	-	.	gene\_id "NM\_001001180"; transcript\_id "NM\_001001180"; 

> chr7	mm9\_refGene	start\_codon	148007934	148007936	0.000000	-	.	gene\_id "NM\_001001180"; transcript\_id "NM\_001001180"; 

> chr7	mm9\_refGene	exon	148007934	148008077	0.000000	-	.	gene\_id "NM\_001001180"; transcript\_id "NM\_001001180"; 

> chr1	mm9\_refGene	exon	58519615	58521134	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	stop\_codon	58521048	58521050	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58522839	58522957	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58524495	58524556	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58526512	58526683	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58527784	58527930	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58529149	58529245	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58531653	58531785	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58533278	58533387	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58537095	58537193	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58537804	58537997	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58540487	58540547	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58549701	58549732	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58550505	58550594	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58554220	58554309	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	exon	58558167	58558270	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr1	mm9\_refGene	start\_codon	58558258	58558260	0.000000	-	.	gene\_id "NM\_001025378"; transcript\_id "NM\_001025378"; 

> chr18	mm9\_refGene	exon	48204989	48205099	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr18	mm9\_refGene	exon	48206387	48208037	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr18	mm9\_refGene	start\_codon	48206411	48206413	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr18	mm9\_refGene	stop\_codon	48207713	48207715	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149611433	149611449	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149613582	149613675	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	start\_codon	149613591	149613593	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149615154	149615249	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149616231	149616289	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149618114	149618183	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149618350	149618483	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149619224	149619446	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149620679	149620876	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149621560	149621761	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149621940	149622048	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149622170	149622228	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	exon	149622595	149622982	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr4	mm9\_refGene	stop\_codon	149622662	149622664	0.000000	+	.	gene\_id "NM\_001025388"; transcript\_id "NM\_001025388"; 

> chr16	mm9\_refGene	exon	26581791	26581972	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26624241	26624305	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	start\_codon	26624242	26624244	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26676795	26677080	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26680189	26680375	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26692831	26692996	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26695308	26695379	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26698913	26699039	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26701174	26701322	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26710567	26710716	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26712203	26712346	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26722442	26723017	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	stop\_codon	26723017	26723017	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	stop\_codon	26723307	26723308	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr16	mm9\_refGene	exon	26723307	26725233	0.000000	+	.	gene\_id "NM\_001159317"; transcript\_id "NM\_001159317"; 

> chr1	mm9\_refGene	exon	100317701	100318074	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	start\_codon	100317783	100317785	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100319666	100319926	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100324843	100325028	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100328810	100328906	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100340205	100340323	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100343290	100343399	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100363235	100363379	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100377168	100377363	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100387074	100387227	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100392762	100392949	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100394054	100394118	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100396336	100396473	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	stop\_codon	100396473	100396473	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	stop\_codon	100405796	100405797	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chr1	mm9\_refGene	exon	100405796	100405957	0.000000	+	.	gene\_id "NM\_001164233"; transcript\_id "NM\_001164233"; 

> chrUn\_random	mm9\_refGene	exon	527839	528262	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chrUn\_random	mm9\_refGene	stop\_codon	528232	528234	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chrUn\_random	mm9\_refGene	exon	528345	528527	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chrUn\_random	mm9\_refGene	exon	528622	528742	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chrUn\_random	mm9\_refGene	exon	528831	528969	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chrUn\_random	mm9\_refGene	start\_codon	528895	528897	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chr4	mm9\_refGene	exon	41774207	41774345	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chr4	mm9\_refGene	start\_codon	41774279	41774281	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chr4	mm9\_refGene	exon	41774434	41774554	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chr4	mm9\_refGene	exon	41774649	41774831	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chr4	mm9\_refGene	exon	41774914	41775337	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chr4	mm9\_refGene	stop\_codon	41774942	41774944	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666"; 

> chrUn\_random	mm9\_refGene	exon	739163	739586	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chrUn\_random	mm9\_refGene	stop\_codon	739556	739558	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chrUn\_random	mm9\_refGene	exon	739669	739851	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chrUn\_random	mm9\_refGene	exon	739946	740066	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chrUn\_random	mm9\_refGene	exon	740155	740293	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chrUn\_random	mm9\_refGene	start\_codon	740219	740221	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chr4	mm9\_refGene	exon	41985510	41985648	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chr4	mm9\_refGene	start\_codon	41985582	41985584	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chr4	mm9\_refGene	exon	41985737	41985857	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chr4	mm9\_refGene	exon	41985952	41986134	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chr4	mm9\_refGene	exon	41986217	41986640	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chr4	mm9\_refGene	stop\_codon	41986245	41986247	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup1"; 

> chr4	mm9\_refGene	exon	42391950	42392373	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup2"; 

> chr4	mm9\_refGene	stop\_codon	42392343	42392345	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup2"; 

> chr4	mm9\_refGene	exon	42392456	42392638	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup2"; 

> chr4	mm9\_refGene	exon	42392733	42392853	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup2"; 

> chr4	mm9\_refGene	exon	42392942	42393080	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup2"; 

> chr4	mm9\_refGene	start\_codon	42393006	42393008	0.000000	-	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup2"; 

> chr4	mm9\_refGene	exon	42625655	42625793	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup3"; 

> chr4	mm9\_refGene	start\_codon	42625727	42625729	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup3"; 

> chr4	mm9\_refGene	exon	42625882	42626002	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup3"; 

> chr4	mm9\_refGene	exon	42626097	42626279	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup3"; 

> chr4	mm9\_refGene	exon	42626362	42626785	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup3"; 

> chr4	mm9\_refGene	stop\_codon	42626390	42626392	0.000000	+	.	gene\_id "NM\_001193666"; transcript\_id "NM\_001193666\_dup3"; 

> chrUn\_random	mm9\_refGene	exon	1737773	1737846	0.000000	+	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chrUn\_random	mm9\_refGene	exon	1738982	1739295	0.000000	+	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chrUn\_random	mm9\_refGene	start\_codon	1739009	1739011	0.000000	+	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chrUn\_random	mm9\_refGene	exon	1739750	1740340	0.000000	+	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chrUn\_random	mm9\_refGene	exon	1741238	1741852	0.000000	+	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chrUn\_random	mm9\_refGene	stop\_codon	1741803	1741805	0.000000	+	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chr5	mm9\_refGene	exon	94495480	94496094	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chr5	mm9\_refGene	stop\_codon	94495527	94495529	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chr5	mm9\_refGene	exon	94496992	94497582	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chr5	mm9\_refGene	exon	94498037	94498350	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chr5	mm9\_refGene	start\_codon	94498321	94498323	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chr5	mm9\_refGene	exon	94499498	94499571	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457"; 

> chr5	mm9\_refGene	exon	96161111	96161725	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457\_dup1"; 

> chr5	mm9\_refGene	stop\_codon	96161158	96161160	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457\_dup1"; 

> chr5	mm9\_refGene	exon	96162623	96163213	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457\_dup1"; 

> chr5	mm9\_refGene	exon	96163668	96163981	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457\_dup1"; 

> chr5	mm9\_refGene	start\_codon	96163952	96163954	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457\_dup1"; 

> chr5	mm9\_refGene	exon	96165119	96165192	0.000000	-	.	gene\_id "NM\_001270457"; transcript\_id "NM\_001270457\_dup1"; 

> chr17	mm9\_refGene	exon	31298341	31298538	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr17	mm9\_refGene	stop\_codon	31298522	31298524	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr17	mm9\_refGene	exon	31299600	31299752	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr17	mm9\_refGene	exon	31301872	31301998	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr17	mm9\_refGene	start\_codon	31301963	31301965	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr5	mm9\_refGene	exon	143285577	143285774	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr5	mm9\_refGene	stop\_codon	143285758	143285760	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr5	mm9\_refGene	exon	143286836	143286988	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr5	mm9\_refGene	exon	143289108	143289234	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr5	mm9\_refGene	start\_codon	143289199	143289201	0.000000	-	.	gene\_id "NM\_009362"; transcript\_id "NM\_009362"; 

> chr11	mm9\_refGene	exon	68902030	68902129	0.000000	+	.	gene\_id "NM\_009497"; transcript\_id "NM\_009497"; 

> chr11	mm9\_refGene	start\_codon	68902128	68902129	0.000000	+	.	gene\_id "NM\_009497"; transcript\_id "NM\_009497"; 

> chr11	mm9\_refGene	start\_codon	68902608	68902608	0.000000	+	.	gene\_id "NM\_009497"; transcript\_id "NM\_009497"; 

> chr11	mm9\_refGene	exon	68902608	68902728	0.000000	+	.	gene\_id "NM\_009497"; transcript\_id "NM\_009497"; 

> chr11	mm9\_refGene	exon	68903233	68903391	0.000000	+	.	gene\_id "NM\_009497"; transcript\_id "NM\_009497"; 

> chr11	mm9\_refGene	exon	68903478	68903529	0.000000	+	.	gene\_id "NM\_009497"; transcript\_id "NM\_009497"; 

> chr11	mm9\_refGene	exon	68904152	68905883	0.000000	+	.	gene\_id "NM\_009497"; transcript\_id "NM\_009497"; 

> chr11	mm9\_refGene	stop\_codon	68904166	68904168	0.000000	+	.	gene\_id "NM\_009497"; transcript\_id "NM\_009497"; 

> chrY	mm9\_refGene	exon	155156	155257	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	start\_codon	157264	157266	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	157264	157380	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	157495	157550	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	157635	157803	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	157893	158027	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	158589	158695	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	158902	158992	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	159587	159719	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	161891	161988	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	162085	162231	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	162342	162518	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	162621	162725	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	162814	162894	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	163205	163360	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	165209	165374	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	165584	165780	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	167702	167766	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	168018	168213	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	168767	168841	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	168947	169139	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	170618	170706	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	178411	178503	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	178623	178814	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	179367	179468	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	179577	179677	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	exon	179830	180667	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY	mm9\_refGene	stop\_codon	179963	179965	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43172478	43172579	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	start\_codon	43174586	43174588	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43174586	43174702	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43174817	43174872	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43174957	43175125	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43175215	43175349	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43175911	43176017	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43176224	43176314	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43176909	43177041	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43179213	43179310	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43179407	43179553	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43179664	43179840	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43179943	43180047	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43180136	43180216	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43180527	43180682	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43182531	43182696	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43182906	43183102	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43185024	43185088	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43185340	43185535	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43186089	43186163	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43186269	43186461	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43187940	43188028	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43195733	43195825	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43195945	43196136	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43196689	43196790	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43196899	43196999	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	exon	43197152	43197989	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chrY\_random	mm9\_refGene	stop\_codon	43197285	43197287	0.000000	+	.	gene\_id "NM\_011667"; transcript\_id "NM\_011667"; 

> chr12	mm9\_refGene	exon	31596534	31597092	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	start\_codon	31597092	31597092	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	start\_codon	31607100	31607101	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31607100	31607210	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31609629	31609742	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31611675	31611739	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31624439	31624551	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31625156	31625284	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31626832	31626994	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31627655	31627733	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31643713	31643769	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	exon	31644669	31645014	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr12	mm9\_refGene	stop\_codon	31644857	31644859	0.000000	+	.	gene\_id "NM\_013709"; transcript\_id "NM\_013709"; 

> chr17\_random	mm9\_refGene	exon	581195	581311	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	exon	600251	600446	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	start\_codon	600275	600277	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	exon	602234	602362	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	exon	604618	604715	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	exon	609590	609716	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	exon	610273	610367	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	exon	611771	611951	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	exon	612164	612733	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17\_random	mm9\_refGene	stop\_codon	612274	612276	0.000000	+	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	exon	54100940	54101509	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	stop\_codon	54101397	54101399	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	exon	54101722	54101902	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	exon	54103306	54103400	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	exon	54103957	54104083	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	exon	54108958	54109055	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	exon	54111311	54111439	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	exon	54113227	54113422	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	start\_codon	54113396	54113398	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr17	mm9\_refGene	exon	54129840	54129956	0.000000	-	.	gene\_id "NM\_018751"; transcript\_id "NM\_018751"; 

> chr11	mm9\_refGene	exon	79314484	79316529	0.000000	-	.	gene\_id "NM\_019409"; transcript\_id "NM\_019409"; 

> chr11	mm9\_refGene	stop\_codon	79315201	79315203	0.000000	-	.	gene\_id "NM\_019409"; transcript\_id "NM\_019409"; 

> chr11	mm9\_refGene	start\_codon	79317405	79317407	0.000000	-	.	gene\_id "NM\_019409"; transcript\_id "NM\_019409"; 

> chr11	mm9\_refGene	exon	79317405	79317584	0.000000	-	.	gene\_id "NM\_019409"; transcript\_id "NM\_019409"; 

> chr10	mm9\_refGene	exon	127496038	127496342	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	start\_codon	127496341	127496342	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	start\_codon	127505728	127505728	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	exon	127505728	127505841	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	exon	127506272	127506341	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	exon	127507190	127507288	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	exon	127509124	127509213	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	exon	127511278	127511340	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	exon	127512394	127512418	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	exon	127513123	127514310	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr10	mm9\_refGene	stop\_codon	127513140	127513142	0.000000	+	.	gene\_id "NM\_019766"; transcript\_id "NM\_019766"; 

> chr17\_random	mm9\_refGene	exon	39677	41691	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	stop\_codon	40445	40447	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	42329	42443	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	43007	43202	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	44596	44705	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	45129	45290	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	45800	45966	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	47141	47207	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	47495	47548	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	47638	47718	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	start\_codon	47662	47664	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17\_random	mm9\_refGene	exon	48466	48574	0.000000	-	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8118865	8118973	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8119721	8119801	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	start\_codon	8119775	8119777	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8119891	8119944	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8120232	8120298	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8121473	8121639	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8122149	8122310	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8122734	8122843	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8124237	8124432	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8124996	8125110	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	exon	8125748	8127762	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr17	mm9\_refGene	stop\_codon	8126992	8126994	0.000000	+	.	gene\_id "NM\_145968"; transcript\_id "NM\_145968"; 

> chr3	mm9\_refGene	exon	138868857	138868971	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	start\_codon	138868863	138868865	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138875216	138875328	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138878222	138878350	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138881153	138881317	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138895162	138895274	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138906038	138906149	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138961369	138961476	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138969108	138969264	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138972046	138972206	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	138980356	138980445	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	139082669	139082828	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	139185822	139185940	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	139364589	139364737	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	stop\_codon	139364736	139364737	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	stop\_codon	139372137	139372137	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr3	mm9\_refGene	exon	139372137	139373263	0.000000	+	.	gene\_id "NM\_198659"; transcript\_id "NM\_198659"; 

> chr10	refGene	exon	79635689	79635919	.	+	.	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "1"; exon\_id "NM\_027207.1"; gene\_name "1600002K03Rik";

> chr10	refGene	start\_codon	79635711	79635713	.	+	0	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "1"; exon\_id "NM\_027207.1"; gene\_name "1600002K03Rik";

> chr10	refGene	exon	79636954	79637070	.	+	.	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "2"; exon\_id "NM\_027207.2"; gene\_name "1600002K03Rik";

> chr10	refGene	stop\_codon	79637069	79637070	.	+	0	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "1"; exon\_id "NM\_027207.1"; gene\_name "1600002K03Rik";

> chr10	refGene	stop\_codon	79637562	79637562	.	+	1	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "1"; exon\_id "NM\_027207.1"; gene\_name "1600002K03Rik";

> chr10	refGene	exon	79637562	79637864	.	+	.	gene\_id "1600002K03Rik"; transcript\_id "NM\_027207"; exon\_number "3"; exon\_id "NM\_027207.3"; gene\_name "1600002K03Rik";

> chr11	refGene	exon	110829347	110829409	.	+	.	gene\_id "Kcnj16"; transcript\_id "NM\_001252207"; exon\_number "1"; exon\_id "NM\_001252207.1"; gene\_name "Kcnj16";

> chr11	refGene	exon	110847744	110847824	.	+	.	gene\_id "Kcnj16"; transcript\_id "NM\_001252207"; exon\_number "2"; exon\_id "NM\_001252207.2"; gene\_name "Kcnj16";

> chr11	refGene	exon	110885723	110889281	.	+	.	gene\_id "Kcnj16"; transcript\_id "NM\_001252207"; exon\_number "3"; exon\_id "NM\_001252207.3"; gene\_name "Kcnj16";

> chr11	refGene	start\_codon	110885828	110885830	.	+	0	gene\_id "Kcnj16"; transcript\_id "NM\_001252207"; exon\_number "1"; exon\_id "NM\_001252207.1"; gene\_name "Kcnj16";

> chr11	refGene	stop\_codon	110887085	110887087	.	+	0	gene\_id "Kcnj16"; transcript\_id "NM\_001252207"; exon\_number "1"; exon\_id "NM\_001252207.1"; gene\_name "Kcnj16";

> chrY\_random	refGene	exon	4246223	4247319	.	-	.	gene\_id "LOC434960"; transcript\_id "NM\_001025241"; exon\_number "1"; exon\_id "NM\_001025241.1"; gene\_name "LOC434960";

> chrY\_random	refGene	stop\_codon	4246355	4246357	.	-	0	gene\_id "LOC434960"; transcript\_id "NM\_001025241"; exon\_number "1"; exon\_id "NM\_001025241.1"; gene\_name "LOC434960";

> chrY\_random	refGene	start\_codon	4247036	4247038	.	-	0	gene\_id "LOC434960"; transcript\_id "NM\_001025241"; exon\_number "1"; exon\_id "NM\_001025241.1"; gene\_name "LOC434960";

> chrY\_random	refGene	exon	4248546	4248568	.	-	.	gene\_id "LOC434960"; transcript\_id "NM\_001025241"; exon\_number "2"; exon\_id "NM\_001025241.2"; gene\_name "LOC434960";

> chrY\_random	refGene	exon	52515006	52515028	.	+	.	gene\_id "LOC434960"; transcript\_id "NM\_001025241\_3"; exon\_number "1"; exon\_id "NM\_001025241\_3.1"; gene\_name "LOC434960";

> chrY\_random	refGene	exon	52516257	52517353	.	+	.	gene\_id "LOC434960"; transcript\_id "NM\_001025241\_3"; exon\_number "2"; exon\_id "NM\_001025241\_3.2"; gene\_name "LOC434960";

> chrY\_random	refGene	start\_codon	52516538	52516540	.	+	0	gene\_id "LOC434960"; transcript\_id "NM\_001025241\_3"; exon\_number "1"; exon\_id "NM\_001025241\_3.1"; gene\_name "LOC434960";

> chrY\_random	refGene	stop\_codon	52517219	52517221	.	+	0	gene\_id "LOC434960"; transcript\_id "NM\_001025241\_3"; exon\_number "1"; exon\_id "NM\_001025241\_3.1"; gene\_name "LOC434960";

> chr10	refGene	exon	57857121	57857348	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "1"; exon\_id "NM\_001193303.1"; gene\_name "Lims1";

> chr10	refGene	start\_codon	57857167	57857169	.	+	0	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "1"; exon\_id "NM\_001193303.1"; gene\_name "Lims1";

> chr10	refGene	exon	57861769	57861928	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "2"; exon\_id "NM\_001193303.2"; gene\_name "Lims1";

> chr10	refGene	exon	57870818	57870884	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "3"; exon\_id "NM\_001193303.3"; gene\_name "Lims1";

> chr10	refGene	exon	57872308	57872428	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "4"; exon\_id "NM\_001193303.4"; gene\_name "Lims1";

> chr10	refGene	exon	57872801	57872950	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "5"; exon\_id "NM\_001193303.5"; gene\_name "Lims1";

> chr10	refGene	exon	57875151	57875301	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "6"; exon\_id "NM\_001193303.6"; gene\_name "Lims1";

> chr10	refGene	exon	57876721	57876813	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "7"; exon\_id "NM\_001193303.7"; gene\_name "Lims1";

> chr10	refGene	exon	57879382	57879430	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "8"; exon\_id "NM\_001193303.8"; gene\_name "Lims1";

> chr10	refGene	exon	57881147	57881222	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "9"; exon\_id "NM\_001193303.9"; gene\_name "Lims1";

> chr10	refGene	exon	57881395	57881534	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "10"; exon\_id "NM\_001193303.10"; gene\_name "Lims1";

> chr10	refGene	stop\_codon	57881534	57881534	.	+	0	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "1"; exon\_id "NM\_001193303.1"; gene\_name "Lims1";

> chr10	refGene	stop\_codon	57884202	57884203	.	+	2	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "1"; exon\_id "NM\_001193303.1"; gene\_name "Lims1";

> chr10	refGene	exon	57884202	57887439	.	+	.	gene\_id "Lims1"; transcript\_id "NM\_001193303"; exon\_number "11"; exon\_id "NM\_001193303.11"; gene\_name "Lims1";

> chr1	refGene	exon	20880703	20880767	.	+	.	gene\_id "Paqr8"; transcript\_id "NM\_028829"; exon\_number "1"; exon\_id "NM\_028829.1"; gene\_name "Paqr8";

> chr1	refGene	exon	20922141	20922320	.	+	.	gene\_id "Paqr8"; transcript\_id "NM\_028829"; exon\_number "2"; exon\_id "NM\_028829.2"; gene\_name "Paqr8";

> chr1	refGene	exon	20924663	20928837	.	+	.	gene\_id "Paqr8"; transcript\_id "NM\_028829"; exon\_number "3"; exon\_id "NM\_028829.3"; gene\_name "Paqr8";

> chr1	refGene	start\_codon	20924705	20924707	.	+	0	gene\_id "Paqr8"; transcript\_id "NM\_028829"; exon\_number "1"; exon\_id "NM\_028829.1"; gene\_name "Paqr8";

> chr1	refGene	stop\_codon	20925767	20925769	.	+	0	gene\_id "Paqr8"; transcript\_id "NM\_028829"; exon\_number "1"; exon\_id "NM\_028829.1"; gene\_name "Paqr8";

> chr1	refGene	exon	9535489	9537536	.	+	.	gene\_id "Rrs1"; transcript\_id "NM\_021511"; exon\_number "1"; exon\_id "NM\_021511.1"; gene\_name "Rrs1";

> chr1	refGene	start\_codon	9535605	9535607	.	+	0	gene\_id "Rrs1"; transcript\_id "NM\_021511"; exon\_number "1"; exon\_id "NM\_021511.1"; gene\_name "Rrs1";

> chr1	refGene	stop\_codon	9536700	9536702	.	+	0	gene\_id "Rrs1"; transcript\_id "NM\_021511"; exon\_number "1"; exon\_id "NM\_021511.1"; gene\_name "Rrs1";

> chr1	refGene	exon	157882857	157883050	.	+	.	gene\_id "Tor1aip2"; transcript\_id "NM\_001160180"; exon\_number "1"; exon\_id "NM\_001160180.1"; gene\_name "Tor1aip2";

> chr1	refGene	exon	157888205	157888264	.	+	.	gene\_id "Tor1aip2"; transcript\_id "NM\_001160180"; exon\_number "2"; exon\_id "NM\_001160180.2"; gene\_name "Tor1aip2";

> chr1	refGene	exon	157898424	157900866	.	+	.	gene\_id "Tor1aip2"; transcript\_id "NM\_001160180"; exon\_number "3"; exon\_id "NM\_001160180.3"; gene\_name "Tor1aip2";

> chr1	refGene	start\_codon	157899008	157899010	.	+	0	gene\_id "Tor1aip2"; transcript\_id "NM\_001160180"; exon\_number "1"; exon\_id "NM\_001160180.1"; gene\_name "Tor1aip2";

> chr1	refGene	stop\_codon	157899401	157899403	.	+	0	gene\_id "Tor1aip2"; transcript\_id "NM\_001160180"; exon\_number "1"; exon\_id "NM\_001160180.1"; gene\_name "Tor1aip2";

[1]: http://www.sanger.ac.uk/resources/software/gff/
[2]: http://tianxia-world.tk/2013/05/ucsc-usages/
[3]: https://github.com/Tong-Chen/NGS/blob/adbef1139db6427e8b9a7e7d569a37b9a57d2c71/parseGTF.py
[4]: https://github.com/Tong-Chen/NGS/blob/adbef1139db6427e8b9a7e7d569a37b9a57d2c71/sortGTF.py
