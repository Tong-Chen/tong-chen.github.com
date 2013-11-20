---
title: heatmapS.sh
author: 悟道
layout: post
permalink: /?p=2653
categories:
  - bash
  - R
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<pre class="brush: bash; title: heatmapS.sh; notranslate" title="heatmapS.sh">#!/bin/bash

#set -x

usage()
{
cat &lt;&lt;EOF
${txtcyn}
Usage:

$0 options${txtrst}

${bldblu}Function${txtrst}:

This script is used to do multiple heatmap horizontally for
comparing among samples using package ggplo2 and reshape2.
Also it can deal with kmeans cluster before heatmap.

The parameters for logical variable are either TRUE or FALSE.

${txtbld}OPTIONS${txtrst}:
	-f	Data file (with header line, the first column is the
 		colname, tab seperated)${bldred}[NECESSARY]${txtrst}
	-t	Title of picture[${txtred}Default empty title${txtrst}]
		[Scatter plot of horizontal and vertical variable]
	-a	Display xtics. ${bldred}[Default TRUE]${txtrst}
	-A	Rotation angle for x-axis value(anti clockwise)
		${bldred}[Default 0]${txtrst}
	-l	The position of legend. [${bldred}
		Default right. Accept top,bottom,left.${txtrst}]
	-b	Display ytics. ${bldred}[Default FALSE]${txtrst}
	-u	The width of output picture.[${txtred}Default 2000${txtrst}]
	-v	The height of output picture.[${txtred}Default 2000${txtrst}] 
	-r	The resolution of output picture.[${txtred}Default NA${txtrst}]
	-x	The color for representing low value.[${txtred}Default dark
		green${txtrst}]
	-y	The color for representing high value.[${txtred}Default
		dark red${txtrst}]
	-M	The color representing mid-value.[${txtred}Default 
		yellow${txtrst}]
	-Z	Use mid-value or not. [${txtred}Default FALSE, which means
		do not use mid-value. ${txtrst}]
	-k	Would you like cluster.[${txtred}Default 1 which means no
		cluster, other positive interger is accepted for executing
		kmeans cluster, also the parameter represents the number of
		expected clusters.${txtrst}]
	-c	The cluster methods you want to use.[${bldred}kmeans, for
		distance cluster,
		accept clara for trend cluster.${txtrst}]
	-d	Scale the data or not for clustering.[Default no scale. Accept TRUE, scale by
		row]
	-n	Include cluster info.[Default TRUE, accept FALSE]
	-p	Delete rows all zero.[Default FALSE, accept TRUE]
	-z	Presort data by covariance coefficient.
		[Default FALSE, accept TRUE]
	-s	The smallest value you want to keep, any number smaller will
		be taken as 0.[${bldred}Default -Inf, Optional${txtrst}]  
	-m	The maximum value you want to keep, any number larger willl
		be taken as the given maximum value.
		[${bldred}Default Inf, Optional${txtrst}] 
	-q	The smallest screen and file output.[Default TRUE] 
		Accept FALSE, to output each operation and data files.
	-j	Scale data for picture.[Default FALSE, accept TRUE]
	-J	When -j is TRUE,  supply a value to add to all values in data
		to avoid zero. [${bldred}Default 1${txtrst}]
	-o	Log transfer ot not.[${bldred}Default no log transfer,
		accept log or log2 ${txtrst}]
	-g	Cluster by which group.[${bldred}Default by all group${txtrst}]
	-G	Use quantile for color distribution. Default 5 color scale
		for each quantile.[Default FALSE, accept TRUE. Suitable for data range
		vary large.]
	-C	Color list for plot when -G is TRUE.
		[${bldred}Default 'green','yellow','dark red'.
		Accept a list of colors each wrapped by '' and totally wrapped
		by "" ${txtrst}]
	-O	When -G is TRUE, using given data points as separtor to
		assign colors. [${bldred}Default -G default]
	-e	Execute or not[${bldred}Default TRUE${txtrst}]
	-i	Install the required packages[${bldred}Default FALSE${txtrst}]
EOF
}

file=''
title=''
width=''
label=''
kclu=1
clu='kmeans'
scale='FALSE'
clusterInclu='TRUE'
group=0
execute='TRUE'
ist='FALSE'
legend='FALSE'
legend_pos='right'
small="-Inf"
maximum="Inf"
log=''
uwid=2000
vhig=2000
res='NA'
scale_op='FALSE'
scale_add=1
xcol='dark green'
ycol='dark red'
mcol='yellow'
mid_value_use='FALSE'
xtics='TRUE'
xtics_angle=0
ytics='FALSE'
quiet='TRUE'
delZero='FALSE'
cvSort='FALSE'
gradient='FALSE'
givenSepartor=''
gradientC="'green','yellow','red'"

