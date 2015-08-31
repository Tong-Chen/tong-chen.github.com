---
title: Record of cytoscape usage 
layout: post
categories:
  - Cytoscape
  - letter
tags:
  - Cytoscape
---

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
