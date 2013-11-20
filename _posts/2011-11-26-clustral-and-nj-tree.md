---
title: clustral and NJ tree and Phylip usage
author: 悟道
layout: post
permalink: /?p=1277
categories:
  - bioinformatics
tags:
  - bioinformatics
  - msa
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.Install Phylip [<http://evolution.genetics.washington.edu/phylip/install.html>]

> tar xvzf phylip.tar.gz
> 
> cd phylip/src
> 
> make install
> 
> &nbsp;

2.Usage

>  clustalw fastafile -TYPE=PROTEIN -OUTPUT=PHYLIP -OUTFILE=test.phylip [clustalw output file in [**interleaved**][1]]
> 
> ln -s test.phylip infile  [infile is for protdist, the default filename of inputfile]
> 
> /bin/rm outfile [the default filename for protdist output]
> 
> echo &#8216;Y&#8221; | protdist  [Accept default parameters]
> 
> /bin/mv outfile test.distanceMatrix

3.Result

http://cmgm.stanford.edu/phylip/protdist.html

#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

> clustalw fastafile -TYPE=PROTEIN  
> clustalw fastafile -TYPE=PROTEIN -OUTPUT=FASTA -OUTFILE=fastafile.fa  
> clustalw test.fa -TYPE=PROTIEN -OUTPUTTREE=nexus -TREE -QUIET
> 
> sudo apt-get install treeviewx (cracked)  
> sudo apt-get install njplot (segmentation fault when using option -psonly, x11 works well)
> 
> sudo easy_install NetworkX  
> sudo easy_install pydot  
> sudo apt-get install graphviz  
> sudo apt-get install libgraphviz-dev  
> sudo easy_install PyGraphviz

 [1]: http://cmgm.stanford.edu/phylip/sequence.html#1