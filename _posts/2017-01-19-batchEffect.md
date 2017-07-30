
Just to be clear,  there's an important difference between removing a batch effect and modelling a batch effect. Including the batch in your design formula will model the batch effect in the regression step,  which means that the raw data are not modified (so the batch effect is not removed),  but instead the regression will estimate the size of the batch effect and subtract it out when performing all other tests. In addition,  the model's residual degrees of freedom will be reduced appropriately to reflect the fact that some degrees of freedom were " spent"  modelling the batch effects. This is the preferred approach for any method that is capable of using it (this includes DESeq2). You would only remove the batch effect (e.g. using limma's removeBatchEffect function) if you were going to do some kind of downstream analysis that can't model the batch effects,  such as training a classifier.

add the known batches to the design formula. (And if the batches are not known,  they can be estimated using the sva or RUVseq packages.)

In the DESeq2 vignette,  we recommend putting 'condition' at the end of the design,  so you can use results() without extra arguments (although you can extract any results you like using the arguments).

Similarly,  in edgeR,  it doesn't really matter for GLM fitting or dispersion estimation whether batch is put at the start or end. The only thing that will change is the interpretation of the coefficients,  and the coef or contrast you need to supply to glmLRT. Keeping batch at the start just makes it convenient as the last coefficient will represent the treatment effect. The last coefficient is dropped by default in glmLRT,  so you don't need any extra arguments to do the DE test of interest.


Answers to your first 2 questions:

Yes,  if you have a known batch effect,  you should include it in your design formula.
Normalization happens before any kind of batch effect adjustment or removal,  so there is no problem here.
Additionally,  I don't think you need sva here. The purpose of sva is to discover hidden batch effects in the data,  and represent them as " surrogate variables"  that you can insert into your design in lieu of the real hidden variables. However,  you already know about your batch effect and can include it directly in the design. Hypothetically,  if someone had given you this data set and told you " this was done in several batches,  but I didn't record which samples went in which batches" ,  then you might want to try sva to partially recover the batch information from the data itself. Similarly,  if you suspect that there are additional confounding factors other than the runs,  then sva will help you discover those as well.

Also,  whenever I use sva with DESeq2,  my preference would be to run it on regularized log CPM as calculated by the rlog function. This should reduce the contribution of noise in low-count genes.

I meant that my preference was to use rlog and then pass the resulting normalized,  regularized logCPM values to sva instead of svaseq. (As far as I can tell,  the only difference between the sva and svaseq functions is the log transform in svaseq.



```
https://support.bioconductor.org/p/59195/
library(edgeR)
dge <- DGEList(counts=count)
dge <- calcNormFactors(dge)
logCPM <- cpm(dge, log=TRUE, prior.count=5)
plotMDS(logCPM)
# normalize the data before using removeBatchEffect(),  and quantile is one possibility.
logCPM <- removeBatchEffect(logCPM, batch=batch)
plotMDS(logCPM, col=as.numeric(batch))
```

### References

* https://support.bioconductor.org/p/76099/
* <http://www.bioconductor.org/help/workflows/rnaseqGene/#batch>
* https://support.bioconductor.org/p/86493/

