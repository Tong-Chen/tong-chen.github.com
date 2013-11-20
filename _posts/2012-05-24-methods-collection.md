---
title: Methods collection
author: 悟道
layout: post
permalink: /?p=2113
categories:
  - bioinformatics
tags:
  - bioinformatics
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.LC microarray,Heatmap,PCA

MicroRNA microarray normalization and data analysis  
Microarray normalization removes system-related varia-  
tions, such as sample amount variations, different label-  
ing dyes, and signal gain differences of scanners so that

biological variations can be faithfully revealed. Data were  
analyzed by i rst subtracting the background and then  
normalizing the signals using a LOWESS i lter (locally  
weighted regression) [2]. Background is determined using a  
regression-based background mapping method. The regres-  
sion is performed on 5% to 25% of the lowest intensity data  
points excluding blank spots. Raw data matrix is then sub-  
tracted by the background matrix. Data adjustment includes  
data i ltering, Log2 transformation, and gene centering,  
and normalization. The data i ltering removes miRNAs  
with normalized intensity values below a threshold value  
of 32 across all samples. Gene centering and normalization  
transform the Log2 values using the mean and the standard  
deviation of individual genes across all samples. t Values are  
calculated for each miRNA between groups, and P values  
are computed from the theoretical t-distribution. miRNAs  
with P values below a critical P-value (typically 0.01) are  
selected for cluster analysis. The clustering was done using  
hierarchical methods, with average linkage and Euclidean  
distance metrices [3]. The clustering plot was generated  
using TIGR MeV (Multiple Experimental Viewer) software  
from The Institute for Genomic Research. Principal compo-  
nent analysis was performed using the R statistical pack-  
age (cran.r-project.org) (Fig. 3A,B). For Figure 3A, in order  
to accurately represent the distances between samples in  
principal component space, the loading of the samples along  
each principal component was scaled (multiplied) by the  
standard deviation along that component.

<http://online.liebertpub.com/doi/abs/10.1089/scd.2008.0247>

[comparison of normalization methods for high density oligonu-cleotide array data based on variance and bias]

&nbsp;

&nbsp;

http://www.stat.berkeley.edu/users/statlabs/index.html