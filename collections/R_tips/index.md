---
title: R tips
author: ct
layout: page
---


### 记录无法归类的小问题及解决方法

1. 查看R函数代码

   * 如果是R的内部函数，直接输入函数名字，即可查看函数的代码

     ```r
     > colMeans
     function (x, na.rm = FALSE, dims = 1L) 
     {
         if (is.data.frame(x)) 
             x <- as.matrix(x)
         if (!is.array(x) || length(dn <- dim(x)) < 2L) 
             stop("'x' must be an array of at least two dimensions")
         if (dims < 1L || dims > length(dn) - 1L) 
             stop("invalid 'dims'")
         n <- prod(dn[id <- seq_len(dims)])
         dn <- dn[-id]
         z <- if (is.complex(x)) 
             .Internal(colMeans(Re(x), n, prod(dn), na.rm)) + (0+1i) * 
                 .Internal(colMeans(Im(x), n, prod(dn), na.rm))
         else .Internal(colMeans(x, n, prod(dn), na.rm))
         if (length(dn) > 1L) {
             dim(z) <- dn
             dimnames(z) <- dimnames(x)[-id]
         }
         else names(z) <- dimnames(x)[[dims + 1L]]
         z
     }
     <bytecode: 0x2122250>
     <environment: namespace:base>
     ```

   * 如果是S4函数，则需要使用`getMethod(function_name, package_name)`
     
     ```r
     > showMethods('MeanVarPlot')
     Function: MeanVarPlot (package Seurat)
     object="seurat"
    
     > getMethod("MeanVarPlot", "seurat")
     Method Definition:
    
     function (object, fxn.x = expMean, fxn.y = logVarDivMean, do.plot = TRUE, 
    		set.var.genes = TRUE, do.text = TRUE, x.low.cutoff = 0.1, 
    		x.high.cutoff = 8, y.cutoff = 1, y.high.cutoff = Inf, cex.use = 0.5, 
    		cex.text.use = 0.5, do.spike = FALSE, pch.use = 16, col.use = "black", 
    		spike.col.use = "red", plot.both = FALSE)
     ```
2. sapply usage

   ```r
   > a <- as.data.frame(matrix(rnorm(30), ncol=3))
   > a
              V1           V2            V3
   1   1.1678261  0.535765512 -0.0002789383
   2   1.4408018  0.006156163 -0.8926204461
   3  -0.7577270 -0.252982299  0.7633047153
   4  -0.6555118 -0.940734927  0.5586641498
   5   1.6814423  0.536600480  0.0965808879
   6  -1.5529560 -1.491656309 -0.1404898216
   7  -0.2791699 -0.405854634 -0.6891447979
   8  -0.5111633  1.071639283  0.4492834514
   9  -0.0406343  0.243810629  0.9092924868
   10 -1.4827207 -0.333623245 -0.2155860373
   > a$Group = c(rep('A',5), rep('B',5))
   > a
              V1           V2            V3 Group
   1   1.1678261  0.535765512 -0.0002789383     A
   2   1.4408018  0.006156163 -0.8926204461     A
   3  -0.7577270 -0.252982299  0.7633047153     A
   4  -0.6555118 -0.940734927  0.5586641498     A
   5   1.6814423  0.536600480  0.0965808879     A
   6  -1.5529560 -1.491656309 -0.1404898216     B
   7  -0.2791699 -0.405854634 -0.6891447979     B
   8  -0.5111633  1.071639283  0.4492834514     B
   9  -0.0406343  0.243810629  0.9092924868     B
   10 -1.4827207 -0.333623245 -0.2155860373     B
   > my_function <- function(x) { 
   +     A <- x[a$Group=="A"]
   +     B <- x[a$Group=="B"]
   +     t.test(A, B)$p.value
   + }

   > sapply(X=a[,!(names(a) %in% c("Group"))], FUN=my_function, simplify = T)
          V1        V2        V3 
   0.0675659 0.7597376 0.9180267 
   > t.test(a$V1[1:5],a$V1[6:10])$p.value
   [1] 0.0675659

   ```

3. Automatically install packages if not exist

   ```r
   usePackage <- function(p) {
       if (!is.element(p, installed.packages()[,1]))
           install.packages(p, dep = TRUE)
    	   require(p, character.only = TRUE)
   }
   ```


