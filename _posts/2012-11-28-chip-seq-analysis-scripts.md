---
title: ChIP-Seq analysis scripts
author: 悟道
layout: post
permalink: /?p=2638
categories:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<pre class="brush: powershell; title: update 20130222-10:23; notranslate" title="update 20130222-10:23">include ~/home/server-project/makefile.tm

#---------header----------------------
#The value for allsample and sample usually is the filename without the suffix. 
#Here suffix is saved in variable &lt;type&gt;
#sample.type equals complete filename
#type is the file type. Available choice: fq fastq
allsample=samp1 samp2 samp3
sample=
type=
 
 #----NCBI SRA preprocess---other parameters may be needed----------------
$(sample).$(type):
	fastq-dump $(basename $@).sra
 
all_dump:
	a=($(allsample)); for i in "$${a[@]}"; do make $$i.$(type) sample=$$i & done
#------------------------------------------------------------------------------
#--------------------trim ENCODE data------------------------
#last: a number. The last nt you want to keep
last=
$(sample).trim:
	fastx_trimmer -l $(last) -f 1 -i $(sample).$(type) &gt;$(sample).trim.$(type)

all_trim:
	a=($(allsample)); for i in "$${a[@]}"; do make $$i.trim sample=$$i & done
	#make -j $(addsuffix .trim, $(allsample))
#------------------------------------------------------------------------------

#--------------------quality estimation----------------------
$(sample).fastqc:
	echo "Begin quality estimation $@---`date`" &gt;&gt;$(basename $@).log
	fastqc $(basename $@).$(type)
	echo "End quality estimation $@---`date`" &gt;&gt;$(basename $@).log
 
all_fastqc:
	a=($(allsample)); for i in "$${a[@]}"; do make $$i.fastqc sample=$$i & done
	@echo "All fastqc finished. `date`" 
#------------------------------------------------------------------------------

#-------begin mapping-----------------------------------------
#bwa_index represents index files used. This parameter is controlled by 
#bwa_index_v to faciliate set specise related index. Available choice: mm9 hg19
#way has two choice (uniq quality). uniq means select uniquely mapped reads.
#quality means select mapped reads with quality larger than 1.
bwa_index_v=
bwa_index=$($(bwa_index_v)Index)
way=
 
$(sample):
	echo "Begin --$@---`date`" &gt;&gt;$@.log
	echo "Begin mapping ---`date`" &gt;&gt;$@.log
	bwa aln -t 6 $(bwa_index) $@.$(type) &gt;$@.sai 2&gt;&gt;$@.log
	bwa samse $(bwa_index) $@.sai $@.$(type) &gt; $@.sam 2&gt;&gt;$@.log
	/bin/rm -f $@.sai
	echo "End mapping ---`date`" &gt;&gt;$@.log
ifeq ($(way), uniq)
	echo "Begin filter unmapped reads and sort---`date`" &gt;&gt;$@.log
	grep '^@' $@.sam &gt;$@.uniq.sam
	grep 'XT:A:U' $@.sam &gt;&gt;$@.uniq.sam
	echo "Total mapped reads:`samtools view -F4 -cS $@.sam`" &gt;$@.sta \
		&& /bin/rm -f $@.sam &
	samtools view -F 4 -bS $@.uniq.sam &gt;$@.uniq.map.bam
	samtools sort $@.uniq.map.bam $@.uniq.map.sort 2&gt;&gt;$@.log
	echo "End filter unmapped reads and sort---`date`" &gt;&gt;$@.log
	samtools rmdup -s $@.uniq.map.sort.bam \
		$@.uniq.map.sort.rmdup.bam 2&gt;&gt;$@.log
	echo "End removing PCR artifact---`date`" &gt;&gt;$@.log
	echo "Total redundant reads:`samtools view -c $@.uniq.map.sort.bam`" &gt;&gt;$@.sta
	/bin/rm -f $@.uniq.map.sort.bam &
	echo "Final reads:`samtools view -c $@.uniq.map.sort.rmdup.bam`" &gt;&gt;$@.sta &
	echo "End $@---`date`" &gt;&gt;$@.log
	#echo "Begin indexing---`date`" &gt;&gt;$@.log
	#samtools index $@.uniq.map.sort.rmdup.bam 2&gt;&gt;$@.log
	#echo "End indexing---`date`" &gt;&gt;$@.log
else
	echo "Begin selecting high quality reads---`date`" &gt;&gt;$@.log
	samtools view -F4 -q 1 -ubS $@.sam \
		| samtools sort - $@.map.q1.sort 2 &gt;&gt;$@.log
	echo "End selecting high quality reads---`date`" &gt;&gt;$@.log
	echo "Total mapped reads:`samtools view -F4 -cS $@.sam`" &gt;$@.sta \
		&& /bin/rm -f $@.sam &
	echo "Begin removing PCR artifacast---`date`" &gt;&gt;$@.log
	samtools rmdup -s $@.map.q1.sort.bam \
		$@.map.q1.sort.rmdup.bam 2&gt;&gt;$@.log
	echo "End removing PCR artifact---`date`" &gt;&gt;$@.log
	echo "Total redundant reads:`samtools view -c $@.map.q1.sort.bam`" &gt;&gt;$@.sta
	/bin/rm -f $@.map.q1.sort.bam &
	echo "Final reads:`samtools view -c $@.map.q1.sort.rmdup.bam`" &gt;&gt;$@.sta &
	echo "End $@---`date`" &gt;&gt;$@.log
	#echo "Begin indexing---`date`" &gt;&gt;$@.log
	#samtools index $@.map.q1.sort.rmdup.bam 2&gt;&gt;$@.log
	#echo "End indexing---`date`" &gt;&gt;$@.log