while getopts "hf:t:u:v:x:y:M::r:w:l:a:A:b:k:c:d:n:g:s:j:J:m:o:G:C:O:q:e:i:p:Z:z:" OPTION
do
	case $OPTION in
		h)
			echo "Help mesage"
			usage
			exit 1
			;;
		f)
			file=$OPTARG
			;;
		t)
			title=$OPTARG
			;;
		u)
			uwid=$OPTARG
			;;
		v)
			vhig=$OPTARG
			;;
		x)
			xcol=$OPTARG
			;;
		y)
			ycol=$OPTARG
			;;
		M)
			mcol=$OPTARG
			;;
		Z)
			mid_value_use=$OPTARG
			;;
		r)
			res=$OPTARG
			;;
		w)
			width=$OPTARG
			;;
		l)
			legend_pos=$OPTARG
			;;
		a)
			xtics=$OPTARG
			;;
		A)
			xtics_angle=$OPTARG
			;;
		b)
			ytics=$OPTARG
			;;
		k)
			kclu=$OPTARG
			;;
		c)
			clu=$OPTARG
			;;
		d)
			scale=$OPTARG
			;;
		n)
			clusterInclu=$OPTARG
			;;
		g)
			group=$OPTARG
			;;
		p)
			delZero=$OPTARG
			;;
		z)
			cvSort=$OPTARG
			;;
		s)
			small=$OPTARG
			;;
		m)
			maximum=$OPTARG
			;;
		j)
			scale_op=$OPTARG
			;;
		J)
			scale_add=$OPTARG
			;;
		o)
			log=$OPTARG
			;;
		G)
			gradient=$OPTARG
			;;
		C)
			gradientC=$OPTARG
			;;
		O)
			givenSepartor=$OPTARG
			;;
		q)
			quiet=$OPTARG
			;;
		e)
			execute=$OPTARG
			;;
		i)
			ist=$OPTARG
			;;
		?)
			usage
			echo "Unknown parameters"
			exit 1
			;;
	esac
done

midname=".heatmapS"

if [ -z $file ] ; then
	echo 1&gt;&2 "Please give filename."
	usage
	exit 1
fi

if test $kclu -gt 1; then
	midname=${midname}".${clu}.$kclu.$group"
fi

if test "$log" != ''; then
	midname=${midname}".$log"
fi

if test "${scale}" == "TRUE"; then
	midname=${midname}".scale"
fi

cat &lt;&lt;END &gt;${file}${midname}.r

if ($ist){
	install.packages("ggplot2", repo="http://cran.us.r-project.org")
	install.packages("reshape2", repo="http://cran.us.r-project.org")
	if ($kclu &gt; 1){
		install.packages("cluster", repo="http://cran.us.r-project.org")
	}
}
library(ggplot2)
library(reshape2)
if($gradient){
	library(RColorBrewer)
}
if ($kclu &gt; 1){
	library(cluster)
}
if (! $quiet){
	print("Read in data set.")
}
data &lt;- read.table(file="$file", sep="\t", header=T, row.names=1,
	check.names=F)

#print("Read in label.")
#label is for group level
#label &lt;- as.vector(read.table(file="$label", sep="\t", header=F)\$V1)
#dimD &lt;- dim(data)
##size &lt;- dimD[1] * $width
#size &lt;- dimD[1] * ($width+1)
#print("Prepare group")
#grp &lt;- rep(label, each=size)
#print("Rename each column to make each one uniqu")
#names(data) &lt;- paste0(rep(label, each=$width), names(data))

