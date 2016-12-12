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

