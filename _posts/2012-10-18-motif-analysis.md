---
title: Motif analysis
author: 悟道
layout: post
permalink: /?p=2552
categories:
  - bioinformatics
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

Motif analysis  
We first identified 19 clusters of tissue-specific enhancers (Fig. 4e), and ran HOMER de novo  
motif finding software on the center 2kb regions with the following parameters:  
findMotifsGenome.pl peak\_file mm9 ou tput\_directory -size 2000 -len 8. Only motifs with P  
value < 1e-20 were kept for further analysis. To identify the de novo motifs with known  
transcription factor motifs in the mammalian genome, we used the TOMTOM program  
from  
the MEME software suite (http://meme.sdsc.edu/meme4\_3\_0/cgi-bin/tomtom.cgi). We chose  
TRANSFAC, JASPAR CORE and UNIPROBE as the candidate databases. The comparison  
function was set as “Pearson correlation coefficient”. Typically, there were multiple candidates  
for each de novo motif. In an effort to identify the most likely transcription factor, we filtered the  
candidates by choosing a cutoff P value < 0.0005 and an empirical FDR < 0.02. To compute the

FDR for each motif, we shuffled the motif 1000 times and run TOMTOM with the pseudo motifs  
against the known motif database. The FDR wa s computed as the rank of the original P value  
among the P values for the randomly generated motifs. Next we manu ally inspected the  
remaining candidates, requiring that the candidate transcription factor is expressed in the same  
tissue. To perform the motif enrichment analysis, we combined all de novo motifs and the  
known motifs from HOMER  
59  
. Only the motifs with an enrichment P value < 1e-20 in at least  
one cluster of enhancers were presented in Fig. 4f.  
To perform the motif conservation study, we first located the motif occurrences in the  
tissue-specific enhancers. The conservation score was computed as the sum of the average of  
phastCon scores at each base pair for all motif occurrences. To compare, we randomly generated  
1000 8-mers and compute their average PhastCon score. We repeated this step 1000 times to  
generate a population of the phasCcon scores. Then based on the average and standard deviation  
of this population, we computed a Z-score for each de novo motif. We defined a motif as  
conserved when z-score > 2.58.

&nbsp;

&nbsp;

http://www.nature.com/nature/journal/vaop/ncurrent/full/nature11243.html?WT.ec_id=NATURE-20120705

&nbsp;

&nbsp;

We next screened the CpG island sets for TF motif occurrences. 668 position weight matrices (PWMs) were obtained from the Jaspar (Release 3.0 [[34]][1]) and TRANSFAC (Release 9.4; [[35]][2]) databases, excluding any non-vertebrate factors. We prepared sets of Ezh2-positive and Ezh2-negative sequences by extracting each CpG island along with flanking sequence equal to 50% of its length. The MAST algorithm [[36]][3] was then used to search for significant PWM matches (p<5e-5) in the Ezh2-positive and negative sets. Occurrences were length-normalized and used to calculate ratios that reflect the enrichment in the Ezh2-positive set relative to the Ezh2-negative set, or vice versa. We identified significantly over-represented motifs using Fisher&#8217;s exact test with Bonferroni-adjusted p-values. These candidate motifs were then scrambled, re-scored, and excluded if any enrichment was observed in the scramble.

We used a clustering algorithm to collapse similar motifs identified as enriched in one of the sets to a single consensus sequence [[65]][4]. This was necessary due to high motif redundancy in the databases. After clustering, all intra-cluster motif occurrences overlapping by more than 50% were counted as a single instance. Expression values for corresponding DNA binding proteins were determined from previously published Affymetrix mRNA profiles for v6.5 ES cells [[16]][5].

A simple count-based model was used to determine the extent to which motif occurrences are predictive of Ezh2 status. The motif content which allowed for maximum discrimination in mouse is as follows: a CpG island was predicted to be Ezh2-positive if it either (i) contained >8 ‘Ezh2-positive’ motifs or (ii) contained >4 ‘Ezh2-positive’ motifs and <2 ‘Ezh2-negative’ motifs. Ezh2 status in human was predicted using the motifs identified in mouse but with the following metric: a CpG island was predicted to be Ezh2-positive if it contained >15 ‘Ezh2-positive’ motifs and <2 ‘Ezh2-negative’ motifs.

http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1000242

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;  
findMotifs.pl or findMotifsGenome.pl when using fasta or centered position to search for motifs. The position of center is the length of fasta divide 2.  
100&#8211;50  
101&#8211;50  
102&#8211;51  
Motifs in negative value means before central point. You can just add the returned position value to midpoint value to get the 1-based location of the motif.  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

<div class="wp_codebox">
  <table>
    <tr id="p2552168">
      <td class="code" id="p2552code168">
        <pre class="make" style="font-family:monospace;"><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">cell</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">.</span>macs_peaks<span style="color: #004400;">.</span>homer<span style="color: #004400;">.</span>cmyc<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">cell</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">.</span>macs_summits<span style="color: #004400;">.</span>bed
        findMotifsGenome<span style="color: #004400;">.</span>pl <span style="color: #000088; font-weight: bold;">$&lt;</span> mm9 <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #004400;">-</span>size <span style="color: #CC2200;">2000</span> <span style="color: #004400;">-</span>p <span style="color: #CC2200;">8</span> <span style="color: #004400;">-</span>cache <span style="color: #CC2200;">1000</span>
        <span style="color: #339900; font-style: italic;">#findMotifsGenome.pl $&lt; mm9 $@ -size 2000 -p 8 -cache 1000 -find ~/home/soft/homer/data/knownTFs/vertebrates/known.motifs.cMyc_nMyc -dumpFasta &gt;$@.result</span>
        pythonmail2<span style="color: #004400;">.</span>py <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span>
        tail <span style="color: #004400;">-</span>n <span style="color: #004400;">+</span><span style="color: #CC2200;">2</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">.</span>result <span style="color: #004400;">|</span> cut <span style="color: #004400;">-</span>f <span style="color: #CC2200;">1</span> <span style="color: #004400;">|</span> sort <span style="color: #004400;">-</span>u <span style="color: #004400;">&gt;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">.</span>result<span style="color: #004400;">.</span>peak
        parseFindMotifsForHeatmap<span style="color: #004400;">.</span>py <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">.</span>result <span style="color: #004400;">-</span><span style="color: #CC2200;">1000</span> <span style="color: #CC2200;">1000</span> <span style="color: #CC2200;">1</span> <span style="color: #CC2200;">1</span> <span style="color: #004400;">&gt;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">.</span>result<span style="color: #004400;">.</span>heat</pre>
      </td>
    </tr>
  </table>
</div>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;  
parseFindMotifsForHeatmap.py

<div class="wp_codebox">
  <table>
    <tr id="p2552169">
      <td class="code" id="p2552code169">
        <pre class="python" style="font-family:monospace;">&nbsp;
<span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
<span style="color: #808080; font-style: italic;"># -*- coding: utf-8 -*-</span>
<span style="color: #808080; font-style: italic;">#from __future__ import division, with_statement</span>
<span style="color: #483d8b;">''</span><span style="color: #483d8b;">'
Copyright 2010, 陈同 (chentong_biology@163.com).  
Please see the license file for legal information.
===========================================================
'</span><span style="color: #483d8b;">''</span>
__author__ = <span style="color: #483d8b;">'chentong & ct586[9]'</span>
__author_email__ = <span style="color: #483d8b;">'chentong_biology@163.com'</span>
<span style="color: #808080; font-style: italic;">#=========================================================</span>
<span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
&nbsp;
<span style="color: #ff7700;font-weight:bold;">def</span> main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    len_argv = <span style="color: #008000;">len</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> len_argv <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">4</span>:
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">"Print the result to file"</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #66cc66;">&gt;&gt;</span>sys.<span style="color: black;">stderr</span>, <span style="color: #483d8b;">'Using python %s filename min max head[1]<span style="color: #000099; font-weight: bold;">\</span>
strand_info[consider stand info if 1 is given else do not consider <span style="color: #000099; font-weight: bold;">\</span>
strand info when 0 is given.]'</span> <span style="color: #66cc66;">%</span> <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span>
        <span style="color: #dc143c;">sys</span>.<span style="color: black;">exit</span><span style="color: black;">&#40;</span><span style="color: #ff4500;"></span><span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">#--------------------------------------------------------------</span>
<span style="color: #808080; font-style: italic;">#'''</span>
<span style="color: #808080; font-style: italic;">#Offset : Count form left to right no matter + or -</span>
<span style="color: #808080; font-style: italic;">#'''</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> len_argv <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">4</span>:
        head = <span style="color: #008000;">int</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
        head = <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> len_argv <span style="color: #66cc66;">&gt;</span> <span style="color: #ff4500;">5</span>:
        strand = <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
        strand = <span style="color: #ff4500;"></span>
    <span style="color: #808080; font-style: italic;">#--------------------------------------</span>
    aDict = <span style="color: black;">&#123;</span><span style="color: black;">&#125;</span>
    <span style="color: #008000;">min</span> = <span style="color: #008000;">int</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #008000;">max</span> = <span style="color: #008000;">int</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #008000;">file</span> = <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> line <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">open</span><span style="color: black;">&#40;</span><span style="color: #008000;">file</span><span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">if</span> head:
            head -= <span style="color: #ff4500;">1</span>
            <span style="color: #ff7700;font-weight:bold;">continue</span>
        <span style="color: #808080; font-style: italic;">#-----------------------</span>
        lineL = line.<span style="color: black;">split</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">"<span style="color: #000099; font-weight: bold;">\t</span>"</span><span style="color: black;">&#41;</span>
        start = <span style="color: #008000;">int</span><span style="color: black;">&#40;</span>lineL<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
        end = start + <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>lineL<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;">#not inciluded</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>lineL<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #ff7700;font-weight:bold;">in</span> aDict<span style="color: black;">&#41;</span>:
            aDict<span style="color: black;">&#91;</span>lineL<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span> = <span style="color: black;">&#91;</span><span style="color: black;">&#40;</span>start, end, lineL<span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            aDict<span style="color: black;">&#91;</span>lineL<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span>.<span style="color: black;">append</span><span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>start, end, lineL<span style="color: black;">&#91;</span><span style="color: #ff4500;">4</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #808080; font-style: italic;">#------------------------------------------------------------</span>
    <span style="color: #ff7700;font-weight:bold;">if</span> strand:
        vDict = <span style="color: black;">&#123;</span><span style="color: #483d8b;">'+'</span>:<span style="color: #483d8b;">'1'</span>,  <span style="color: #483d8b;">'-'</span>:<span style="color: #483d8b;">'-1'</span><span style="color: black;">&#125;</span>
    <span style="color: #ff7700;font-weight:bold;">else</span>:
        vDict = <span style="color: black;">&#123;</span><span style="color: #483d8b;">'+'</span>:<span style="color: #483d8b;">'1'</span>,  <span style="color: #483d8b;">'-'</span>:<span style="color: #483d8b;">'1'</span><span style="color: black;">&#125;</span>
    step = <span style="color: #ff4500;">1</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">"Peak<span style="color: #000099; font-weight: bold;">\t</span>%s"</span> <span style="color: #66cc66;">%</span> <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\t</span>'</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span><span style="color: black;">&#91;</span><span style="color: #008000;">str</span><span style="color: black;">&#40;</span>i<span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span><span style="color: #008000;">min</span>, <span style="color: #008000;">max</span>+<span style="color: #ff4500;">1</span>, step<span style="color: black;">&#41;</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> key,  valueL <span style="color: #ff7700;font-weight:bold;">in</span> aDict.<span style="color: black;">items</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
        newdict = <span style="color: black;">&#123;</span><span style="color: black;">&#125;</span>
        <span style="color: #ff7700;font-weight:bold;">for</span> itemL <span style="color: #ff7700;font-weight:bold;">in</span> valueL:
            <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span>itemL<span style="color: black;">&#91;</span><span style="color: #ff4500;"></span><span style="color: black;">&#93;</span>, itemL<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>:
                newdict<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span> = vDict<span style="color: black;">&#91;</span>itemL<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#93;</span>
        <span style="color: #808080; font-style: italic;">#----------------------------------------</span>
        tmpvalue = <span style="color: black;">&#91;</span>key<span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span><span style="color: #008000;">min</span>, <span style="color: #008000;">max</span>+<span style="color: #ff4500;">1</span>, step<span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">if</span> i <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #ff7700;font-weight:bold;">in</span> newdict:
                tmpvalue.<span style="color: black;">append</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'0'</span><span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">else</span>:
                tmpvalue.<span style="color: black;">append</span><span style="color: black;">&#40;</span>newdict<span style="color: black;">&#91;</span>i<span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
        <span style="color: #808080; font-style: italic;">#-------------------------------------------</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\t</span>'</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span>tmpvalue<span style="color: black;">&#41;</span>
&nbsp;
&nbsp;
<span style="color: #808080; font-style: italic;">#-----------------------------------------------------------------------</span>
<span style="color: #ff7700;font-weight:bold;">if</span> __name__ == <span style="color: #483d8b;">'__main__'</span>:
    main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre>
      </td>
    </tr>
  </table>
</div>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;

<pre class="brush: python; title: transferfindMotifsOutputToBed.py; notranslate" title="transferfindMotifsOutputToBed.py">#!/usr/bin/env python
# -*- coding: utf-8 -*-
#from __future__ import division, with_statement
'''
Copyright 2013, 陈同 (chentong_biology@163.com).  
===========================================================
'''
__author__ = 'chentong & ct586[9]'
__author_email__ = 'chentong_biology@163.com'
#=========================================================
'''
Functionla description

This transfers the output of findMotifsGenome.pl to normal bed file.
'''

import sys
import os
from time import localtime, strftime 
timeformat = "%Y-%m-%d %H:%M:%S"
from optparse import OptionParser as OP

def cmdparameter(argv):
    if len(argv) == 1:
        cmd = 'python ' + argv[0] + ' -h'
        os.system(cmd)
        sys.exit(1)
    desc = ""
    usages = "%prog -i homer_out -b bed_used_for_findMotif -t rna"
    parser = OP(usage=usages)
    parser.add_option("-i", "--input-file", dest="filein",
        metavar="FILEIN", help="This is the output of \
findMotifsGenome.pl when using -find. ")
    parser.add_option("-b", "--bed-file", dest="bedin",
        metavar="inputBed", help="The original bed file which has been given to \
findMotifsGenome.pl and used to get the file given to -i. If -t is \
RNA, an at least six-column file is needed. If -t is DNA,  an at-leat \
four-column file is needed. Other columns will be ignored. \
If you run findMotifsGenome.pl using -size 200 or other parameters \
rather than &lt;-size given&gt;,  you may need the real bed which \
findMotifsGenome.pl used. ")
    parser.add_option("-t", "--type", dest="type",
        default='RNA', help="The attribute of given bed file \
represented sequences. For DNA, the strand information of regions in \
output bed file is accordant with output file of findMotifsGenome.pl. \
For RNA, the strand information of one region is accordant with its \
strand information in file given to -i.")
    parser.add_option("-v", "--verbose", dest="verbose",
        default=0, help="Show process information")
    parser.add_option("-d", "--debug", dest="debug",
        default=False, help="Debug the program")
    (options, args) = parser.parse_args(argv[1:])
    assert options.filein != None, "A filename needed for -i"
    return (options, args)
#--------------------------------------------------------------------


def main():
    options, args = cmdparameter(sys.argv)
    #-----------------------------------
    file = options.filein
    bedin = options.bedin
    type = options.type
    verbose = options.verbose
    debug = options.debug
    #-----------------------------------
    #--------get the coordinate of original bed file------
    bedinD = {}
    '''
    bedinD = {name:(chr, start, end, strand)}
    '''
    for line in open(bedin):
        lineL = line.split()
        if type == 'RNA':
            assert len(lineL) &gt;=6, line
            key = lineL[3]
            if key not in bedinD:
                bedinD[key] = (lineL[0], int(lineL[1]), int(lineL[2]), lineL[5])
            else:
                print &gt;&gt;sys.stderr, "Diplicate region name %s" % key
        elif type == 'DNA':
            if key not in bedinD:
                bedinD[key] = (lineL[0], int(lineL[1], int(lineL[2])))
            else:
                print &gt;&gt;sys.stderr, "Diplicate region name %s" % key
    #--------read findMotifGenoms.pl output---------------------------------
    if file == '-':
        fh = sys.stdin
    else:
        fh = open(file)
    #--------------------------------
    motifD ={}
    '''
    motifD = {name:[(start, end, value, strand),]}
    '''
    head = 1
    for line in fh:
        if head:
            head -= 1
            continue
        #-----------------------------
        lineL = line.split()
        name = lineL[0]
        start = int(lineL[1])
        end  = start + len(lineL[2])
        if type == 'RNA':
            tmpTuple = (start,end,lineL[5])
        elif type == 'DNA':
            strand = lineL[4]
            tmpTuple = (start,end,lineL[5],strand)
        if name not in motifD:
            motifD[name] = []
        motifD[name].append(tmpTuple)
    #-------------END reading file----------
    #----close file handle for files-----
    if file != '-':
        fh.close()
    #-----------end close fh-----------
    #----------output-----------------
    '''
    bedinD = {name:(chr, start, end, strand)}
    motifD = {name:[(start, end, value, strand),]}
    '''
    for key, valueL in motifD.items():
        chr         = bedinD[key][0]
        genomeStart = bedinD[key][1]
        genomeEnd   = bedinD[key][2]
        if type == 'RNA':
            strand = bedinD[key][3]
        #---------------------------------
        label = 1
        for item in valueL:
            if type == 'RNA' and strand == '+':
                newstart = genomeStart + item[0]
                newend   = genomeStart + item[1]
            #pay attention to negative strand----------
            elif type == 'RNA' and strand == '-':
                newstart = genomeEnd - item[1]
                newend   = genomeEnd - item[0]
            score   = item[2]
            if type == 'DNA':
                strand = item[3]
            outputL = [chr, str(newstart), str(newend),
                    key+'@'+str(label), score, strand]
            print '\t'.join(outputL)
            label += 1
    #----------finish output------------
    if verbose:
        print &gt;&gt;sys.stderr,\
            "--Successful %s" % strftime(timeformat, localtime())
if __name__ == '__main__':
    startTime = strftime(timeformat, localtime())
    main()
    endTime = strftime(timeformat, localtime())
    fh = open('python.log', 'a')
    print &gt;&gt;fh, "%s\n\tRun time : %s - %s " % \
        (' '.join(sys.argv), startTime, endTime)
    fh.close()


</pre>

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

 [1]: http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1000242#pgen.1000242-Sandelin1
 [2]: http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1000242#pgen.1000242-Matys1
 [3]: http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1000242#pgen.1000242-Bailey1
 [4]: http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1000242#pgen.1000242-Xie1
 [5]: http://www.plosgenetics.org/article/info%3Adoi%2F10.1371%2Fjournal.pgen.1000242#pgen.1000242-Mikkelsen1