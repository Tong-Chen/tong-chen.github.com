---
title: Simple tutorial for cytoscape usage 
layout: post
categories:
  - Cytoscape
  - letter
tags:
  - Cytoscape
---

#### What is cytoscape

[Cytoscape](http://www.cytoscape.org) is an open source 
software platform for visualizing *molecular
interaction networks* and *biological pathways* and integrating these
networks with annotations, gene expression profiles and other state
data. Although Cytoscape was originally designed for biological
research, now it is a general platform for complex network analysis
and visualization. Cytoscape core distribution provides a basic set
of features for data integration, analysis, and visualization.
Additional features are available as Apps (formerly called Plugins).
Apps are available for network and molecular profiling analyses,
new layouts,  additional file format support,  scripting,  and
connection with databases.   They may be developed by anyone using
the Cytoscape open API based on Java™ technology and App
community development is encouraged. Most of the Apps are freely
available from [Cytoscape App Store](http://apps.cytoscape.org/).

#### How to install cytoscape

* Install [Java](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) if you do not have one.

* Download [cytoscape](http://cytoscape.org/download.php).

* App installation
	- Cytoscape menu bar --> Apps --> App manager --> Browse and install apps.
	- ![cytoscape APP install](/images/cytoscape/cytoscape_app_install.png)

#### Simple cytoscape usage

A toy data (saved in `toy.txt`)

```
SUPERIOR	SUBORDINATE
Dean	Vice dean1
Dean	Vice dean2
Vice dean1	DirectorA
Vice dean2	DirectorB
Vice dean1	DirectorC
Vice dean1	DirectorD
DirectorA	T1
DirectorA	T2
DirectorB	T3
DirectorB	T4
DirectorB	T5
```

The toy network

![toy network](/images/cytoscape/cytoscape_toy.png)

The video tutorial to show how to use `cytoscape` to transfer the text
into a network.

{::nomarkdown}
<embed src="http://player.youku.com/player.php/sid/XMTU1NDU3MzQyNA==/v.swf"
allowFullScreen="true"  quality="high"  width="480"  height="400" align="middle"  allowScriptAccess="always"  type="application/x-shockwave-flash" ></embed>
{:/nomarkdown}

#### More cytoscape operations

##### Node searching, adding, deletion, selection and attribute chaning

* Files needed
	- [RUAL.subset.sif](/images/cytoscape/RUAL.subset.sif): Protein-protein interaction data
	- [RUAL.subset.na](/images/cytoscape/RUAL.subset.na):  The map file between Gene ID and protein name

* The video tutorial

{::nomarkdown}
<embed src="http://player.youku.com/player.php/sid/XMTU1NDgwMDcxMg==/v.swf"
allowFullScreen="true"  quality="high"  width="480"  height="400" 
align="middle" allowScriptAccess="always"  
{:/nomarkdown}

##### Heatmap nodes color using expression data

* Files needed
	- [galFiltered.sif](/images/cytoscape/galFiltered.sif): Protein-protein and protein-DNA interaction data
	- [galExpData.mrna](/images/cytoscape/galExpData.mrna): Gene expression profile in various conditions

* Effect picture
![cytoscape_galfilter.png](/images/cytoscape/cytoscape_galfilter.png)

{::nomarkdown}
<embed src="http://player.youku.com/player.php/sid/XMTU1NDc5OTI1Mg==/v.swf"
allowFullScreen="true"  quality="high"  width="480"  height="400" 
align="middle" allowScriptAccess="always"  

{:/nomarkdown}

#### Cytoscape mapping gene expression to KEGG pathway

* Time-series expression profile within KEGG pathway

![kegg_expression](/images/cytoscape/cytoscape_kegg.png)

* Files needed
	- KEGG pathway xml file, like ko00900.xml
	![ko00900.xml](cytoscape_kegg_xml.png)
	- Expression data for genes involved in ko00900 pathway

* Plugins needed
	- KEGGscape: used to parse XML files of KEGG pathway
	- enhancedGraphics: used to do barPlot and linePlot

* The video tutorial

{::nomarkdown}

<embed src="http://player.youku.com/player.php/sid/XMTU1NDU4NDQ5Mg==/v.swf"
allowFullScreen="true"  quality="high"  width="480"  height="400" 
align="middle" allowScriptAccess="always"  
type="application/x-shockwave-flash" ></embed>

{:/nomarkdown}



{::nomarkdown}
<div id="youkuplayer" style="width:480px;height:400px"></div>
<script type="text/javascript" src="http://player.youku.com/jsapi"></script>
<script type="text/javascript">
player = new YKU.Player('youkuplayer', {
styleid: '0', 
client_id: 'a40cba4210523c08', 
vid: 'XMTU1NDU4NDQ5Mg', 
autoplay: false, 
show_related: false
});
</script>
{:/nomarkdown}

===

#### Import a table to construct network

* "Import" - "Network" - "File" - "Selet a two-column file", then a network is constructed.
* "Tools" - "NetworkAnalyzer" - "Network Analysis" - "Analyze network"
* - The attribute of the network is analyzed. The analyzing result can
* be used to set the visulization styles of nodes and edges.

#### Layout

`Attribute Circle Layout` is my favorite algorithm to show networks especially when you select some nodes.
This algorithm can put nodes with same values together when you are
performing `Attribute Circle Layout` by the related `attributes`. 

For example, I have two classes of genes, one is upregulated, the other is downregulated. 
This information is saved in a two columns file with the first column containing gene names and 
the second column named `expr` containing `0` (down-regulated) and `1` (up-regulated). 
This file can be imported into Cytoscape by "File-Import-Table". 
Following one can select all these genes and perform `Attribute Circle
Layout` by `expr`.

#### Select nodes

"Select"-"Nodes"-"From ID list file" (working in Cytoscape 3.1.1)

#### Color specific nodes

* Contruct a at-least two columns file to represent nodes and their attributes. Make sure the attribute columns have unique names to facilitate selection.
* Import this attribute file as "Node Table Column" through "FIle" - "Import" - "Table".
* Set node color by given attributes using given column names.