if ($kclu&gt;1){

	if (! $quiet){
		print("Delete rows containing 0 only.")
	}
	data.zero &lt;- data[rowSums(data)==0,]
	rowZero &lt;- nrow(data.zero)
	data &lt;- data[rowSums(data)!=0,]

	if (! $quiet){
		print("Prepare data for clustering.")
	}
	if ($small != "-Inf"){
		mindata &lt;- $small
	}else{
		mindata &lt;- min(data)
	}
	if ($maximum != "Inf"){
		maxdata &lt;- $maximum
	}else{
		maxdata &lt;- max(data)
	}
	step &lt;- (maxdata-mindata)/$kclu
	if ($cvSort){
		if (! $quiet){
			print("Sort data by coefficient variance.")
		}
		sd &lt;- apply(data, 1, sd) #1 means row, 2 means col
		mean &lt;- rowMeans(data)
		cv &lt;- sd/mean
		data &lt;- data[order(cv),]
	}
	if ($group == 0){
		data.k &lt;- data
	}
	else if ($group &gt; 0){
		start = ($group-1) * $width + 1
		end = $group * $width
		data.k &lt;- data[,start:end]
	}
	if ($scale){
		if (! $quiet){
			print("Scale data.")
		}
		data.k &lt;- t(apply(data.k,1,scale))
	}
	if (! $quiet){
		print("Cluster data.")
	}
	if ("$clu" == "clara" ){
		data.d &lt;- t(apply(data.k,1,diff))
		data.clara &lt;- clara(data.d, $kclu)
		cluster_172 &lt;- data.clara\$clustering
		#data.clara &lt;- kmeans(data.d, $kclu, iter.max=1000)
		#cluster_172 &lt;- data.clara\$cluster
		rm(data.d)
	}else
	if ("$clu" == 'kmeans'){
		set.seed(3)
		data.clara &lt;- kmeans(data.k, $kclu, iter.max = 1000)
		cluster_172 &lt;- data.clara\$cluster
	}
	tmp_cluster_172 &lt;- mindata + (cluster_172-1) * step
	data.m1 &lt;- cbind(cluster=cluster_172, rownames(data))[,1]
	if (! $quiet){
		print("Output clustered result")
		output &lt;- paste("${file}${midname}", "cluster", sep='.')
		#data.m1 &lt;- data.m1[order(cluster_172),]
		write.table(data.m1, file=output, sep="\t", quote=F, col.names=F)
		print("Sort data by cluster.")
	}
	if (${scale_op}){
		data &lt;- data + ${scale_add}
		data.s &lt;- as.data.frame(t(apply(data, 1, scale)))
		colnames(data.s) &lt;- colnames(data)

		mindata &lt;- min(data.s)
		maxdata &lt;- max(data.s)
		step &lt;- (maxdata-mindata)/$kclu
		tmp_cluster_172 &lt;- mindata + (cluster_172-1) * step
		#---------------add cluster info-------------------
		if ($clusterInclu){
			data.s\$cluster &lt;- tmp_cluster_172
		}
		#----------sort data by cluster-----this must be after add
		#-----cluster info-------------
		data.s &lt;- data.s[order(cluster_172),]
		if (rowZero &gt; 0){
			if (! $quiet) {
				print("Add rows which are all zero")
			}
			if ($clusterInclu){
				if (! $quiet) {
					print("Add cluster info for rows which are all zero")
				}
				newcluster &lt;- mindata - step
				cluster_315_for_zero &lt;- c(rep(newcluster, rowZero)) 
				data.zero\$cluster &lt;- cluster_315_for_zero
			}
			data.s &lt;- rbind(data.zero, data.s)
		}
		if (! $quiet){
			output &lt;- paste("${file}${midname}", \
				"cluster.scaleop.final", sep='.')
			write.table(data.s, file=output, sep="\t", \
				quote=F, col.names=T)
		}
	}
	#--for output original data ---------------------------
	if ($clusterInclu){
		data\$cluster &lt;- tmp_cluster_172
	}
	data &lt;- data[order(cluster_172),]

	if (rowZero &gt; 0){
		if (! $quiet) {
			print("Add rows which are all zero")
		}
		if ($clusterInclu){
			if (! $quiet) {
				print("Add cluster info for rows which are all zero")
			}
			newcluster &lt;- mindata - step
			cluster_315_for_zero &lt;- c(rep(newcluster, rowZero)) 
			data.zero\$cluster &lt;- cluster_315_for_zero
		}
		data &lt;- rbind(data.zero, data)
	}


	if (! $quiet){
		output &lt;- paste("${file}${midname}", "cluster.final", sep='.')
		write.table(data, file=output, sep="\t", quote=F, col.names=T)
	}
	#--for output original data ---------------------------
	#--for use scaled data-----------------------------
	if ($scale_op){
		data &lt;- data.s
	}
	rm(data.m1, data.k, data.clara)
	
}else{
	#---for raw data scale-----no cluster------------
	if ($scale_op){
		colname &lt;- colnames(data)
		data &lt;- as.data.frame(t(apply(data,1,scale)))
		colnames(data) &lt;- colname
	}
}