endif
	touch $@
	pythonmail2.py $@ $@
 
all_map: 
	a=($(allsample)); for i in "$${a[@]}"; do make $$i sample=$$i & done
	@echo "All mapping, filtering "
#--------------------end mapping------------------------------------------------ 

#-----------------peak calling and ceas annotation-------------------------------
wgEncodeSydhHistEse14H3k04me3StdRawDataRep1.mapreads=14192647
wgEncodeSydhHistEse14H3k04me3StdRawDataRep2.mapreads=21244147


#------------------------------------------------
#genomesize is used for macs. Available choice mm hs
#control represents if there is an input. The &lt;filename&gt; of input 
	#(without .&lt;type&gt; suffix) should be given
	#if you want to call peaks with control.
#peak_typeo is used to label sharp peaks and broad peaks. 
	#Available choice: TF,histone_s histone_b.
#normalize: normalize wig data using RPM. 
	#If 'TRUE' is given, RPM wig will be computed.
#igv: transfer wig to tdf for visularization in IGV if a value 'igv' is given.
	#When value 'igv' is given, normalize will be TRUE automately.
#ceas:	execute peak annotation if value 'ceas' is given
	#When value 'ceas' is given, normalize will be TRUE automately.
#ceas_ref_v is used for ease annotation. Available choice: mm9 hg19
genomesize=
control=
peak_type=
macs_para=
ifeq ($(peak_type), TF)
macs_para=--call-subpeaks 
endif
ifeq ($(peak_type), histone_s)
macs_para=--call-subpeaks 
endif
ifeq ($(peak_type), histone_b)
macs_para=--pvalue 1e-3 --call-subpeaks --nomodel --shiftsize 
endif
normalize=
igv=
ifeq ($(igv),igv)
normalize=TRUE
endif
ifeq ($(way), uniq)
bam_suffix=.uniq.map.sort.rmdup.bam
else
bam_suffix=.map.q1.sort.rmdup.bam
endif
ceas=
ifeq ($(ceas),ceas)
normalize=TRUE
endif

ceas_ref_v=
ceas_ref=$($(ceas_ref_v)_refGene)

$(sample).$(control).macs:
	touch $@
	echo "macs `date`" &gt;&gt;$(basename $@).log
ifdef control
	macs14 -t $(addsuffix $(bam_suffix), $(sample)) \
		-c $(addsuffix $(bam_suffix), $(control)) \
		--name=$@ --format=BAM --wig -S -g $(genomesize) $(macs_para)  \
		&gt;&gt;$(basename $@).log 2&gt;&1
else
	macs14 -t $(addsuffix $(bam_suffix),  $(sample)) \
		--name=$@ --format=BAM --wig -S -g $(genomesize) $(macs_para)  \
		&gt;&gt;$(basename $@).log 2&gt;&1
endif
	echo "macs `date`" &gt;&gt;$(basename $@).log
ifeq ($(normalize),TRUE)
	-gunzip -f $@_MACS_wiggle/treat/$@_treat_afterfiting_all.wig.gz
	awk 'BEGIN{FS="\t" }{if($$2!="") $$2=1000000*$$2/$($(addsuffix .mapreads,  $(sample))); print $$0 }' $@_MACS_wiggle/treat/$@_treat_afterfiting_all.wig &gt; $@_MACS_wiggle/treat/$@_treat_afterfiting_all.wig.norm
	/bin/mv -f $@_MACS_wiggle/treat/$@_treat_afterfiting_all.wig.norm \
		$@_MACS_wiggle/treat/$@_treat_afterfiting_all.wig
endif
ifeq ($(igv),igv)
	echo "Transfer wig to igv tdf begins at `date`" &gt;&gt;$(basename $@).log
	igvtools tile $@_MACS_wiggle/treat/$@_treat_afterfiting_all.wig $@_MACS_wiggle/treat/$@_treat_afterfiting_all.tdf mm9 &gt;&gt;$(basename $@).log 2&gt;&1 &
	echo "Transfer wig to igv tdf ends at `date`" &gt;&gt;$(basename $@).log
endif
ifeq ($(ceas),ceas)
	echo "begin ceas `date`" &gt;&gt;$(basename $@).log
	ceas -g $(ceas_ref) -b $@_peaks.bed -w $@_MACS_wiggle/treat/$@_treat_afterfiting_all.wig --name=$@ &gt;&gt;$(basename $@).log 2&gt;&1
	echo "end ceas `date`" &gt;&gt;$(basename $@).log
endif
	pythonmail2.py $@ $@
 
all_macs:
	a=($(allsample)); for i in "$${a[@]}"; do make $$i.$(control).macs sample=$$i & done
#--------------------------------------------------------------------

#--------------------one key to solve all---------------
onekey:
	make $(sample)
ifdef control
	make $(control) sample=$(control)
endif
	make $(sample).$(control).macs

all_onekey:
	make all_sample
ifdef control
	make $(control) sample=$(control)
endif
	make all_macs

#--------------------one key to solve all---------------

#--------------------------------------------------------------------

</pre>