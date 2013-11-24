---
title: 'Notes for &#8220;computing for data analysis&#8221; [Coursera course]'
author: 悟道
layout: post
categories:
  - R
---

1. colClass.  
Specifying this option instead of using default can make &#8216;read.table&#8217; run MUCH faster, often twice as faster. In order to use this option, you have to know the class of each column in your data frame. If all of the columns are &#8216;numberic&#8217;, for example, then you can just set colClass=&#8221;numeric&#8221;. A quick and dirty way to figure out classes for each column is the following:

<pre class="brush: bash; title: ; notranslate" title="">initial &lt;- read.table("data",nrows=100)
classes &lt;- sapply(initial,class)
tabAll &lt;- read.table("data",colClass=classes)
</pre>

2. &#8230;  
The &#8230; represents argument list when put in the end. All additional parameters will be saved to &#8230; and passed to inner functions.  
The &#8230; argument is also necessary when the number of arguments passed to the functions can not be known in advance like:

<pre class="brush: bash; title: ; notranslate" title="">args(paste)
function (..., sep=" ", collapse=NULL)
</pre>

Once catch with &#8230; is that any arguments that appear after &#8230; on the argument list must be named explicitly and cannot be partially matched.

3.split function

Divide into Groups and Reassemble

> Description:
> 
> ‘split’ divides the data in the vector ‘x’ into the groups defined  
> by ‘f’. The replacement forms replace values corresponding to  
> such a division. ‘unsplit’ reverses the effect of ‘split’.
> 
> Usage:
> 
> split(x, f, drop = FALSE, &#8230;)  
> split(x, f, drop = FALSE, &#8230;) <- value  
> unsplit(value, f, drop = FALSE)

<pre class="brush: bash; title: ; notranslate" title="">&gt; x &lt;- c(rnorm(10), runif(10), rnorm(10,1))
&gt; f &lt;- gl(3,10)
&gt; split(x,f)
$`1`
 [1]  0.04568824  1.43881538  1.20726247  0.89607034 -1.82028884  0.41100988
 [7] -0.89489825 -1.91846889 -1.61372116  1.12882772

$`2`
 [1] 0.82255701 0.71847213 0.58078540 0.72514585 0.02594232 0.93178561
 [7] 0.85934484 0.10371824 0.99216828 0.45048527

$`3`
 [1]  1.1336430  1.4560381  0.5475995  1.9924938 -1.8635712  0.4090884
 [7]  2.0350326 -0.2822986 -0.1865551 -1.1014422

&gt; a &lt;- split(x,f)
&gt; a$1
Error: unexpected numeric constant in "a$1"
&gt; a[1]
$`1`
 [1]  0.04568824  1.43881538  1.20726247  0.89607034 -1.82028884  0.41100988
 [7] -0.89489825 -1.91846889 -1.61372116  1.12882772

&gt; x
 [1]  0.04568824  1.43881538  1.20726247  0.89607034 -1.82028884  0.41100988
 [7] -0.89489825 -1.91846889 -1.61372116  1.12882772  0.82255701  0.71847213
[13]  0.58078540  0.72514585  0.02594232  0.93178561  0.85934484  0.10371824
[19]  0.99216828  0.45048527  1.13364297  1.45603806  0.54759947  1.99249377
[25] -1.86357122  0.40908842  2.03503258 -0.28229863 -0.18655514 -1.10144215
&gt; f
 [1] 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 3 3 3 3 3 3 3 3 3 3
Levels: 1 2 3
</pre>

<pre class="brush: bash; title: ; notranslate" title="">#split by two factors
&gt; f1 &lt;- gl(2,5)
&gt; f2 &lt;- gl(5,2)
&gt; f1
 [1] 1 1 1 1 1 2 2 2 2 2
Levels: 1 2
&gt; f2
 [1] 1 1 2 2 3 3 4 4 5 5
Levels: 1 2 3 4 5
&gt; interaction(f1,f2)
 [1] 1.1 1.1 1.2 1.2 1.3 2.3 2.4 2.4 2.5 2.5
Levels: 1.1 2.1 1.2 2.2 1.3 2.3 1.4 2.4 1.5 2.5
&gt; x &lt;- rnorm(10)
&gt; str(split(x, list(f1,f2)))
List of 10
 $ 1.1: num [1:2] -0.855 -0.852
 $ 2.1: num(0) 
 $ 1.2: num [1:2] -0.629 -0.494
 $ 2.2: num(0) 
 $ 1.3: num -0.0677
 $ 2.3: num -0.296
 $ 1.4: num(0) 
 $ 2.4: num [1:2] 0.403 -0.791
 $ 1.5: num(0) 
 $ 2.5: num [1:2] -1.35 -1.01
&gt; str(split(x, interaction(f1,f2)))
List of 10
 $ 1.1: num [1:2] -0.855 -0.852
 $ 2.1: num(0) 
 $ 1.2: num [1:2] -0.629 -0.494
 $ 2.2: num(0) 
 $ 1.3: num -0.0677
 $ 2.3: num -0.296
 $ 1.4: num(0) 
 $ 2.4: num [1:2] 0.403 -0.791
 $ 1.5: num(0) 
 $ 2.5: num [1:2] -1.35 -1.01
</pre>

4.apply, sapply, tapply, mapply

> apply
> 
> Apply Functions Over Array Margins
> 
> Description:
> 
> Returns a vector or array or list of values obtained by applying a  
> function to margins of an array or matrix.
> 
> Usage:
> 
> apply(X, MARGIN, FUN, &#8230;)
> 
> Arguments:
> 
> X: an array, including a matrix.
> 
> MARGIN: a vector giving the subscripts which the function will be  
> applied over. E.g., for a matrix ‘1’ indicates rows, ‘2’  
> indicates columns, ‘c(1, 2)’ indicates rows and columns.  
> Where ‘X’ has named dimnames, it can be a character vector  
> selecting dimension names. 

<pre class="brush: bash; title: ; notranslate" title="">&gt; x &lt;- c(rnorm(10), runif(10), rnorm(10,1))
&gt; y &lt;- matrix(x,nrow=3)
&gt; y
           [,1]       [,2]       [,3]      [,4]       [,5]      [,6]      [,7]
[1,] 0.04568824  0.8960703 -0.8948982 1.1288277 0.58078540 0.9317856 0.9921683
[2,] 1.43881538 -1.8202888 -1.9184689 0.8225570 0.72514585 0.8593448 0.4504853
[3,] 1.20726247  0.4110099 -1.6137212 0.7184721 0.02594232 0.1037182 1.1336430
          [,8]       [,9]      [,10]
[1,] 1.4560381 -1.8635712 -0.2822986
[2,] 0.5475995  0.4090884 -0.1865551
[3,] 1.9924938  2.0350326 -1.1014422
&gt; apply(y,1,mean)
[1] 0.2990596 0.1327723 0.4912411
</pre>

> tapply
> 
> Apply a Function Over a Ragged Array
> 
> Description:
> 
> Apply a function to each cell of a ragged array, that is to each  
> (non-empty) group of values given by a unique combination of the  
> levels of certain factors.
> 
> Usage:
> 
> tapply(X, INDEX, FUN = NULL, &#8230;, simplify = TRUE)
> 
> Arguments:
> 
> X: an atomic object, typically a vector.
> 
> INDEX: list of one or more factors, each of same length as ‘X’. The  
> elements are coerced to factors by ‘as.factor’. 

<pre class="brush: bash; title: ; notranslate" title="">&gt; x &lt;- c(rnorm(10), runif(10), rnorm(10,1))
&gt; f &lt;- gl(3,10)
&gt; tapply(x,f,range)
$`1`
[1] -1.918469  1.438815

$`2`
[1] 0.02594232 0.99216828

$`3`
[1] -1.863571  2.035033
</pre>

> Apply a Function to Multiple List or Vector Arguments
> 
> Description:
> 
> ‘mapply’ is a multivariate version of ‘sapply’. ‘mapply’ applies  
> ‘FUN’ to the first elements of each &#8230; argument, the second  
> elements, the third elements, and so on. Arguments are recycled  
> if necessary.
> 
> Usage:
> 
> mapply(FUN, &#8230;, MoreArgs = NULL, SIMPLIFY = TRUE,  
> USE.NAMES = TRUE)
> 
> Arguments:
> 
> FUN: function to apply, found via ‘match.fun’.
> 
> &#8230;: arguments to vectorize over (vectors or lists of strictly  
> positive length, or all of zero length). See also ‘Details’.
> 
> MoreArgs: a list of other arguments to ‘FUN’. 

<pre class="brush: bash; title: ; notranslate" title="">&gt; list(rep(1,4), rep(2,3), rep(3,2), rep(4,1))
[[1]]
[1] 1 1 1 1

[[2]]
[1] 2 2 2

[[3]]
[1] 3 3

[[4]]
[1] 4

&gt; mapply(rep,1:4,4:1)
[[1]]
[1] 1 1 1 1

[[2]]
[1] 2 2 2

[[3]]
[1] 3 3

[[4]]
[1] 4

&gt; noise &lt;- function(n, mean, sd) {
+ rnorm(n, mean, sd)
+ }
&gt; noise(5,1,2)
[1]  2.3318087 -0.5513379  2.1479612  3.6134264  2.3675103
&gt; noise(1:5,1:5,2) #wrong usage
[1] 1.1778732 0.3632799 6.2087896 2.9261086 3.5094597
&gt; mapply(noise,1:5,1:5,2)
[[1]]
[1] -0.1760846

[[2]]
[1] -0.7810509 -1.4659350

[[3]]
[1] 3.0684418 0.7133993 4.5190991

[[4]]
[1] 1.946463 3.025599 2.906996 5.319200

[[5]]
[1] 5.443579 5.280245 2.844177 4.538039 6.393585

&gt; list(noise(1,1,2), noise(2,2,2), noise(3,3,2), noise(4,4,2), noise(5,5,2))
[[1]]
[1] 1.524288

[[2]]
[1] 1.547129 5.261838

[[3]]
[1] 3.150581 4.107338 2.906161

[[4]]
[1] 3.280658 2.605533 3.905065 5.884222

[[5]]
[1] 5.200394 5.541272 4.189657 5.596289 5.019267
</pre>

5.interaction

> Compute Factor Interactions
> 
> Description:
> 
> ‘interaction’ computes a factor which represents the interaction  
> of the given factors. The result of ‘interaction’ is always  
> unordered.
> 
> Usage:
> 
> interaction(&#8230;, drop = FALSE, sep = &#8220;.&#8221;, lex.order = FALSE)

<pre class="brush: bash; title: ; notranslate" title="">&gt; f1 &lt;- gl(2,5)
&gt; f2 &lt;- gl(5,2)
&gt; f1
 [1] 1 1 1 1 1 2 2 2 2 2
Levels: 1 2
&gt; f2
 [1] 1 1 2 2 3 3 4 4 5 5
Levels: 1 2 3 4 5
&gt; interaction(f1,f2)
 [1] 1.1 1.1 1.2 1.2 1.3 2.3 2.4 2.4 2.5 2.5
Levels: 1.1 2.1 1.2 2.2 1.3 2.3 1.4 2.4 1.5 2.5
</pre>

6.plot

<pre class="brush: bash; title: ; notranslate" title="">#plot two types of points in a scatter plot
&gt; x &lt;- rnorm(100)
&gt; str(x)
 num [1:100] 1.128 -1.144 0.523 1.179 -0.602 ...
&gt; y &lt;- x + rnorm(100)
&gt; str(y)
 num [1:100] 1.814 -2.452 0.271 1.844 -1.471 ...
&gt; g &lt;- gl(2,50, labels=c("Male", "Female"))
&gt; str(g)
 Factor w/ 2 levels "Male","Female": 1 1 1 1 1 1 1 1 1 1 ...
&gt; plot(x, y, type="n")
&gt; points(x[g=="Male"], y[g=="Male"], col="green")
&gt; points(x[g=="Female"], y[g=="Female"], col="blue")
&gt; 

</pre>
