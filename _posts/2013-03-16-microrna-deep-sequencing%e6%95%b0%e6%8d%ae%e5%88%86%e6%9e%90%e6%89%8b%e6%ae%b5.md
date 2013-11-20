---
title: microRNA deep-sequencing数据分析手段
author: 悟道
layout: post
permalink: /?p=2993
categories:
  - seq
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<div id="post-2888">
  <h1>
    <a title="microRNA deep-sequencing数据分析手段" href="http://pgfe.umassmed.edu/ou/archives/2888" rel="bookmark">microRNA deep-sequencing数据分析手段 </a>
  </h1>
  
  <div>
    14 九 2012   | <a href="http://pgfe.umassmed.edu/ou/archives/category/it">程序员</a>Tags: <a href="http://pgfe.umassmed.edu/ou/archives/tag/bioinformatics" rel="tag">生物信息学</a> · <a href="http://pgfe.umassmed.edu/ou/archives/tag/application" rel="tag">软件</a>
  </div>
  
  <div>
    <p>
      什么是microRNA呢？MicroRNAs(miRNAs)是在真核生物中长约20-22个碱基的对基因表达起负调控作用的RNA分子。它对于发育，细胞分化，分形，凋亡，染色体结构及病毒抗性都起着极其重要的作用。
    </p>
    
    <p>
      最近也有研究表明在原核生物及病毒中也发现了类似机制的RNA。
    </p>
    
    <p>
      microRNA是高度保守的。受这些高度保守的RNAs调控的基因比例非常高，约占基因组中1-5%的预测基因，10%（多的可至30%）的已知蛋白编码基因受到miRNAs的调控。
    </p>
    
    <p>
      miRNAs的工作机制如下图所示：<br /> <a href="http://pgfe.umassmed.edu/ou/wp-content/uploads/2012/09/image003.png"><img title="miRNAs调控机制。He, L. and Hannon, G.J. 2004. MicroRNAs: small RNAs with a big role in gene regulation.Nat Rev Genet. 5(7):522-31." alt="" src="http://pgfe.umassmed.edu/ou/wp-content/uploads/2012/09/image003-560x637.png" width="560" height="637" /></a><br /> miRNA分子是从核内的较大的转录子剪切而来。首先会被剪切成一个带发卡环的前体（hairpin precursors）。之后在两种RNaseIII内切酶（RNase III endonucleases）（Drosha和Dicer）的作用下切出发卡环的两段尾巴（发卡环的双链部分，长约～22碱基）以及发卡环本身。两段尾巴 此时并未解链，被称为miRNA复合体（duplex）。解链后和目标DNA链结合的那段miRNA被称为成熟miRNA（mature miRNA），与之（不完全）互补另一段RNA被称为星型miRNA(miRNA*)。成熟miRNA与被调控单元形成RNA诱导的沉默复合体（RNA- induced silencing complex, RISC）对目标RNA起负调控作用。需要注意的是mature miRNA和miRNA*并不一定完全互补，下图显示的就是第一个在线虫中发现的miRNA的前体。<br /> <a href="http://pgfe.umassmed.edu/ou/wp-content/uploads/2012/09/image001.png"><img title="lin-4的前体结构及成熟miRNA序列，He, L. and Hannon, G.J. 2004. MicroRNAs: small RNAs with a big role in gene regulation.Nat Rev Genet. 5(7):522-31." alt="" src="http://pgfe.umassmed.edu/ou/wp-content/uploads/2012/09/image001-560x177.png" width="560" height="177" /></a>
    </p>
    
    <p>
      随着第二代测序技术(next-generation sequencing (NGS))的发展，人们开发了很多用于microRNAs深度测序分析的软件。这其中包括：
    </p>
    
    <ul>
      <li>
        mireap: http://sourceforge.net/mailarchive/forum.php?forum_name=mireap-user
      </li>
      <li>
        miRDeep: Friedlander,M.R., Chen,W., Adamidi,C., Maaskola,J., Einspanier,R., Knespel,S. and Rajewsky,N. (2008) Discovering microRNAs from deep sequencing data using miRDeep. Nat. Biotechnol., 26, 407–415.
      </li>
      <li>
        miRanalyzer: Hackenberg,M., Sturm,M., Langenberger,D., Falcon-Perez,J.M. and Aransay,A.M. (2009) miRanalyzer: a microRNA detection and analysis tool for next-generation sequencing experiments. Nucleic Acids Res., 37, W68–W76.
      </li>
      <li>
        miRExpress: Wang,W.C., Lin,F.M., Chang,W.C., Lin,K.Y., Huang,H.D. and Lin,N.S. (2009) miRExpress: analyzing high-throughput sequencing data for proﬁling microRNA expression. BMC Bioinformatics, 10, 328.
      </li>
      <li>
        miRTRAP: Hendrix,D., Levine,M. and Shi,W. (2010) miRTRAP, a computational method for the systematic identiﬁcation of miRNAs from high throughput sequencing data. Genome Biol., 11, R39.
      </li>
      <li>
        DSAP: Huang,P.J., Liu,Y.C., Lee,C.C., Lin,W.C., Gan,R.R., Lyu,P.C. and Tang,P. (2010) DSAP: deep-sequencing small RNA analysis pipeline. Nucleic Acids Res., 38, W385–W391.
      </li>
      <li>
        mirTools: Zhu,E., Zhao,F., Xu,G., Hou,H., Zhou,L., Li,X., Sun,Z. and Wu,J. (2010) mirTools: microRNA proﬁling and discovery based on high-throughput sequencing. Nucleic Acids Res., 38, W392–W397.
      </li>
      <li>
        MIReNA: Mathelier,A. and Carbone,A. (2010) MIReNA: ﬁnding microRNAs with high accuracy and no learning at genome scale and from deep sequencing data. Bioinformatics, 26, 2226–2234.
      </li>
      <li>
        miRNAkey: Ronen,R., Gan,I., Modai,S., Sukacheov,A., Dror,G., Halperin,E. and Shomron,N. (2010) miRNAkey: a software for microRNA deep sequencing analysis. Bioinformatics, 26, 2615–2616.
      </li>
    </ul>
    
    <p>
      从历史的角度来讲，所有这些软件的先驱应该是miRDeep和mireap。其中miRDeep更是后面多种软件的基础而被广泛使用。本文出于篇辐的考虑也只介绍两个软件，miRDeep及miRanalyzer.
    </p>
    
    <p>
      miRDeep是用perl写成的，具有跨平台的优势，容易为生物信息工作者使用。但是因为其缺少用户界面而不受普通生物科研人员的喜爱。而 miRanalyzer是具有良好用户界面的服务器端应用，普通生物科研人员可以通过简单易用的几个选项得到较为清晰的分析结果。但是它需要事先将 fastq文件转换成unique sequence count文件。当然这一步转换已经有很多工具可以使用，其实也未必就是难事。
    </p>
    
    <p>
      但是要了解miRNA Deep-sequencing的分析机理，我们还需要深入地从miRDeep谈起。<br /> <a href="http://pgfe.umassmed.edu/ou/wp-content/uploads/2012/09/image0011.png"><img title="miRNA深度测序模型图 Friedlander,M.R., Chen,W., Adamidi,C., Maaskola,J., Einspanier,R., Knespel,S. and Rajewsky,N. (2008) Discovering microRNAs from deep sequencing data using miRDeep. Nat. Biotechnol., 26, 407–415." alt="" src="http://pgfe.umassmed.edu/ou/wp-content/uploads/2012/09/image0011.png" width="518" height="381" /></a><br /> 在收集的总RNA样品中，用于测序的可能会是多种多样的小片段RNA，上图a所示的就是miRNA的深度测序的理想状态，miRNA前体被切割成三段，成 熟miRNA, miRNA*以及发卡环，这时测序的话，会得到多个成熟miRNA的reads，较少量star sequence以及loop的reads，这是因为单链RNA更容易被降解。但是往往实验中是不可能如此理想的，还会有许多miRNA前体被测序，还有 如图中b所示的非miRNA但具有与miRNA类似结构的RNA小分子的干扰。幸运的是这些小分子片段干扰因为缺少保护会如同start sequence及loop一样很少被测序到。由此，我们可以得到假阳性较低的结果。
    </p>
    
    <p>
      <a href="http://pgfe.umassmed.edu/ou/wp-content/uploads/2012/09/image002.png"><img title="miRDeep工作流程" alt="" src="http://pgfe.umassmed.edu/ou/wp-content/uploads/2012/09/image002.png" width="441" height="681" /></a><br /> 在安装miRDeep时，我们需要同时安装
    </p>
    
    <div>
      <table>
        <tr>
          <td>
            <pre>a     bowtie short read aligner (http://bowtie-bio.sourceforge.net/index.shtml)
b     Vienna package with RNAfold (http://www.tbi.univie.ac.at/~ivo/RNA/)
c.i   SQUID library (http://selab.janelia.org/software.html) goto Squid and download it
c.ii  randfold (http://bioinformatics.psb.ugent.be/software/details/Randfold)
d     Perl package PDF::API2 (http://search.cpan.org/search?query=PDF%3A%3AAPI2&mode=all)</pre>
          </td>
        </tr>
      </table>
    </div>
    
    <p>
      miRDeep首先使用mapper.pl将fastq文件转换成它所需要的格式，其中hg19为bowtie主页上下载的index文件, 0hr.fastq为需要分析的文件。
    </p>
    
    <div>
      <table>
        <tr>
          <td>
            <pre>mapper.pl 0hr.fastq -e -h -i -j -l 18 -m -p hg19 -s reads_collapsed.fa -t reads_collapsed_vs_genome.arf -v -n</pre>
          </td>
        </tr>
      </table>
    </div>
    
    <p>
      而后使用quantifier.pl来分析样品的质量。这里的hsa_precursors.fa及hsa_mature.fa是从<a href="http://www.mirbase.org/" target="_blank">miRBase上下载</a>而来。
    </p>
    
    <div>
      <table>
        <tr>
          <td>
            <pre>quantifier.pl -p hsa_precursors.fa -m hsa_mature.fa -r reads_collapsed.fa -y now -t hsa</pre>
          </td>
        </tr>
      </table>
    </div>
    
    <p>
      之后需要将rna模板库转换成dna
    </p>
    
    <div>
      <table>
        <tr>
          <td>
            <pre>rna2dna.pl hsa_precursors.fa &gt;  hsa_precursors.rna2dna.fa
rna2dna.pl hsa_mature.fa &gt;  hsa_mature.rna2dna.fa</pre>
          </td>
        </tr>
      </table>
    </div>
    
    <p>
      最后使用miRDeep2.pl分析数据。其中hg19.fa是从<a href="http://hgdownload.soe.ucsc.edu/downloads.html" target="_blank">UCSC下载</a>而来。
    </p>
    
    <div>
      <table>
        <tr>
          <td>
            <pre>miRDeep2.pl reads_collapsed.fa hg19.fa reads_collapsed_vs_genome.arf hsa_mature.rna2dna.fa none hsa_precursors.rna2dna.fa -t Human -q expression_analyses/expression_analyses_now/miRBase.mrd 2&gt;report.log</pre>
          </td>
        </tr>
      </table>
    </div>
    
    <p>
      至此我们就可以得到结果了。我们需要注意的是，有一些counts很高的unique sequence并不一定会在结果中，有以下几种可能：<br /> 1，污染<br /> 2，miRDeep会抛弃在基因组上有超过5个比对匹配结果的序列<br /> 3，RNAfold预测的结构不符合标准的miRNA前体<br /> 4，其它。
    </p>
    
    <p>
      题外话，在本文的写作过程中，阅读了一些文献，发现许多关于miRDeep的文献在讲述其机理时会有诸多谬误。所以本文在讲述的过程中都列有最初的参考文献，以避免因本人能力不足而误导了读者。
    </p>
    
    <p>
      转载：http://pgfe.umassmed.edu/ou/archives/2888
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <span><span>microRNA测序的深度一般在10M Reads。</span></span><span><span>关于microRNA的测序的背景知识参见：<br /> </span></span><span><span>illumina NGS的microRNA预测相关的文献 </span></span><span><span><a href="http://seq.cn/3518-50820" target="_blank">http://seq.cn/3518-<span style="text-decoration: underline;"><span style="color: #336699;">50820</span></span></a>;<br /> </span></span><span><span>第20120823期集结号&#8211;microRNA测序概述及实验分析流程 </span></span><span><span><a href="http://seq.cn/3042-50820" target="_blank">http://seq.cn/3042-<span style="text-decoration: underline;"><span style="color: #336699;">50820</span></span></a>;<br /> </span></span><span><span>关于microRNA的命名规则 </span></span><span><span><a href="http://seq.cn/1828-50820" target="_blank">http://seq.cn/1828-50820</a></span></span><span><span> 等</span></span>
    </p>
    
    <p>
      <span><span>这里<strong><span style="color: red;">我拿我分析过的一批microRNA的数据，来详述microRNA的分析过程</span></strong>：</span></span>
    </p>
    
    <p>
      <span><span>microRNA测序数分析选用软件<strong><span style="color: red;">miRDeep</span></strong>，关于这个软件，有文章：</span></span><br /> <span><span>Discovering microRNAs from deep sequencing data using miRDeep</span></span><br /> <span><span>Nature Biotechnology 26, 407 &#8211; 415 (2008)  </span></span><br /> <span><span>引用次数：251次</span></span><br /> <span><span>链接：</span></span><span><span>http://www.nature.com/nbt/journal/v26/n4/abs/nbt1394.html</span></span>
    </p>
    
    <p>
      <span><span>分析流程如下：</span></span>
    </p>
    
    <p>
      <span><span><span style="color: red;"><strong>第一步 去接头！（</strong></span>如果你的测序数据是等长的，远大于microRNA的长度18~26的话，那肯定没去过接头）</span></span>
    </p>
    
    <div id="highlighter_426098">
      <div>
        <a href="http://seq.cn/#">?</a>
      </div>
      
      <table border="0" cellspacing="0" cellpadding="0">
        <tr>
          <td>
            <div>
              1
            </div>
          </td>
          
          <td>
            <div>
              <div>
                <code>mapper.pl $</code><code>file</code>  <code>-d -h -i -j -k $adapter -l 18 -m -s $</code><code>file</code><code>.collapsed</code>
              </div>
            </div>
          </td>
        </tr>
      </table>
    </div>
    
    <p>
      <span><span><strong><span style="color: red;">第二步 回贴</span></strong>  将去过接头的reads回贴回参考基因组</span></span>
    </p>
    
    <div>
      <div id="highlighter_67101">
        <div>
          <a href="http://seq.cn/#">?</a>
        </div>
        
        <table border="0" cellspacing="0" cellpadding="0">
          <tr>
            <td>
              <div>
                1
              </div>
            </td>
            
            <td>
              <div>
                <div>
                  <code>mapper.pl $</code><code>file</code><code>.collapsed -c -p $genome  -t $</code><code>file</code><code>.aln</code>
                </div>
              </div>
            </td>
          </tr>
        </table>
      </div>
    </div>
    
    <p>
      <span><span><span></p> <p>
        <span style="color: red;"><strong>第三步 鉴定miRNA  </strong></span><span style="color: black;">已知的miRNA或是新的miRNA都会被出来，而且表达量也会报出<br /> </span></span></span></span>
      </p>
      
      <div>
        <div id="highlighter_311606">
          <div>
            <a href="http://seq.cn/#">?</a>
          </div>
          
          <table border="0" cellspacing="0" cellpadding="0">
            <tr>
              <td>
                <div>
                  1
                </div>
              </td>
              
              <td>
                <div>
                  <div>
                    <code>miRDeep2.pl $</code><code>file</code><code>.collapsed $genome.fa $</code><code>file</code><code>.aln $mature.fa $homology.mature.fa $pre.fa -t $species.name -c 2&gt;$</code><code>file</code><code>.report.log</code>
                  </div>
                </div>
              </td>
            </tr>
          </table>
        </div>
      </div>
      
      <p>
        <span><span><span></p> <p>
          <span style="color: red;"><strong>第四步  如果你有一个miRNA的集合 先跳过第三步直接做定量的话<br /> </strong></span></span></span></span>
        </p>
        
        <div>
          <div id="highlighter_261592">
            <div>
              <a href="http://seq.cn/#">?</a>
            </div>
            
            <table border="0" cellspacing="0" cellpadding="0">
              <tr>
                <td>
                  <div>
                    1
                  </div>
                </td>
                
                <td>
                  <div>
                    <div>
                      <code>quantifier.pl -p $pre.fa -m $mature.fa. -r $</code><code>file</code><code>.collapsed -U &</code>
                    </div>
                  </div>
                </td>
              </tr>
            </table>
          </div>
        </div></div> </div>