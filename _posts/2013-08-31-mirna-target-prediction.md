---
title: miRNA target prediction
author: 悟道
layout: post
categories:
  - bioinformatics
---

1. miRanda

The mirSVR score provided at mircrorna.org is the best tool for making predictions, as it utilizes the most recent miRanda prediction rules such as seed-site pairing, site context, free-energy, and conservation. I would recommend a mirSVR cutoff of <= -1.2. This value represents the top 5% of miRSVR scores, where the expected probability of observing a log expression change of <=.5 is ~50%, or of <=0.1 is 70%. The authors of the SVR score also suggest conservation as merely another factor to consider when determining the overall confidence of the prediction, and not as an absolute cut off.

Also if you are using miRanda locally on your own sequences, the generally recommended values for pairing score is >150 and energy score < -7. However, others have used the more stringent values of a pairing score of >155 and an energy score of < -20. I&#8217;m hoping soon they will release an updated miranda algorithm that provides local calculation of mirSVR scores.

This reference describes how the mirSVR score was put together: Betel, D., Koppal, A., Agius, P., Sander, C. Leslie, C, et al. (2010) Comprehensive modeling of microRNA targets predicts functional non-conserved and non-canonical sites. Genome Biol, 11, R90.

[<http://www.biostars.org/p/5998/>]

&nbsp;