4. Sometimes when you found the lines reading by `read.table` smaller than real line number, please check it you have `""` or `''` in your file.

   ```r
   ### Always set no quote
   a <- read.table(file, sep="\t",  header=T, row.names=1, quote="")
   ```

5. Read in data from string rather than files

   ```r
   string="a\tb\tc
   d\te\tf
   g\th\ti"
   
   data  <- read.table(text=string, sep="\t")
   ```

6. 使用Aggregate进行分组计算

   Aggregate by one column of dataframe.

   ```r
   > ID <- c("a", "b", "c", "b", "c", "d", "e")
   > A <- c(1:7)
   > B <- c(3:9)
   > C <- c(9:3)
   > test <- data.frame(ID, A, B, C)
   > test
     ID A B C
   1  a 1 3 9
   2  b 2 4 8
   3  c 3 5 7
   4  b 4 6 6
   5  c 5 7 5
   6  d 6 8 4
   7  e 7 9 3
   > a = aggregate(test[2:4], by=test[1], FUN=mean)
   > a
     ID A B C
   1  a 1 3 9
   2  b 3 5 7
   3  c 4 6 6
   4  d 6 8 4
   5  e 7 9 3
   ```
   
   Aggregate by an external variable

   ```r
   > a <- "ID;Grp
   A.1;A
   A.2;A
   A.3;A
   B.3;B
   B.4;B
   C.1;C
   B.1;B
   B.2;B
   C.2;C"
   > 
   > b <- "ID;A.1;A.2;A.3;B.1;B.2;B.3;B.4;C.1;C.2
   a;1;2;3;8;2;3;4;4;2
   b;1;3;3;1;3;3;4;1;2
   c;2;4;3;1;5;3;6;2;2"
   > 
   > sampFile <- read.table(text=a, sep=';', row.names=1, header=T)
   > 
   > mat <- read.table(text=b, sep=';', header=T,row.names=1)
   > mat_t <- t(mat)
   > mat_t
       a b c
   A.1 1 1 2
   A.2 2 3 4
   A.3 3 3 3
   B.1 8 1 1
   B.2 2 3 5
   B.3 3 3 3
   B.4 4 4 6
   C.1 4 1 2
   C.2 2 2 2
   > 
   > Grp <- sampFile[match(rownames(mat_t), rownames(sampFile)),1]
   >
   > #The variable given to `by` in `aggregate` must be a list 
   > mat_mean <- aggregate(mat_t, by=list(Grp=Grp), FUN=mean)
   > 
   > mat_mean_grp <- mat_mean$Grp
   > 
   > mat_mean_final <- do.call(rbind, mat_mean)[-1,]
   > 
   > colnames(mat_mean_final) <- mat_mean_grp
   > 
   > mat_mean_final
            A    B   C
   a 2.000000 4.25 3.0
   b 2.333333 2.75 1.5
   c 3.000000 3.75 2.0
   ```

7. 条件填充数据表

   ```r
   > A <- c(1:9)
   > B <- c(11:5,13,14)
   > C <- c(9:1)
   > test <- data.frame(A, B, C)
   > test
     A  B C
   1 1 11 9
   2 2 10 8
   3 3  9 7
   4 4  8 6
   5 5  7 5
   6 6  6 4
   7 7  5 3
   8 8 13 2
   9 9 14 1
   > lod_generate3 <- function(x){
   +   for(i in 2:length(x)){
   +     if(x[i]<x[1])
   +       x[i] <- round(runif(1,min=0,max=x[1]))
   +   }
   +   x
   + }
   > apply(test, 2, lod_generate3)
         A  B C
    [1,] 1 11 9
    [2,] 2  9 6
    [3,] 3  9 7
    [4,] 4  2 8
    [5,] 5  9 6
    [6,] 6 10 2
    [7,] 7  7 7
    [8,] 8 13 2
    [9,] 9 14 5
   ```

