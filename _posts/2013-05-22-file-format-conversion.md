---
title: File format conversion
author: 悟道
layout: post
permalink: /?p=3154
categories:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.Bed to GTF or Gff

<pre class="brush: bash; title: ; notranslate" title="">1.bedToGtf from GenePattern [http://genepattern.broadinstitute.org/gp/pages/index.jsf]
2.scripture
java -Xmx1000m -jar &lt;path_to_scripture&gt;/scripture_alpha2.jar -task toGFF -cufflinks -in your_file.bed -source SCRIPTURE -out your_file.gtf
3.bedToGenePred input.bed stdout | genePredToGtf file stdin output.gtf [ucsc, can not find bedToGenePred]
</pre>

3.Gtf to bed

<pre class="brush: bash; title: ; notranslate" title="">1.gtf2bed from http://code.google.com/p/bedops/wiki/gtf2bed.
$ gtf2bed &lt; foo.gtf | sort-bed - &gt; foo.bed
$ awk '{print $1"\t"$7"\t"$8"\t"($2+1)"\t"$3"\t"$5"\t"$6"\t"$9"\t"(substr($0, index($0,$10)))}' foo.bed &gt; foo_from_gtf2bed.gtf

2.perl gtf2bed.pl input.gtf &gt; output.bed [http://code.google.com/p/ea-utils/source/browse/trunk/clipper/gtf2bed]

</pre>