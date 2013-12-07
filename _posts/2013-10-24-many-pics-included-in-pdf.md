---
title: 将多张图片整合到一个文件并输出PDF
author: 悟道
layout: post
categories:
  - bash
  - tex
  - scripts
tag:
  - bash
  - tex
---

<pre class="brush: bash; title: ; notranslate" title="">#!/bin/bash

#set -x

usage()
{
cat &lt;&lt;EOF
${txtcyn}
Usage:

$0 options${txtrst}

${bldblu}Function${txtrst}:

This script is used generate a picture collection for all pics in
given folder.

${txtbld}OPTIONS${txtrst}:
	-d	The path for pics${bldred}[NECESSARY], like tandem/. The slash
	'/' at the end is alternative. ${txtrst}
	-p	Prefix for header line[${bldred}NECESSARY, like 50-200${txtrst}]
	-o	Output prefix, the name for output files.
		[${bldred}NECESSARY, like 50-200${txtrst}]
	-e	Execute or not[${bldred}Default TRUE, accept FALSE${txtrst}]
EOF
}

dir=
prefix=
output=
execute='TRUE'

while getopts "hd:p:o:e:" OPTION
do
	case $OPTION in
		h)
			usage
			exit 1
			;;
		d)
			dir=$OPTARG
			;;
		p)
			prefix=$OPTARG
			;;
		o)
			output=$OPTARG
			;;
		e)
			execute=$OPTARG
			;;
		?)
			usage
			exit 1
			;;
	esac
done
if [ -z $dir ]; then
	usage
	echo "** No dir **"
	exit 1
fi

if [ -z $prefix ]; then
	usage
	echo "** No prefix **"
	exit 1
fi

if [ -z $output ]; then
	usage
	echo "** No output **"
	exit 1
fi

dir=`echo ${dir%/}`
dir=$dir"/"

file=${output}.tex


newdir=${prefix}.${output}.${dir}

/bin/rm -rf ${newdir}*
/bin/mkdir -p $newdir


cat &lt;&lt;END &gt;$file
	
\documentclass[presentation, compress, blue, 9pt]{beamer}

\usetheme{Frankfurt}
\usefonttheme[stillsansseriflarge, stillsansserifsmall]{serif}

\usepackage[english]{babel}
\usepackage{graphicx} %used to insert picture
\usepackage{times}
\usepackage{color}

\usepackage{caption}

%\captionsetup{labelformat=simple, labelsep=period, font=scriptsize}
%\captionsetup[subfigure]{labelformat=simple}
%\renewcommand\thesubfigure{\Alph{subfigure}}

\usepackage{xcolor}


\graphicspath{{${newdir}}} 
\setbeamercovered{dynamic}

\setbeamertemplate{caption}[numbered]
%%this delete the naigation bar at bottom-right
\setbeamertemplate{navigation symbols}{} 
\setbeamertemplate{blocks}[rounded][shadow=true]
%-------------newcommand---------------------------------------------
\newcommand{\graph}[1]{\includegraphics[width=\textwidth,
height=0.8\textheight, keepaspectratio=true]{#1}}
\newcommand{\graphe}[1]{
\begin{figure}
  \centering
  \includegraphics[width=\textwidth, height=0.85\textheight, keepaspectratio=true]{#1}
\end{figure}}
%
% The following info should normally be given in you main file:
%
\title{To my Dou dou}
\author[Qhy]{Qhy}
\date{\today}

\begin{document}

\frame1{\titlepage} %delete the navagation bar at first page


\part&lt;presentation&gt;{Main Talk}

END

num=0


for i in `ls ${dir} | grep 'png$'`; do
	((num++))
	title=${prefix}"-"${num}
	subtitle=`echo $i | \
		awk '{split($0,a,"_"); chr=a[1]; start=a[2]; \
	split(a[3],b,"."); end=b[1]; name=chr":"start"-"end; print \
		name,"(Distance:", end-start,"nt)";}'`
	/bin/cp -f ${dir}${i} ${newdir}${num}.png
	#echo $pic_file
	cat &lt;&lt;END &gt;&gt;$file
\begin{frame}1
  \begin{figure}
	\centering
	\textbf{${title}}
  \end{figure}
  \begin{figure}
	\centering
	${subtitle}
  \end{figure}
  \graphe{${num}}
\end{frame}
END
done

#\begin{frame}1
#  \begin{figure}#
#	\centering
#	\Huge Thank you!
#  \end{figure}
#\end{frame}

cat &lt;&lt;END &gt;&gt;$file
\end{document}
END

if [ "$execute" == "TRUE" ]; then
	xelatex $file
fi
</pre>
