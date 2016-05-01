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
	- [cytoscape APP install](/images/cytoscape/cytoscape_app_install.png)

#### Simple cytoscape usage

A toy data (saved in toy.txt)

```
SUPERIOR	SUBORDINATE	edge	
Dean	Vice dean1	1
Dean	Vice dean2	1
Vice dean1	DirectorA	1
Vice dean2	DirectorB	1
Vice dean1	DirectorC	1
Vice dean1	DirectorD	1
DirectorA	T1	1
DirectorA	T2	1
DirectorB	T3	1
DirectorB	T4	1
DirectorB	T5	1
```

The toy network

![toy network](/images/cytoscape/cytoscape_toy.png)

The video tutorial

{::nomarkdown}
<iframe width="800" src="//www.ehbio.com/video/ehbio_cytoscape_toy.mp4"  frameborder="0" allowfullscreen></iframe>
{:/nomarkdown}

#### More cytoscape operations

* jjj

{::nomarkdown}
<iframe width="800" src="//www.ehbio.com/video/ehbio_cytoscape_toy.mp4"  frameborder="0" allowfullscreen></iframe>
{:/nomarkdown}

{::nomarkdown}
<iframe width="800" src="//www.ehbio.com/video/ehbio_cytoscape_toy.mp4"  frameborder="0" allowfullscreen></iframe>
{:/nomarkdown}

#### Cytoscape mapping gene expression to KEGG pathway

* Time-series expression profile 
#### Import a table to construct network

* "Import" - "Network" - "File" - A network is constructed.
* "Tools" - “"NetworkAnalyzer" - "Network Analysis" - "Analyze network" - The attribute of the network is analyzed. The analyzing result can be used to set the visulization of nodes and edges.

#### Layout

Attribute Circle Layout is my favorite algorithm to show networks especially when you select some nodes.
This algorithm can put nodes with same values together when you are performing 'Attribute Circle Layout' by the related attributes. 
For example, I have two classes of genes, one is upregulated, the other is downregulated. 
This information is saved in a two columns file with the first column containing gene names and 
the second column named 'expr' containing 0 (down-regulated) and 1 (up-regulated). 
This file can be imported into Cytoscape by "File-Import-Table". 
Following one can select all these genes and perform 'Attribute Circle Layout' by 'expr'.

#### Select nodes

"Select"-"Nodes"-"From ID list file" (working in Cytoscape 3.1.1)

#### Color specific nodes

* Contruct a at-least two columns file to represent nodes and their attributes. Make sure the attribute columns have unique names to facilitate selection.
* Import this attribute file as "Node Table Column" through "FIle" - "Import" - "Table".
* Set node color by given attributes using given column names.
*
*
