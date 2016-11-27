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
     
     ```
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
2. 
