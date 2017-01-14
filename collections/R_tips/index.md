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

9. 