8. 每一列的数除以该列的总和 

   ```r
   > a <- data.frame('a'=c(1,2,3,4),'b'=c(1,2,3,4),'d'=2:5)
   > a
     a b d
   1 1 1 2
   2 2 2 3
   3 3 3 4
   4 4 4 5
   > colSums(a)
    a  b  d 
   10 10 14 
   > a/colSums(a) #Wrong
             a         b         d
   1 0.1000000 0.1000000 0.1428571
   2 0.2000000 0.1428571 0.3000000
   3 0.2142857 0.3000000 0.4000000
   4 0.4000000 0.4000000 0.3571429
   > t(a)/colSums(a) #Half-right
          [,1]      [,2]      [,3]      [,4]
   a 0.1000000 0.2000000 0.3000000 0.4000000
   b 0.1000000 0.2000000 0.3000000 0.4000000
   d 0.1428571 0.2142857 0.2857143 0.3571429
   > t(t(a)/colSums(a)) #Right
          a   b         d
   [1,] 0.1 0.1 0.1428571
   [2,] 0.2 0.2 0.2142857
   [3,] 0.3 0.3 0.2857143
   [4,] 0.4 0.4 0.3571429
   ```

9. 取出共同的列 

   ```r
   > a <- data.frame('a'=1:5,'b'=2:6,'c'=round(runif(5,min=0, max=2)),'d'=sample(1:10,5))
   > a
     a b c d
   1 1 2 2 6
   2 2 3 2 8
   3 3 4 1 1
   4 4 5 1 2
   5 5 6 2 4
   > b = data.frame('b'=round(rnorm(5, mean=50, sd=10)),'e'=rep(1,5),'d'=round(runif(5,min=0, max=10)),'c'=sample(1:10,5, replace=T))
   > b
      b e d c
   1 33 1 5 7
   2 62 1 8 6
   3 26 1 8 1
   4 63 1 8 6
   5 43 1 9 4
   > ?match(x, y)
   # Select elements existed in x for each in y and ordered as in x
   # Remove elements only existed in y
   > b[,na.omit(match(colnames(a),colnames(b)))]
      b c d
   1 33 7 5
   2 62 6 8
   3 26 1 8
   4 63 6 8
   5 43 4 9
   ```

10. pairwise.t.test for a matrix

    ```r
    > data = data.frame(Group=c(rep('a',20),rep('b',20),rep('c',20)), A=runif(60, min=0, max=60), B=c(sample(1:10,20,replace=T), sample(20:30,20,replace=T), c(sample(1:30,20, replace=T))))
    > data
       Group          A  B
    1      a  8.3522445  6
    2      a 22.9813777  4
    3      a 11.5574241  8
    4      a 57.5316085  6
    5      a 20.2775717  2
    .	  . .           .
    .	  . .           .
    21     b 36.8333789 25
    22     b 23.5413342 24
    23     b 41.6235628 26
    24     b 27.5968927 25
    25     b 48.6045175 20
    .	  . .           .
    .	  . .           .
    58     c 51.0684425 30
    59     c  4.0294234 27
    60     c 22.6168908 27
    > my_function <- function(x) {
    +     pvalue_m = pairwise.t.test(x, data$Group, pool.sd = F)$p.value
    +     pvalue_m <- as.data.frame(pvalue_m)
    +     pvalue_m$id <- rownames(pvalue_m)
    +     pvalue_m <- melt(pvalue_m, id.vars=c('id'))
    +     name_combine = paste(pvalue_m$id, pvalue_m$variable,sep='.vs.')
    +     pvalue_m <- as.data.frame(pvalue_m$value)
    +     rownames(pvalue_m) <- name_combine
    +     pvalue_m
    +     #colnames(pvalue_m)[colnames(pvalue_m)=="value"] = name_col
    +     #x
    + }
    > p.value <- apply(X=data[,-1], 2,FUN=my_function)
    > p.value <- do.call(cbind, p.value)
    > colnames(p.value) <- colnames(data[,-1])
    > t(p.value)
            b.vs.a      c.vs.a b.vs.b       c.vs.b
    A 8.670387e-01 0.454526764     NA 0.4545267642
    B 3.111305e-22 0.008677007     NA 0.0001068359
    ```

