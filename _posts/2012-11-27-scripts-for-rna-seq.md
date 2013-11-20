---
title: Scripts for RNA-Seq
author: 悟道
layout: post
permalink: /?p=2633
categories:
  - seq
tags:
  - RNA-Seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
Makefile scripts for RNA-Seq

<pre class="brush: powershell; title: ; notranslate" title="">include ~/home/server-project/makefile.tm

rawn=TP16_1.fq \
TP16_2.fq \
TP22_1.fq \
TP22_2.fq \
TP23_1.fq \
TP23_2.fq
raws=$(addsuffix .fastq,  $(rawn))
fastqc=$(addsuffix .fastqc, $(rawn))
trans=/home/chentong/home/project/project5/ucsc/mm9.gene.refgene.gtf
transIndex=/home/chentong/home/server-project/trans_index/mm9/
mm9=~/home/server-project/bowtie2_index/mm9/mm9.fa

$(fastqc):
	fastqc $(basename $@).fastq &gt;$(basename $@).log 2&gt;&1

line=TP16


$(line).tophat.test:
	mkdir $(line).test
	tophat -r 0 --mate-std-dev 500 -o $(line).test/topout \
		-p 8 \
		--library-type fr-secondstrand \
		$(bowtie2mm9) $(line)_1.fq $(line)_2.fq &gt;$(line).test.log 2&gt;&1
	java -Xmx2g -jar /home/chentong/home/soft/picard-tools-1.74/CollectInsertSizeMetrics.jar \
		INPUT=$(line).test/topout/accepted_hits.bam OUTPUT=$(line).test/topout/insertSize.out \
		HISTOGRAM_FILE=$(line).test/topout/insertSize.hist
	pythonmail2.py $@ $@



libtype=fr-secondstrand

$(line).tophat_corrected:
	tophat -r 130 --mate-std-dev 30 -o $(line)/topout \
		--solexa-quals -p 8 \
		-G $(trans) --transcriptome-index $(transIndex) \
		--library-type $(libtype) \
		$(bowtie2mm9) $(line)_1.fq $(line)_2.fq &gt;$(line).log 2&gt;&1
	samtools flagstat $(line)/topout/accepted_hits.bam &gt;$(line)/$(line).sta &
	echo `samtools view $(line)/topout/accepted_hits.bam | greo 'NH:i:1' | cut -f 1 | sort -u | wc -l` &gt;$(line)/topout/uniq_mapped.reads &
	echo `samtools view $(line)/topout/accepted_hits.bam |  cut -f 1 | sort -u | wc -l` &gt;$(line)/topout/mapped.reads &
	samtools view $(line)/topout/accepted_hits.bam | awk 'BEGIN{OFS="\t";FS="\t"}{for(i=12;i&lt;=NF;i++) if($$i~/^XS:A:/) print $$2,$$i}' | sort | uniq -c &gt;$(line)/topout/accepted_hits.bam.flag_xs &
	correctTophatOutput.sh -f $(line)/topout/accepted_hits.bam -t bam -l $(libtype) -e $(line)/topout/accepted.hits.wrongFlag.sam
	pythonmail2.py $@ $@

$(line).cufflinks.corrected:
	cufflinks -p 8 --GTF-guide $(trans) --label $(line) \
		-o $(line)/cufout_corrected $(line)/topout/accepted_hits.corrected.bam \
		--library-type $(libtype) &gt;$(line).log 2&gt;&1
	pythonmail2.py $@ $@

cuffmerge_corrected: 
	cuffmerge -o TP16_TP22_TP23.corrected.cuffmerge -g $(trans) -s $(bowtie2mm9).fa -p 8 assemblies.corrected.txt 
	pythonmail2.py $@ $@