if (! $quiet){
	print("Melt data.")
}
#oriLen &lt;- dimD[2]
data\$id &lt;- rownames(data)
idlevel &lt;- as.vector(rownames(data))
#data\$idsort &lt;- data\$id[order(data\$cluster)]
#data\$idsort &lt;- order(data\$idsort)
if (! $quiet){
	print("Reorganize data.")
}
#data.m &lt;- melt(data, id.vars = c("id", "idsort"))
#---------------
#data.m &lt;- melt(data, c("id"), names(data)[1:oriLen])
data.m &lt;- melt(data, c("id"))
if (! $quiet){
	output2 &lt;- paste("${file}${midname}", "cluster.melt", sep='.')
	write.table(data.m, file=output2, sep="\t" , quote=F,
	col.names=T, row.names=F)
}
data.m\$id &lt;- factor(data.m\$id, levels=idlevel, ordered=T)

data.m\$value[data.m\$value &lt; $small] &lt;- 0

data.m\$value[data.m\$value &gt; $maximum] &lt;- $maximum

if (! $quiet){
	print("Prepare ggplot layers.")
}

p &lt;- ggplot(data=data.m, aes(x=variable, y=id)) + \
geom_tile(aes(fill=value)) + xlab(NULL) + ylab(NULL)
#facet_grid( .~grp) 

if($gradient){
	gradientC &lt;- c(${gradientC})
	summary_v &lt;- summary(data.m\$value)
	break_v &lt;- c($givenSepartor)
	if (length(break_v) &lt; 3){
		break_v &lt;- \
		unique(c(seq(summary_v[1]-0.00000001,summary_v[2],length=8),seq(summary_v[2],summary_v[3],length=13),seq(summary_v[3],summary_v[5],length=25),seq(summary_v[5],summary_v[6],length=40)))
	}
	
	data.m\$value &lt;- cut(data.m\$value, breaks=break_v,\
		labels=break_v[2:length(break_v)])

	break_v=unique(data.m\$value)
	
	col &lt;- colorRampPalette(gradientC)(length(break_v))
	print(col)
	print(break_v)
	#p &lt;- p + scale_fill_gradientn(colours = c("$xcol", "$mcol","$ycol"), breaks=break_v, labels=format(break_v))
	p &lt;- ggplot(data=data.m, aes(x=variable, y=id)) + \
	geom_tile(aes(fill=value)) + xlab(NULL) + ylab(NULL) + \
	scale_fill_manual(values=col)
	#scale_fill_brewer(palette="PRGn")
} else {
	if( "$log" == ''){
		if (${mid_value_use}){
			p &lt;- p + scale_fill_gradient2(low="$xcol", mid="$mcol",
			high="$ycol", midpoint=median(data.m\$value))
		}else {
			p &lt;- p + scale_fill_gradient(low="$xcol", high="$ycol")
		}
	}else {
		p &lt;- p + scale_fill_gradient(low="$xcol", high="$ycol",
		trans="$log", name="$log value", na.value="$xcol")
	}
} #end the else of gradient 

p &lt;- p + theme(axis.ticks=element_blank())

if ("$xtics" == "FALSE"){
	p &lt;- p + theme(axis.text.x=element_blank())
}else{
	if (${xtics_angle} != 0){
	p &lt;- p + theme(axis.text.x=element_text(angle=${xtics_angle},hjust=1))
	}
}
if ("$ytics" == "FALSE"){
	p &lt;- p + theme(axis.text.y=element_blank())
}

if ("${legend_pos}" != "right"){
	p &lt;- p + theme(legend.position="${legend_pos}")
}

if (! $quiet){
	print("Begin plotting.")
}
png(filename="${file}${midname}.png", width=$uwid, height=$vhig,
res=$res)
p
dev.off()
END

if [ "$execute" == "TRUE" ]; then
	Rscript ${file}${midname}.r
fi

#if [ "$quiet" == "TRUE" ]; then
#	/bin/rm -f ${file}${midname}.r
#fi
#convert -density 200 -flatten ${file}${midname}.eps ${first}${midname}.png


</pre>

<http://stackoverflow.com/questions/9409937/change-the-colour-palette-in-histogram>  
<http://stackoverflow.com/questions/11299705/asymmetric-color-distribution-in-scale-gradient2>  
<http://r.789695.n4.nabble.com/Heatmap-in-R-and-or-ggplot2-td3594590.html>  
<http://stackoverflow.com/questions/14000232/2-color-heatmap-in-r-with-middle-color-anchored-to-a-specific-value>

&#8212;&#8212;&#8212;&#8212;-heatmap with dendrom cluster information&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

http://stackoverflow.com/questions/6673162/reproducing-lattice-dendrogram-graph-with-ggplot2

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;another heatmap fucntion&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

http://www.r-bloggers.com/ggheat-a-ggplot2-style-heatmap-function/