11. t.test & pairwise.t.test [ref](http://stackoverflow.com/questions/11454521/r-t-test-and-pairwise-t-test-give-different-results)

    The problem is not in the p-value correction,  but in the (declaration of the) variance assumptions. You have used var.equal=T in your t.test calls and pooled.sd=FALSE in your paired.t.test calls. However,  the argument for paired.t.test is pool.sd,  not pooled.sd. Changing this gives p-values equivalent to the individual calls to t.test
    ```r
    pairwise.t.test(df$freq,  df$class,  p.adjust.method="none" ,  
    						paired=FALSE,  pool.sd=FALSE)
    ```

12. Several ggplot pic together

    ![Several ggplot pic together]({{ site.img_url }}/heatmap-t-1-1.png "Several ggplot pic together")

    ```r
    data <- c(1:6,6:1,6:1,1:6, (6:1)/10,(1:6)/10,(1:6)/10,(6:1)/10,2:7,7:2,6:1,1:6, 6:1,1:6,3:8,7:2)
    data <- as.data.frame(matrix(data, ncol=12, byrow=T))
    data$type <- c(rep("Gene Expression",2), rep("DNA methylation",2), rep("H3K4me3",2), rep("H3K27me3",2))
    colnames(data) <- c("Zygote","2_cell","4_cell","8_cell","Morula","ICM","ESC","4 week PGC","7 week PGC","10 week PGC","17 week PGC", "OOcyte", "type")
    data$ID <- rep(c("gene1","gene2"),4)
    library(reshape2)
    library(ggplot2)
    data_m <- melt(data, id.vars=c("type","ID"))
    data_m$type <- factor(data_m$type, levels=c("Gene Expression", "DNA methylation", "H3K4me3","H3K27me3"))

    library(gridExtra)
    out <- by(data=data_m, INDICES=data_m$type, FUN=function(m) {
    	m <- droplevels(m)
    	p <- ggplot(m, aes(x=variable,y=ID)) + xlab(NULL) + 
    	     labs(title=levels(m$type))  + theme_bw()  + 
    		 theme(panel.grid.major = element_blank()) + theme(legend.key=element_blank()) + 
    		 theme(axis.text.x=element_text(angle=45,hjust=1, vjust=1)) + 
    		 theme(legend.position="right") + geom_tile(aes(fill=value)) + 
    		 scale_fill_gradient(low = "white", high = "red")
        }
    )
    do.call(grid.arrange,c(out, ncol=1))
    ```
    
    ```r
    grid_plot = function(m, hline){
      ID = unique(m$Metabolites)
      coords = hline[[ID]]$coord
      text = hline[[ID]]$text
      p <- ggplot(m, aes(x=Samples, y=Concentration, color=Year, group=Year))
      p <- p + geom_line(size=1, alpha=0.6) + labs(title=ID) + theme(legend.position = "right") + expand_limits(y=0)+ theme(axis.text.x=element_text(angle=45,hjust=1, vjust=1)) + geom_hline(yintercept = coords, linetype="dotted", size=0.5) + annotate("text", y=coords, x=0, label=text, vjust=0, hjust=0)
    }
    
    hline = list(H1=list(coord=c(5000), text=c(5000)), Glu=list(coord=c(50), text=c(50)), Arg..Arg.Orn.=list(coord=c(0.5), text=c(0.5)))
    
    out <- by(data=ctrl.m, INDICES=ctrl.m$Metabolites, FUN=grid_plot,hline)
    do.call(grid.arrange,c(out, ncol=1))
    ```

13. 查看R包的版本 `installed.packages()[c("SC3"), c("Package", "Version")]`
    
    移除安装包 `remove.packages(c('package_name'))`

    去加载已经加载的包 `detach("package:package_name")`

14. 判断一个变量是否存在

    ```r
    if(exists("debug")){
      debug=FALSE
    } else {
      debug=TRUE
    }
    ```

15. stop and warn

    ```r
    warning("output a message after a function finishes")
    stop("stops the execution of the function and outputs an error message")
    ```

16. Extract all numeric columns
 
    ```r
    new_df <- df[sapply(df, is.numeric)]
    ```

17. r-studio usages

    ```r
    rstudio-server start/stop/restart
    ps -u user | grep 'rsession' # Kill this process when rstuido-server becomes unresponsive
    ```

18. merge dataframes

    ```r
    library(data.table)
    merge(a, b, all.x=T)
    ```

    ```r
    a <- "ID;Grp
    A.1;A
    A.2;A
    A.3;A
    B.3;B
    B.4;B
    C.1;C
    B.1;B
    B.2;B
    C.2;C"
    
    b <- "ID;A.1;A.2;A.3;B.1;B.2;B.3;B.4;C.1;C.2
    a;1;2;3;8;2;3;4;4;2
    b;1;3;3;1;3;3;4;1;2
    c;2;4;3;1;5;3;6;2;2"
    
    sampFile <- read.table(text=a, sep=';', row.names=1, header=T)
    
    mat <- read.table(text=b, sep=';', header=T,row.names=1)
    mat_t <- t(mat)
    mat_t
    > c = merge(sampFile, mat_t, by=0)
	> #c = merge(sampFile, mat_t, by="row.names")  #Both work
    > c
      Row.names Grp a b c
    1       A.1   A 1 1 1
    2       A.2   A 2 2 2
    3       A.3   A 3 3 3
    4       B.1   B 1 1 1
    5       B.2   B 2 2 2
    6       B.3   B 3 3 3
    7       B.4   B 4 4 4
    8       C.1   C 1 1 1
    9       C.2   C 2 2 2
    > c = dataframe(c[,-1], row.names=c[,1])
    > c
        Grp a b c
    A.1   A 1 1 1
    A.2   A 2 2 2
    A.3   A 3 3 3
    B.1   B 1 1 1
    B.2   B 2 2 2
    B.3   B 3 3 3
    B.4   B 4 4 4
    C.1   C 1 1 1
    C.2   C 2 2 2
    ```

19. strsplit

    ```r
    sample <- c("a_samp1_1", "a_samp1_2", "a_samp1_3", "a_samp2_1", "a_samp2_2", "a_samp2_3")
    # 把样品名字按 <_> 分割，取出其第二部分作为样品的组名
    # lapply(X,  FUC) 对列表或向量中每个元素执行FUC操作，FUNC为自定义或R自带的函数
    ## One better way to generate group
    group <- unlist(lapply(strsplit(sample, "_" ), function(x) x[2]))
    ```

20. Multiple rows or columns legend

    ```r
    gg+guides(fill=guide_legend(nrow=2, byrow=TRUE))
    gg+guides(fill=guide_legend(ncol=2))
    ```

21. 条件替换数据表

    ```r
    > a <- data.frame(a=1:4,b=1:4,c=1:4)
    > a
      a b c
    1 1 1 1
    2 2 2 2
    3 3 3 3
    4 4 4 4
    > a[a$b<3,"b"] <- 3
    > a
      a b c
    1 1 3 1
    2 2 3 2
    3 3 3 3
    4 4 4 4
    > a <- within(a, a[a<4] <- 2)
    > a
      a b c
    1 2 3 1
    2 2 3 2
    3 2 3 3
    4 4 4 4
    ```

30. Batch effects [ref](https://support.bioconductor.org/p/60581/)

    In a literal sense,  getting a matrix of batch corrected counts is not possible. Once the batch effects have been removed,  the values will no longer be counts.

    To batch correct, it is necessary to first transform the counts to a pseudo-continuous scale. Then you can use batch correction methods developed for microarrays. This is how we usually do it.
    
    First,put the counts in a DGEList object:
    
    ```r
    library(edgeR)
    y <- DGEList(counts=counts)
    ```
        
    Filter non-expressed genes:
    
    ```r
    A <- aveLogCPM(y)
    y2 <- y2[A>1,]
    ```
    
    Then normalize and compute log2 counts-per-million with an offset:
    
    ```r
    y2 <- calcNormFactors(y2)
    logCPM <- cpm(y2, log=TRUE, prior.count=5)
    ```
    
    Then remove batch correct:
    
    ```r
    logCPMc <- removeBatchEffect(y2, batch)
    ```
    
    Here batch is a vector or factor taking a different value for each batch group. You can input two batch vectors.
    
    Now you can cluster the samples, for example by:
    
    ```r
    plotMDS(logCPMc)
    ```
    
    Variations on this would be use `rpkm()` instead of `cpm()`, or to give `removeBatchEffect()` a design matrix of known groups that are not batch effects.



**Reference**

* http://rfunction.com/archives/1377

