---
title: Tutorial for boxplot
layout: post
categories:
  - scripts
  - pic
  - ggplot2
  - R
tags:
  - tutorial
  - pic
  - ggplot2
  - R
---
#### Box-plot and violin plot

These words were typed according to [`wikipedia`](http://wikipedia.org) to let me know the concepts and descriptions. One can totally skip this part.

In descriptive statistics, a box plot or boxplot is a convenient way of graphically depicting groups of numerical data through their quartiles. Box plots may also have lines extending vertically from the boxes (whiskers) indicating variability outside the upper and lower quantiles, hence the terms box-and-whisker plot and box-and-whisker diagram. Outliers may be plooted as individual points.

Box plots display differences between populations without making any assumptions of the underlying statistical distribution: they are non-parametric. The spacings between the different parts of the box help indicate the degree of dispersion (spread) and skewness in the data, and identify outliers. In addition to the points themselves, they allow one to visually estimate various L-estimators, notably the interquartile range, midhinge, range, mid-range, and trimean. Boxplots can be drawn either horizontally or vertically. [Wiki](http://en.wikipedia.org/wiki/Box_plot)

Violin plots are a method of plotting numeric data. A violin plot is a combination of a box plot and a kernel density plot. Specifically, it starts woth a box plot. It then adds a rotared kernel density plot to each side of the boxplot.

The violoin plots is similar to box plots, except that they show the prbability density of the data ad different values (in the simplest case this could be a hitogram). Typically violin plots will include a marker for the median of the data and a box indicaiting the interquantile range, as in standard box plots. Oberlaid on this box plot is a kernel density estimation. [Wiki](http://en.wikipedia.org/wiki/Violin_plot)


![boxplot-norm-distribution wiki](http://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Boxplot_vs_PDF.svg/550px-Boxplot_vs_PDF.svg.png)
![violin-plot wiki](http://upload.wikimedia.org/wikipedia/commons/thumb/e/eb/Violinplot-hiv-paper-plot-pathogens.png/320px-Violinplot-hiv-paper-plot-pathogens.png)

#### How-to do the plot

Here I will introduce a script `boxplot.sh` as one-line command to plot various box-plots on given data.

##### Input file format

Two types of input file are supported. If each boxplot contains the same number of points, the first format may be suitable. If each box contains different number of points, you may use the sceond format.

* Matrix data table like `diamonds` as described in [Basic things you should know to use s-plot]({{ site.url }}/2013/01/test-data-sets/).

  The first column is the ID variable, normally the values in this column should be unqiue. The other columns are data columns and you can have any number of columns if you want. 
  {% highlight r %}
  #filename diamond.extract.matrix 
  ID  carat       cut color price
  1  0.23     Ideal     E 0.326
  2  0.21   Premium     E 0.326
  3  0.23      Good     E 0.327
  4  0.29   Premium     I 0.334
  5  0.31      Good     J 0.335
  6  0.24 Very Good     J 0.336
  {% endhighlight %}

* A melted format as in described in [Basic things you should know to use s-plot]({{ site.baseurl }}/2013/01/test-data-sets/).

  {% highlight r %}
       cut color variable value
     Ideal     E    carat  0.23
   Premium     E    carat  0.21
      Good     E    carat  0.23
   Premium     I    carat  0.29
      Good     J    carat  0.31
 Very Good     J    carat  0.24
   Premium     D    price 2.757
     Ideal     D    price 2.757
      Good     D    price 2.757
 Very Good     D    price 2.757
   Premium     H    price 2.757
     Ideal     D    price 2.757
  {% endhighlight %}

##### Begin plotting

* The easiest way `boxplot.sh -f diamond.extract.matrix` or `boxplot.sh -f diamond.extract.matrix.melt -m TRUE` will get the following boxplot.

  ![diamond.extract.matrix.boxplot-simple1]({{ site.img_url }}/tutorial/diamond.extract.matrix.boxplot-simple1.png)

* Also want to get the violin plot, `boxplot.sh -f diamond.extract.matrix`. If you do not want to plot the inner-boxplot, please give `FALSE` to `-W`.

  ![diamond.extract.matrix.boxplot.violin1]({{ site.img_url }}/tutorial/diamond.extract.matrix.boxplot.violin1.png)

* Plot the distribution of `carat` and `price` in each `cut` category,
`boxplot.sh -f diamond.extract.matrix -r 70 -a cut -I "'color'"`; or
in each `color` category `boxplot.sh -f diamond.extract.matrix -r 70
-a color -I "'cut','carat'"`. Remember to exclude other columns if there is
any by giving their names to `-I` in format `"'col1','col2'"` or
`"'col'"`.

  ![diamond.extract.matrix.boxplot.violin1.set]({{ site.img_url}}/tutorial/diamond.extract.matrix.boxplot.violin1.set.png)

* Plot the distribution of `price` in each `cut` category,
`boxplot.sh -f diamond.extract.matrix -r 70 -a cut -I
"'color','carat'"`; or
in each `color` category `boxplot.sh -f diamond.extract.matrix -r 70
-a color -I "'cut','carat'"`. Remember to exclude other columns if there is
any by giving their names to `-I` in format `"'col1','col2'"` or
`"'col'"`.

  ![diamond.extract.matrix.boxplot.price_color]({{ site.img_url}}/tutorial/diamond.extract.matrix.boxplot.price_color.png)


* Plot the distribution of `price` in different `carat` categories, 
`boxplot.sh -f diamond.extract.matrix -a carat -I "'cut','color'"  -B 4 -x 'carat' -y 'price'`
or 
` boxplot.sh -f diamond.extract.matrix -a carat -I "'cut','color'" -B "c(0.1,0.4,0.7,1,6)"  -x 'carat' -y 'price'`

  ![diamond.extract.matrix.boxplot.price_carat_num]({{ site.img_url}}/tutorial/diamond.extract.matrix.boxplot.price_carat_num.png)
  ![diamond.extract.matrix.boxplot.price_carat_interval]({{ site.img_url}}/tutorial/diamond.extract.matrix.boxplot.price_carat_interval.png)


