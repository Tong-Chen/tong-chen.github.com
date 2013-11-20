---
title: bar plot (An useful guide for ggplot2)
author: 悟道
layout: post
permalink: /?p=2707
categories:
  - R
tags:
  - ggplot2
  - pic
  - R
---
 
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

<div class="wp_codebox">
  <table>
    <tr id="p2707171">
      <td class="code" id="p2707code171">
        <pre class="bash" style="font-family:monospace;">&nbsp;
<span style="color: #666666; font-style: italic;">#!/bin/bash</span>
&nbsp;
<span style="color: #666666; font-style: italic;">#set -x</span>
&nbsp;
usage<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#123;</span>
<span style="color: #c20cb9; font-weight: bold;">cat</span> <span style="color: #cc0000; font-style: italic;">&lt;&lt;EOF
${txtcyn}
Usage:
&nbsp;
$0 options${txtrst}
&nbsp;
${bldblu}Function${txtrst}:
&nbsp;
This script is used to do boxplot using ggplot2.
&nbsp;
fileformat for -f (suitable for data extracted from one sample)
&nbsp;
Gene	hmC	expr	Set
NM_001003918_26622	0	83.1269257376101	1
NM_001011535_3260	0	0	1
NM_001012640_14264	0	0	1
NM_001012640_30427	0	0	1
NM_001003918_266221	0	0	1
NM_001017393_30504	0	0	1
NM_001025241_30464	0	0	1
NM_001017393_30504	0	0	1
&nbsp;
fileformat when -m is true
#The name "value" and "variable" shoud not be altered.
#"Set" needs to be the parameter after -a.
#Actually this format is the melted result of last format.
value	variable	Set
0	var	1
1	vhig	2
&nbsp;
${txtbld}OPTIONS${txtrst}:
	-f	Data file (with header line, the first column is the
 		colname, tab seperated)${bldred}[NECESSARY]${txtrst}
	-m	When true, it will skip preprocess. But the format must be
		the same as listed before.
		${bldred}[Default FALSE, accept TRUE]${txtrst}
	-a	Name for x-axis variable
		[${txtred}Necessary, for example 'Gene' which represents 
	   	name of each gene Set${txtrst}]
	-b	Order of xvariable (parameter for -a). 	
		[${txtred}Optional, format: 'chr1','chr2','chr3',...${txtrst}]
		["'chr1','chr2','chr3','chr4','chr5','chr6','chr7','chr8',
		'chr9','chr10','chr11','chr12','chr13','chr14','chr15',
		'chr16','chr17','chr18','chr19','chrX','chrY','chrM'"]
	-l	Order for legend.
		[${txtred}Optional, format: 'Expected','5hmC',...${txtrst}]
	-n	Rotation angle for x-axis.  
		[${txtred}Optional, Default oriental. Accept an integer
		like 45,90 (count anti-clockwise). ${txtrst}]
	-g	Variable name for facet.
		[${txtred}Optional, like 'sample' or 'grp' ${txtrst}]
	-j	Number of columns in one row.	
		[${txtred}Necessary if -g is given ${txtrst}]
	-k	Paramter for scales for facet.
		[${txtred}Optional, only used when -g is given. Default each 
	    inner graph use same scale [x,y range]. 'free','free_x','free_y' 
	    is accepted. ${txtrst}]
	-o	Order of facet.
		[${txtred}Optional, format:
		'F1_6-1','R1','F1_MEF','1422','2737','17-3-15','15-4-6','513','233'${txtrst}]
	-p	Other columns that needs to be ignored.
		[Optional, format (begins with ,) ',col_name1,colname2...']
	-t	Title of picture[${txtred}Default empty title${txtrst}]
	-x	xlab of picture[${txtred}Default empty xlab${txtrst}]
	-y	ylab of picture[${txtred}Default empty ylab${txtrst}]
	-s	Scale y axis
		[${txtred}Default null. Accept TRUE.${txtrst}]
	-v	If scale is TRUE, give the following
		scale_y_log10(), coord_trans(y="log10"), or other legal
		#command for ggplot2)${txtrst}]
	-w	The width of output picture.[${txtred}Default 800${txtrst}]
	-u	The height of output picture.[${txtred}Default 800${txtrst}] 
	-r	The resolution of output picture.[${txtred}Default NA${txtrst}]
	-z	Is there a header[${bldred}Default TRUE${txtrst}]
	-e	Execute or not[${bldred}Default TRUE${txtrst}]
	-i	Install depeneded packages[${bldred}Default FALSE${txtrst}]
EOF</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #007800;">file</span>=
<span style="color: #007800;">title</span>=<span style="color: #ff0000;">''</span>
<span style="color: #007800;">melted</span>=<span style="color: #ff0000;">'FALSE'</span>
<span style="color: #007800;">xlab</span>=<span style="color: #ff0000;">'NULL'</span>
<span style="color: #007800;">ylab</span>=<span style="color: #ff0000;">'NULL'</span>
<span style="color: #007800;">xvariable</span>=<span style="color: #ff0000;">''</span>
<span style="color: #007800;">xvar_order</span>=<span style="color: #ff0000;">''</span>
<span style="color: #007800;">legend_order</span>=<span style="color: #ff0000;">''</span>
<span style="color: #007800;">angle</span>=<span style="color: #000000;"></span>
<span style="color: #007800;">facet</span>=<span style="color: #ff0000;">'haha'</span>
<span style="color: #007800;">facet_ncol</span>=<span style="color: #000000;">1</span>
<span style="color: #007800;">facet_order</span>=<span style="color: #ff0000;">''</span>
<span style="color: #007800;">col_exclu</span>=<span style="color: #ff0000;">''</span>
<span style="color: #007800;">scales</span>=<span style="color: #ff0000;">'fixed'</span>
<span style="color: #007800;">scaleY</span>=<span style="color: #ff0000;">'FALSE'</span>
<span style="color: #007800;">scaleY_x</span>=<span style="color: #ff0000;">'FALSE'</span>
<span style="color: #007800;">header</span>=<span style="color: #ff0000;">'TRUE'</span>
<span style="color: #007800;">execute</span>=<span style="color: #ff0000;">'TRUE'</span>
<span style="color: #007800;">ist</span>=<span style="color: #ff0000;">'FALSE'</span>
<span style="color: #007800;">uwid</span>=<span style="color: #000000;">800</span>
<span style="color: #007800;">vhig</span>=<span style="color: #000000;">800</span>
<span style="color: #007800;">res</span>=<span style="color: #ff0000;">'NA'</span>
&nbsp;
&nbsp;
&nbsp;
<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #7a0874; font-weight: bold;">getopts</span> <span style="color: #ff0000;">"hf:m:a:b:l:o:n:g:j:k:p:t:x:y:w:u:r:s:z:v:e:i:"</span> OPTION
<span style="color: #000000; font-weight: bold;">do</span>
	<span style="color: #000000; font-weight: bold;">case</span> <span style="color: #007800;">$OPTION</span> <span style="color: #000000; font-weight: bold;">in</span>
		h<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			usage
			<span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		f<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">file</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		m<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">melted</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		a<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">xvariable</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		b<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">xvar_order</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		l<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">legend_order</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		o<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">facet_order</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		n<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">angle</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		g<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">facet</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		j<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">facet_ncol</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		k<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">scales</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		p<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">col_exclu</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		t<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">title</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		x<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">xlab</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		y<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">ylab</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		<span style="color: #c20cb9; font-weight: bold;">w</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">uwid</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		u<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">vhig</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		r<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">res</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		s<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">scaleY</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		v<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">scaleY_x</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		z<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">header</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		e<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">execute</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		i<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			<span style="color: #007800;">ist</span>=<span style="color: #007800;">$OPTARG</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
		?<span style="color: #7a0874; font-weight: bold;">&#41;</span>
			usage
			<span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span>
			<span style="color: #000000; font-weight: bold;">;;</span>
	<span style="color: #000000; font-weight: bold;">esac</span>
<span style="color: #000000; font-weight: bold;">done</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #660033;">-z</span> <span style="color: #007800;">$file</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
	usage
	<span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span>
<span style="color: #000000; font-weight: bold;">fi</span>
&nbsp;
<span style="color: #c20cb9; font-weight: bold;">cat</span> <span style="color: #000000; font-weight: bold;">&lt;&lt;</span>END <span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #800000;">${file}</span>.r
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">$ist</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#123;</span>
	install.packages<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"ggplot2"</span>, <span style="color: #007800;">repo</span>=<span style="color: #ff0000;">"http://cran.us.r-project.org"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
	install.packages<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"reshape2"</span>, <span style="color: #007800;">repo</span>=<span style="color: #ff0000;">"http://cran.us.r-project.org"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
library<span style="color: #7a0874; font-weight: bold;">&#40;</span>ggplot2<span style="color: #7a0874; font-weight: bold;">&#41;</span>
library<span style="color: #7a0874; font-weight: bold;">&#40;</span>reshape2<span style="color: #7a0874; font-weight: bold;">&#41;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span><span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #000000; font-weight: bold;">!</span> <span style="color: #007800;">$melted</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#123;</span>
&nbsp;
	data <span style="color: #000000; font-weight: bold;">&lt;</span>- read.table<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">file</span>=<span style="color: #ff0000;">"<span style="color: #007800;">${file}</span>"</span>, <span style="color: #007800;">sep</span>=<span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\t</span>"</span>, <span style="color: #007800;">header</span>=<span style="color: #007800;">$header</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">${facet}</span>"</span> <span style="color: #000000; font-weight: bold;">!</span>= <span style="color: #ff0000;">"haha"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#123;</span>
		id_vars = c<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">${xvariable}</span>"</span>, <span style="color: #ff0000;">"<span style="color: #007800;">${facet}</span>"</span> <span style="color: #800000;">${col_exclu}</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
		<span style="color: #666666; font-style: italic;">#data_m &lt;- melt(data, id.vars=c("${xvariable}", "${facet}"))</span>
	<span style="color: #7a0874; font-weight: bold;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>
		id_vars = c<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">${xvariable}</span>"</span> <span style="color: #800000;">${col_exclu}</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
		<span style="color: #666666; font-style: italic;">#data_m &lt;- melt(data, id.vars=c("${xvariable}"))</span>
	<span style="color: #7a0874; font-weight: bold;">&#125;</span>
	data_m <span style="color: #000000; font-weight: bold;">&lt;</span>- melt<span style="color: #7a0874; font-weight: bold;">&#40;</span>data, id.vars=id_vars<span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>
	data_m <span style="color: #000000; font-weight: bold;">&lt;</span>- read.table<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">file</span>=<span style="color: #ff0000;">"<span style="color: #007800;">$file</span>"</span>, <span style="color: #007800;">sep</span>=<span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\t</span>"</span>,
	<span style="color: #007800;">header</span>=<span style="color: #007800;">$header</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">${legend_order}</span>"</span> <span style="color: #000000; font-weight: bold;">!</span>= <span style="color: #ff0000;">""</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#123;</span>
	data_m\<span style="color: #007800;">$variable</span> <span style="color: #000000; font-weight: bold;">&lt;</span>- factor<span style="color: #7a0874; font-weight: bold;">&#40;</span>data_m\<span style="color: #007800;">$variable</span>,
	<span style="color: #007800;">levels</span>=c<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #800000;">${legend_order}</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">${xvar_order}</span>"</span> <span style="color: #000000; font-weight: bold;">!</span>= <span style="color: #ff0000;">""</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#123;</span>
	data_m\$<span style="color: #800000;">${xvariable}</span> <span style="color: #000000; font-weight: bold;">&lt;</span>- factor<span style="color: #7a0874; font-weight: bold;">&#40;</span>data_m\$<span style="color: #800000;">${xvariable}</span>,
	<span style="color: #007800;">levels</span>=c<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #800000;">${xvar_order}</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">${facet_order}</span>"</span> <span style="color: #000000; font-weight: bold;">!</span>= <span style="color: #ff0000;">""</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#123;</span>
	data_m\$<span style="color: #800000;">${facet}</span> <span style="color: #000000; font-weight: bold;">&lt;</span>- factor<span style="color: #7a0874; font-weight: bold;">&#40;</span>data_m\$<span style="color: #800000;">${facet}</span>,
	<span style="color: #007800;">levels</span>=c<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #800000;">${facet_order}</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
p <span style="color: #000000; font-weight: bold;">&lt;</span>- ggplot<span style="color: #7a0874; font-weight: bold;">&#40;</span>data_m, aes<span style="color: #7a0874; font-weight: bold;">&#40;</span>factor<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">$xvariable</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>, value<span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> + xlab<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">$xlab</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> +
ylab<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">$ylab</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
&nbsp;
p <span style="color: #000000; font-weight: bold;">&lt;</span>- p + geom_bar<span style="color: #7a0874; font-weight: bold;">&#40;</span>aes<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">fill</span>=factor<span style="color: #7a0874; font-weight: bold;">&#40;</span>variable<span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>, <span style="color: #007800;">stat</span>=<span style="color: #ff0000;">"identity"</span>,
<span style="color: #007800;">position</span>=<span style="color: #ff0000;">"dodge"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> + theme_bw<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">$angle</span> <span style="color: #000000; font-weight: bold;">!</span>= <span style="color: #000000;"></span><span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>
	p <span style="color: #000000; font-weight: bold;">&lt;</span>- p + theme<span style="color: #7a0874; font-weight: bold;">&#40;</span>axis.text.x=element_text<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">angle</span>=<span style="color: #800000;">${angle}</span>,<span style="color: #007800;">hjust</span>=<span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">$facet</span>"</span> <span style="color: #000000; font-weight: bold;">!</span>= <span style="color: #ff0000;">"haha"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#123;</span>
	p <span style="color: #000000; font-weight: bold;">&lt;</span>- p + facet_wrap<span style="color: #7a0874; font-weight: bold;">&#40;</span>~<span style="color: #800000;">${facet}</span>, <span style="color: #007800;">ncol</span>=<span style="color: #800000;">${facet_ncol}</span>,
	<span style="color: #007800;">scales</span>=<span style="color: #ff0000;">"<span style="color: #007800;">${scales}</span>"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
&nbsp;
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span><span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #ff0000;">"<span style="color: #007800;">$scaleY</span>"</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#123;</span>
	p <span style="color: #000000; font-weight: bold;">&lt;</span>- p + <span style="color: #007800;">$scaleY_x</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
&nbsp;
png<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">filename</span>=<span style="color: #ff0000;">"<span style="color: #007800;">${file}</span>.png"</span>, <span style="color: #007800;">width</span>=<span style="color: #007800;">$uwid</span>, <span style="color: #007800;">height</span>=<span style="color: #007800;">$vhig</span>,
<span style="color: #007800;">res</span>=<span style="color: #007800;">$res</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
p
dev.off<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
END
&nbsp;
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #ff0000;">"<span style="color: #007800;">$execute</span>"</span> == <span style="color: #ff0000;">"TRUE"</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
	Rscript <span style="color: #800000;">${file}</span>.r
<span style="color: #000000; font-weight: bold;">fi</span></pre>
      </td>
    </tr>
  </table>
</div>

#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-