cuffdiff_corrected:
	cuffdiff -o TP16-22-23-corrected.cuffdiff -b $(mm9) -p 8 -L TP16,TP22,TP23 -u \
		--library-type $(libtype) \
		TP16_TP22_TP23.corrected.cuffmerge/merged.gtf \
		TP16/topout/accepted_hits.corrected.bam \
		TP22/topout/accepted_hits.corrected.bam \
		TP23/topout/accepted_hits.corrected.bam
	pythonmail2.py $@ $@

all:
	/bin/rm -rf $(line)
	/bin/mkdir $(line)
	make $(line).tophat
	make $(line).cufflinks

</pre>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;  
Assisted scripts  
correctTophatOutput.sh  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

<pre class="brush: bash; title: ; notranslate" title="">#!/bin/bash


usage()
{
cat &lt;&lt;EOF
${txtcyn}
Usage:

$0 options${txtrst}

${bldblu}Function${txtrst}:

This script is used to correct wrong tags from Tophat output.

${txtbld}OPTIONS${txtrst}:
	-f	Data file (Tophat outputted bam or file)
 		${bldred}[NECESSARY]${txtrst}
	-t	File type of input.
 		${bldred}[bam or sam]${txtrst}
	-l	library-type[${bldred}Default fr-secondstrand, acceppt
		fr-firststrand${txtrst}]
	-e	Output reads with wrong mapped flags[${bldred}Default FALSE,
		accept a string to be the name of outputed file${txtrst}]
EOF
}

file=
ltype="fr-secondstrand"
error='FALSE'
itype=''

while getopts "hf:t:l:e:" OPTION
do
	case $OPTION in
		h)
			usage
			exit 1
			;;
		f)
			file=$OPTARG
			;;
		t)
			itype=$OPTARG
			;;
		l)
			ltype=$OPTARG
			;;
		e)
			error=$OPTARG
			;;
		?)
			usage
			exit 1
			;;
	esac
done
if [ -z $file ]; then
	usage
	exit 1
fi

cat &lt;&lt;EOF &gt;correctTophatOutput.awk
#!/bin/awk -f

BEGIN{
	OFS="\t";FS="\t";libtype="${ltype}";
	save_discrepancy_to_file="${error}";
	if(save_discrepancy_to_file!="FALSE") system("[ -e " save_discrepancy_to_file " ] && rm " save_discrepancy_to_file);
}
{
    if(\$1 ~ /^@/) print;
    else
    {
        for(i=1;i&lt;=NF;i++) if(\$i!~/^XS/) printf("%s\t",\$i); else XS0=\$i;
        XS1=XS0;
        if(\$2~/^0x/ || \$2~/^[0-9]+\$/){   # FLAG in HEX or Decimal format
            if(libtype=="fr-firststrand") XS1=((and(\$2, 0x10) && and(\$2, 0x40)) || (and(\$2,0x80) && !and(\$2,0x10)))?"XS:A:+":"XS:A:-";
            if(libtype=="fr-secondstrand") XS1=((and(\$2, 0x10) && and(\$2, 0x80)) || (and(\$2,0x40) && !and(\$2,0x10)))?"XS:A:+":"XS:A:-";
        }
        else if(\$2~/^[:alpha:]/){   # FLAG in string
            if(libtype=="fr-firststrand") XS1=(\$2~/r.*1/ || (\$2~/2/ && \$2!~/r/))?"XS:A:+":"XS:A:-";
            if(libtype=="fr-secondstrand") XS1=(\$2~/r.*2/|| (\$2~/1/ && \$2!~/r/))?"XS:A:+":"XS:A:-";
        }
        print XS1;

        if(save_discrepancy_to_file!="FALSE" && XS1!=XS0) print &gt;&gt; save_discrepancy_to_file;
    }
}

EOF

if test $itype == "sam"; then
	output=${file/sam/corrected.sam}
	cat $file | awk -f correctTophatOutput.awk &gt;$output 
else
	output_p=${file/bam/corrected.bam}
	samtools view -h ${file} | awk -f correctTophatOutput.awk \
	| samtools view -Sb - -o ${output_p}
fi



</pre>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;