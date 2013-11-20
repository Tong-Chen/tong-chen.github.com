---
title: Gene Set Summary Statistics
author: 悟道
layout: post
permalink: /?p=2702
categories:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

http://genomewiki.ucsc.edu/index.php/Gene\_Set\_Summary_Statistics

&nbsp;

# Gene Set Summary Statistics

<div id="bodyContent">
  <div id="contentSub">
  </div>
  
  <table id="toc">
    <tr>
      <td>
        <div id="toctitle">
          <h2>
            Contents
          </h2>
          
          <p>
            [<a id="togglelink">hide</a>]</div> <ul>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#gene_sets_measured">1 gene sets measured</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#summary_of_gene_and_exon_counts">2 summary of gene and exon counts</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#summary_of_exon_size_statistics">3 summary of exon size statistics</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#summary_of_intron_size_statistics">4 summary of intron size statistics</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#Top_five_exon_count_genes">5 Top five exon count genes</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#Top_five_largest_CDS_extent_genes">6 Top five largest CDS extent genes</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#Top_five_smallest_transcript_genes">7 Top five smallest transcript genes</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#Custom_Track_of_Small_Exons_and_Introns">8 Custom Track of Small Exons and Introns</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#Histogram_graphs">9 Histogram graphs</a>
              </li>
              <li>
                <a href="http://genomewiki.ucsc.edu/index.php/Gene_Set_Summary_Statistics#Methods">10 Methods</a>
              </li>
            </ul></td> </tr> </tbody> </table> 
            
            <h2>
              gene sets measured
            </h2>
            
            <ul>
              <li>
                hg17 &#8211; knownGenes version 2
              </li>
              <li>
                hg18 &#8211; knownGenes version 3
              </li>
              <li>
                mm8 &#8211; knownGenes version 2
              </li>
              <li>
                mm9 &#8211; knownGenes version 3
              </li>
            </ul>
            
            <p>
              The min, max and mean measurements are <em>per gene</em>
            </p>
            
            <h2>
              summary of gene and exon counts
            </h2>
            
            <table border="1">
              <tr>
                <th>
                  db
                </th>
                
                <th>
                  gene<br /> count
                </th>
                
                <th>
                  total exon<br /> count
                </th>
                
                <th>
                  min exon<br /> count
                </th>
                
                <th>
                  max exon<br /> count
                </th>
                
                <th>
                  mean exon<br /> count
                </th>
              </tr>
              
              <tr>
                <th>
                  hg17
                </th>
                
                <td align="RIGHT">
                  39368
                </td>
                
                <td align="RIGHT">
                  405720
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  149
                </td>
                
                <td align="RIGHT">
                  10
                </td>
              </tr>
              
              <tr>
                <th>
                  hg18
                </th>
                
                <td align="RIGHT">
                  56722
                </td>
                
                <td align="RIGHT">
                  519308
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  2899
                </td>
                
                <td align="RIGHT">
                  9
                </td>
              </tr>
              
              <tr>
                <th>
                  mm8
                </th>
                
                <td align="RIGHT">
                  31863
                </td>
                
                <td align="RIGHT">
                  314628
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  313
                </td>
                
                <td align="RIGHT">
                  10
                </td>
              </tr>
              
              <tr>
                <th>
                  mm9
                </th>
                
                <td align="RIGHT">
                  49220
                </td>
                
                <td align="RIGHT">
                  417114
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  610
                </td>
                
                <td align="RIGHT">
                  8
                </td>
              </tr>
            </table>
            
            <h2>
              summary of exon size statistics
            </h2>
            
            <table border="1">
              <tr>
                <th>
                  db
                </th>
                
                <th>
                  sum exon<br /> sizes
                </th>
                
                <th>
                  min exon<br /> size
                </th>
                
                <th>
                  max exon<br /> size
                </th>
                
                <th>
                  mean exon<br /> size
                </th>
              </tr>
              
              <tr>
                <th>
                  hg17
                </th>
                
                <td align="RIGHT">
                  106839720
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  18172
                </td>
                
                <td align="RIGHT">
                  263
                </td>
              </tr>
              
              <tr>
                <th>
                  hg18
                </th>
                
                <td align="RIGHT">
                  146371091
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  36861
                </td>
                
                <td align="RIGHT">
                  282
                </td>
              </tr>
              
              <tr>
                <th>
                  mm8
                </th>
                
                <td align="RIGHT">
                  83159087
                </td>
                
                <td align="RIGHT">
                  4
                </td>
                
                <td align="RIGHT">
                  17497
                </td>
                
                <td align="RIGHT">
                  264
                </td>
              </tr>
              
              <tr>
                <th>
                  mm9
                </th>
                
                <td align="RIGHT">
                  117671086
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  29698
                </td>
                
                <td align="RIGHT">
                  282
                </td>
              </tr>
            </table>
            
            <h2>
              summary of intron size statistics
            </h2>
            
            <table border="1">
              <tr>
                <th>
                  db
                </th>
                
                <th>
                  sum intron<br /> sizes
                </th>
                
                <th>
                  min intron<br /> size
                </th>
                
                <th>
                  max intron<br /> size
                </th>
                
                <th>
                  mean intron<br /> size
                </th>
              </tr>
              
              <tr>
                <th>
                  hg17
                </th>
                
                <td align="RIGHT">
                  2223224397
                </td>
                
                <td align="RIGHT">
                  6
                </td>
                
                <td align="RIGHT">
                  1096450
                </td>
                
                <td align="RIGHT">
                  6069
                </td>
              </tr>
              
              <tr>
                <th>
                  hg18
                </th>
                
                <td align="RIGHT">
                  2784923600
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  1047320
                </td>
                
                <td align="RIGHT">
                  6023
                </td>
              </tr>
              
              <tr>
                <th>
                  mm8
                </th>
                
                <td align="RIGHT">
                  1476081990
                </td>
                
                <td align="RIGHT">
                  9
                </td>
                
                <td align="RIGHT">
                  1347550
                </td>
                
                <td align="RIGHT">
                  5220
                </td>
              </tr>
              
              <tr>
                <th>
                  mm9
                </th>
                
                <td align="RIGHT">
                  2055504784
                </td>
                
                <td align="RIGHT">
                  1
                </td>
                
                <td align="RIGHT">
                  1253430
                </td>
                
                <td align="RIGHT">
                  5589
                </td>
              </tr>
            </table>
            
            <h2>
              Top five exon count genes
            </h2>
            
            <table border="1">
              <tr>
                <th>
                  db
                </th>
                
                <th colspan="5">
                  gene name (exon count)
                </th>
              </tr>
              
              <tr>
                <th>
                  hg17
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr2:152167363-152416454" rel="nofollow">NM_004543</a> (149)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr6:152534937-153050100" rel="nofollow">AF535142</a> (146)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr6:152534937-153050100" rel="nofollow">AF535142</a> (146)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr6:152534937-153050100" rel="nofollow">NM_033071</a> (146)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr6:152535029-153050648" rel="nofollow">AF495910</a> (146)
                </td>
              </tr>
              
              <tr>
                <th>
                  hg18
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr14:105065301-106352275" rel="nofollow">uc001yrq.1</a> (2899)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr22:20715572-21595078" rel="nofollow">uc002zvw.1</a> (322)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr2:179098964-179380395" rel="nofollow">uc002umr.1</a> (313)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr2:88937989-89411302" rel="nofollow">uc002stk.1</a> (217)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr2:179098964-179380395" rel="nofollow">uc002umt.1</a> (194)
                </td>
              </tr>
              
              <tr>
                <th>
                  mm8
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr2:76504823-76783386" rel="nofollow">NM_011652</a> (313)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr2:76504823-76783386" rel="nofollow">NM_028004</a> (192)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr9:108810682-108841812" rel="nofollow">NM_007738</a> (118)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr1:33956371-34252174" rel="nofollow">NM_134448</a> (99)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr4:122852023-123186663" rel="nofollow">DQ067088</a> (99)
                </td>
              </tr>
              
              <tr>
                <th>
                  mm9
                </th>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr12:114498400-117248164" rel="nofollow">uc007pgj.1</a> (610)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr2:76542041-76820604" rel="nofollow">uc008kfn.1</a> (313)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr2:76542041-76820604" rel="nofollow">uc008kfo.1</a> (192)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr2:51992167-52194318" rel="nofollow">uc008jqv.1</a> (157)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr9:108855790-108886920" rel="nofollow">uc009rrh.1</a> (118)
                </td>
              </tr>
            </table>
            
            <h2>
              Top five largest CDS extent genes
            </h2>
            
            <table border="1">
              <tr>
                <th>
                  db
                </th>
                
                <th colspan="5">
                  gene name (CDS extent size: thickEnd-thickStart)
                </th>
              </tr>
              
              <tr>
                <th>
                  hg17
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr7:145251477-147555734" rel="nofollow">NM_014141</a> (2298740)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chrX:30897002-33117383" rel="nofollow">NM_000109</a> (2217347)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr11:82846625-85015962" rel="nofollow">CR749820</a> (2138880)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chrX:30897002-32989330" rel="nofollow">NM_004006</a> (2089394)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chrX:30898403-32989184" rel="nofollow">X14298</a> (2089394)
                </td>
              </tr>
              
              <tr>
                <th>
                  hg18
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr7:145444386-147749019" rel="nofollow">uc003weu.1</a> (2298740)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chrX:31047266-33267647" rel="nofollow">uc004ddb.1</a> (2217347)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr11:82843701-85015962" rel="nofollow">uc001pak.1</a> (2138880)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chrX:31047266-33139594" rel="nofollow">uc004dda.1</a> (2089394)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr8:2782789-4839736" rel="nofollow">uc003wqd.1</a> (2055833)
                </td>
              </tr>
              
              <tr>
                <th>
                  mm8
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chrX:79201622-81457760" rel="nofollow">NM_007868</a> (2253366)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr6:44989695-47230955" rel="nofollow">NM_001004357</a> (2238304)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr2:40418782-42475607" rel="nofollow">NM_053011</a> (2055883)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr2:140086871-142081491" rel="nofollow">AK134694</a> (1988713)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr8:15895480-17535258" rel="nofollow">NM_053171</a> (1639258)
                </td>
              </tr>
              
              <tr>
                <th>
                  mm9
                </th>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chrX:80194242-82450380" rel="nofollow">uc009tri.1</a> (2253366)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr6:45010087-47251368" rel="nofollow">uc009bst.1</a> (2238325)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr16:39984484-42176405" rel="nofollow">uc007zfr.1</a> (2189582)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr2:40452293-42509118" rel="nofollow">uc008jon.1</a> (2055883)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr2:140221166-142215786" rel="nofollow">uc008mpv.1</a> (1988713)
                </td>
              </tr>
            </table>
            
            <h2>
              Top five smallest transcript genes
            </h2>
            
            <table border="1">
              <tr>
                <th>
                  db
                </th>
                
                <th colspan="5">
                  gene name (transcript size: txEnd-txStart)
                </th>
              </tr>
              
              <tr>
                <th>
                  hg17
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr4:69806230-69806397" rel="nofollow">AF241539</a> (168)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr7:129369319-129369494" rel="nofollow">AF277175</a> (176)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chrX:9353026-9353265" rel="nofollow">AY459291</a> (240)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr1:35869683-35869925" rel="nofollow">AY605064</a> (243)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg17&position=chr7:128643905-128644162" rel="nofollow">AF503918</a> (258)
                </td>
              </tr>
              
              <tr>
                <th>
                  hg18
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr9:130062323-130062342" rel="nofollow">uc004buj.1</a> (20)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr1:65874524-65874545" rel="nofollow">uc001dcm.1</a> (22)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr12:52671813-52671834" rel="nofollow">uc001seo.1</a> (22)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr12:56504708-56504729" rel="nofollow">uc001sqn.1</a> (22)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=hg18&position=chr20:15523127-15523148" rel="nofollow">uc002wpa.1</a> (22)
                </td>
              </tr>
              
              <tr>
                <th>
                  mm8
                </th>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chrX:12185020-12185236" rel="nofollow">AJ319753</a> (217)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr3:92585666-92585896" rel="nofollow">BC107019</a> (231)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr11:70546334-70546619" rel="nofollow">BC016221</a> (286)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr16:88757957-88758259" rel="nofollow">NM_130876</a> (303)
                </td>
                
                <td>
                  <a href="http://genome.ucsc.edu/cgi-bin/hgTracks?db=mm8&position=chr16:88773645-88773948" rel="nofollow">NM_130873</a> (304)
                </td>
              </tr>
              
              <tr>
                <th>
                  mm9
                </th>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr1:74440898-74440919" rel="nofollow">uc007bma.1</a> (22)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr10:85230424-85230445" rel="nofollow">uc007gmr.1</a> (22)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr11:77886549-77886570" rel="nofollow">uc007khz.1</a> (22)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr12:110831098-110831119" rel="nofollow">uc007pay.1</a> (22)
                </td>
                
                <td>
                  <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=mm9&position=chr13:54944553-54944574" rel="nofollow">uc007qpn.1</a> (22)
                </td>
              </tr>
            </table>
            
            <h2>
              Custom Track of Small Exons and Introns
            </h2>
            
            <p>
              Custom track: <a href="http://genome-test.cse.ucsc.edu/cgi-bin/hgTracks?db=hg18&hgt.customText=http://genomewiki.ucsc.edu/images/3/37/Hg18KnownGenesSmallIntronsExonsCt.txt.gz" rel="nofollow">Hg18 small exons and introns</a> on the UCSC Genes track
            </p>
            
            <p>
              These are exons of size less than 22 bases, and introns of size less than 12 bases. The score column contains the size and thus you can filter smaller subsets via the score column in the table browser.
            </p>
            
            <p>
              These small exons and introns are used to maintain frame coding boundaries as found in mRNAs compared to the reference genome coordinates.
            </p>
            
            <h2>
              Histogram graphs
            </h2>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Hg17_hg18.exonCount.png"><img src="http://genomewiki.ucsc.edu/images/c/ce/Hg17_hg18.exonCount.png" alt="Hg17 hg18.exonCount.png" width="896" height="384" /></a> The caption on the graph above is incorrect. The X axis is Exon Count per Gene
            </p>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Mm8_mm9.exonCount.png"><img src="http://genomewiki.ucsc.edu/images/8/86/Mm8_mm9.exonCount.png" alt="Mm8 mm9.exonCount.png" width="896" height="384" /></a> The caption on the graph above is incorrect. The X axis is Exon Count per Gene
            </p>
            
            <hr />
            
            <hr />
            
            <hr />
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Hg17_hg18.exonSize.png"><img src="http://genomewiki.ucsc.edu/images/9/9a/Hg17_hg18.exonSize.png" alt="Hg17 hg18.exonSize.png" width="896" height="384" /></a>
            </p>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Mm8_mm9.exonSize.png"><img src="http://genomewiki.ucsc.edu/images/f/f1/Mm8_mm9.exonSize.png" alt="Mm8 mm9.exonSize.png" width="896" height="384" /></a>
            </p>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Hg17_hg18_exonsTo300.png"><img src="http://genomewiki.ucsc.edu/images/3/30/Hg17_hg18_exonsTo300.png" alt="Hg17 hg18 exonsTo300.png" width="896" height="384" /></a>
            </p>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Mm8_mm9_exonsTo300.png"><img src="http://genomewiki.ucsc.edu/images/9/9d/Mm8_mm9_exonsTo300.png" alt="Mm8 mm9 exonsTo300.png" width="896" height="384" /></a>
            </p>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Hg17_hg18.intronsTo170.png"><img src="http://genomewiki.ucsc.edu/images/e/ef/Hg17_hg18.intronsTo170.png" alt="Hg17 hg18.intronsTo170.png" width="896" height="384" /></a>
            </p>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Mm8_mm9.intronsTo170.png"><img src="http://genomewiki.ucsc.edu/images/1/16/Mm8_mm9.intronsTo170.png" alt="Mm8 mm9.intronsTo170.png" width="896" height="384" /></a>
            </p>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Hg17_hg18.intronSize.png"><img src="http://genomewiki.ucsc.edu/images/e/e3/Hg17_hg18.intronSize.png" alt="Hg17 hg18.intronSize.png" width="896" height="384" /></a>
            </p>
            
            <p>
              <a href="http://genomewiki.ucsc.edu/index.php/File:Mm8_mm9.intronSize.png"><img src="http://genomewiki.ucsc.edu/images/0/0f/Mm8_mm9.intronSize.png" alt="Mm8 mm9.intronSize.png" width="896" height="384" /></a>
            </p>
            
            <h2>
              Methods
            </h2>
            
            <ul>
              <li>
                From the table browser, request three different bed files for the knownGenes track:
              </li>
            </ul>
            
            <ol>
              <li>
                whole gene
              </li>
              <li>
                exons only
              </li>
              <li>
                introns only
              </li>
            </ol>
            
            <ul>
              <li>
                From those bed files, stats can be extracted
              </li>
            </ul>
            
            <ol>
              <li>
                gene count from: &#8216;wc -l wholeGene.bed&#8217;
              </li>
              <li>
                exon count stats from:
              </li>
            </ol>
            
            <pre> STATS=`ave -col=10 wholeGene.bed -tableOut | grep -v "^#"`
 MIN=`echo $STATS | cut -d' ' -f1`
 MAX=`echo $STATS | cut -d' ' -f5`
 MEAN=`echo $STATS | cut -d' ' -f6 | awk '{printf "%d", $1+0.5}'`
 COUNT=`echo $STATS | cut -d' ' -f8 | awk '{printf "%d", $1}'`</pre>
            
            <ul>
              <li>
                for exon or intron size stats:
              </li>
            </ul>
            
            <pre> STATS=`awk '{print $3-$2}' {introns,exons}.bed \
      | ave -col=1 stdin -tableOut | grep -v "^#"`
 MIN=`echo $STATS | cut -d' ' -f1`
 MAX=`echo $STATS | cut -d' ' -f5 | awk '{printf "%d", $1}'`
 MEAN=`echo $STATS | cut -d' ' -f6 | awk '{printf "%d", $1+0.5}'`
 SUM_SIZE=`awk '{sum += $3-$2} END{printf "%d", sum}' {introns,exons}.bed`</pre>
            
            <ul>
              <li>
                top five exon count genes
              </li>
            </ul>
            
            <pre>sort -k10nr wholeGene.bed | head -5</pre>
            
            <ul>
              <li>
                top five CDS size genes
              </li>
            </ul>
            
            <pre>awk '{cdsSize=$8-$7
if (cdsSize &gt; 0) {printf "%s\t%s\t%s\t%s\t%d\n", $1,$2,$3,$4,cdsSize}
}' wholeGene.bed | sort -k5nr | head -5</pre>
            
            <ul>
              <li>
                top five smallest transcript genes
              </li>
            </ul>
            
            <pre>awk '{size=$3-$2
if (size &gt; 0) {printf "%s\t%s\t%s\t%s\t%d\n", $1,$2,$3,$4,size}
}' wholeGene.bed | sort -k5n | head -5</pre></div>