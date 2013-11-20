---
title: INDEPENDENT SAMPLES t TEST
author: 悟道
layout: post
permalink: /?p=3049
categories:
  - sta
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<p align="center">
  <b><span style="font-size: small;">INDEPENDENT SAMPLES t TEST</span></b>
</p>

* * *

**Syntax**

The syntax for the t.test( ) function is outlined in the [Single Sample t Test][1] tutorial.

* * *

**The t Test With Two Independent Groups**

As part of his senior research project in the Fall semester of 2001, Scott Keats looked for a possible relationship between marijuana smoking and a deficit in performance on a task measuring short term memory&#8211;the digit span task from the Wechsler Adult Intelligence Scale. Two groups of ten subjects were tested. One group, the &#8220;nonsmokers,&#8221; claimed not to smoke marijuana. A second group, the &#8220;smokers,&#8221; claimed to smoke marijuana regularly. The data set is small and easily entered by hand&#8230;

<pre><span style="font-family: courier;">&gt; nonsmokers = c(18,22,21,17,20,17,23,20,22,21)
&gt; smokers = c(16,20,14,21,20,18,13,15,17,21)</span></pre>

The values of the response variable indicate number of items completely successfully on the digit span task. An examination of the distributions would be in order at this point, as the t-test assumes sampling from normal parent populations&#8230;

<pre>&gt; plot(density(nonsmokers))            # output not shown
&gt; plot(density(smokers))               # output not shown</pre>

The smoothed distributions appear reasonably mound-shaped, although with samples this small, it&#8217;s hard to say for sure what the parent distribution looks like. Another way to examine the data graphically is with side-by-side boxplots&#8230;

<pre>&gt; boxplot(nonsmokers,smokers,ylab="Scores on Digit Span Task",
+         names=c("nonsmokers","smokers"),
+         main="Digit Span Performance by\n Smoking Status")</pre>

Note: The &#8220;\n&#8221; inside the main title causes it to be printed on two lines. I&#8217;m not entirely sure this will work in Windows, but it should. <img alt="Boxplots" src="http://ww2.coastal.edu/kingw/statistics/R-tutorials/images/marijuana.png" width="508" height="477" align="left" />

Boxplots are becoming the standard graphical method of displaying this sort of data, although I have an issue with the fact that boxplots are median oriented graphics, while the t-test is comparing means. We could also do a bar graph with error bars (which requires some finagling), and I will discuss this is a future tutorial, but the bar graph would display less information about the data. Meanwhile, the boxplots show the nonsmokers to have done better on the digit span task than the smokers. It also shows an absence of outliers, which is good news.

Of course, the standard numerical summaries could also be done&#8230;

<pre><span style="font-family: courier;">&gt; mean(nonsmokers)
[1] 20.1
&gt; sd(nonsmokers)
[1] 2.131770
&gt; mean(smokers)
[1] 17.5
&gt; sd(smokers)
[1] 2.953341</span></pre>

If you want standard errors, there is no built-in function (we will write one later), but they are easily enough calculated&#8230;

<pre>&gt; sqrt(var(nonsmokers)/length(nonsmokers))
[1] 0.674125
&gt; sqrt(var(smokers)/length(smokers))
[1] 0.9339284</pre>

There is little left to do but the statistical test.

The t-test can be done either by entering the names of the two groups (or two numerical vectors) into the t.test( ) function, or by using a formula interface if the data are in a data frame (below)&#8230;

<pre><span style="font-family: courier;">&gt; t.test(nonsmokers,smokers)

	Welch Two Sample t-test

data:  nonsmokers and smokers 
t = 2.2573, df = 16.376, p-value = 0.03798
alternative hypothesis: true difference in means is not equal to 0 
95 percent confidence interval:
 0.1628205 5.0371795 
sample estimates:
mean of x mean of y 
     20.1      17.5</span></pre>

By default the two-tailed test is done, and the Welch correction for nonhomogeneity of variance is applied. Both of these options can easily enough be changed&#8230;

<pre>&gt; t.test(nonsmokers,smokers,alternative="greater",var.equal=T)

	Two Sample t-test

data:  nonsmokers and smokers 
t = 2.2573, df = 18, p-value = 0.01833
alternative hypothesis: true difference in means is greater than 0 
95 percent confidence interval:
 0.6026879       Inf 
sample estimates:
mean of x mean of y 
     20.1      17.5</pre>

The output also includes a 95% CI (change this using &#8220;conf.level=&#8221;) for the difference between the means and the sample means. Note that the t.test( ) function always subtracts first group minus second group. Since the &#8220;nonsmokers&#8221; were entered first into the function, and our hypothesis was that they would score higher on the digit span test, this dictated the alternative hypothesis to be &#8220;difference between means is greater than zero.&#8221; The null hypothesized difference can also be changed by setting the &#8220;mu=&#8221; option.

* * *

**The Formula Interface**

I hope you haven&#8217;t erased those vectors, because now we are going to make a data frame from them&#8230;

<pre><span style="font-family: courier;">&gt; scores = c(nonsmokers,smokers)
&gt; groups = c("nonsmokers","smokers")   # Make sure these are in the right order!
&gt; groups = rep(groups,c(10,10))
&gt; mj.data = data.frame(groups,scores)
&gt; mj.data
       groups scores
1  nonsmokers     18
2  nonsmokers     22
3  nonsmokers     21
4  nonsmokers     17
5  nonsmokers     20
6  nonsmokers     17
7  nonsmokers     23
8  nonsmokers     20
9  nonsmokers     22
10 nonsmokers     21
11    smokers     16
12    smokers     20
13    smokers     14
14    smokers     21
15    smokers     20
16    smokers     18
17    smokers     13
18    smokers     15
19    smokers     17
20    smokers     21
&gt; rm(scores,groups)                    # Why is this necessary?
&gt; attach(mj.data)</span></pre>

Now for some summary statistics&#8230;

<pre>&gt; by(scores,groups,mean)               # or tapply(scores,groups,mean)
groups: nonsmokers
[1] 20.1
---------------------------------------------------------- 
groups: smokers
[1] 17.5
&gt; by(scores,groups,sd)
groups: nonsmokers
[1] 2.131770
---------------------------------------------------------- 
groups: smokers
[1] 2.953341</pre>

The boxplot function also accepts a formula interface&#8230;

<pre>&gt; boxplot(scores ~ groups)             # output not shown</pre>

Read the formula as &#8220;scores by groups&#8221;. Notice you get group labels on the x-axis this way, too. Finally, the t-test&#8230;

<pre>&gt; t.test(scores ~ groups)

	Welch Two Sample t-test

data:  scores by groups 
t = 2.2573, df = 16.376, p-value = 0.03798
alternative hypothesis: true difference in means is not equal to 0 
95 percent confidence interval:
 0.1628205 5.0371795 
sample estimates:
mean in group nonsmokers    mean in group smokers 
                    20.1                     17.5</pre>

If you don&#8217;t care for attaching data frames (and I usually try to avoid it), the t.test( ) function also has a &#8220;data=&#8221; option&#8230;

<pre>&gt; detach(mj.data)
&gt; t.test(scores ~ groups, data=mj.data)     ### output not shown</pre>

Note: I am told there is an easier way to create a data frame from individual vectors representing group-by-group data, but I haven&#8217;t yet been told what it is. If I find out, I&#8217;ll pass it on!

* * *

**Textbook Problems**

Problems in textbooks often leave out the raw data and just present summary statistics. There is no provision for entering the summary stats into the t.test( ) function, so such problems would have to be calculated at the command prompt&#8230;

<pre><span style="font-family: courier;">       Two groups of ten subjects each were given the digit span subtest from
       the Wechsler Adult Intelligence Scale. One group consisted of regular
       smokers of marijuana, while the other group consisted of nonsmokers.
       Below are summary statistics for number of items completed correctly
       on the digit span task. Is there a significant difference between the
       means of the two groups?

             smokers     nonsmokers
             ----------------------
       mean    17.5         20.1
       sd       2.95         2.13

&gt; mean.diff = 17.5 - 20.1
&gt; df = 10 + 10 - 2
&gt; pooled.var = (2.95^2 * 9 + 2.13^2 * 9) / df
&gt; se.diff = sqrt(pooled.var/10 + pooled.var/10)
&gt; t.obt = mean.diff / se.diff
&gt; t.obt
[1] -2.259640
&gt; p.value = 2*pt(t.obt,df=df)          # two-tailed
&gt; p.value
[1] 0.03648139</span></pre>

A custom function could be written if these calculations had to be done repeatedly, but there is a certain educational value to be had from doing them by hand!

* * *

**Power**

The power.t.test( ) function has the following syntax (from the help page for this function)&#8230;

<pre><span style="font-family: courier;">power.t.test(n = NULL, delta = NULL, sd = 1, sig.level = 0.05, power = NULL,
             type = c("two.sample", "one.sample", "paired"),
             alternative = c("two.sided", "one.sided"),
             strict = FALSE)</span></pre>

Exactly one of the options on the first line should be set to &#8220;NULL&#8221;, and R will then calculate it from the remaining values. Suppose we wanted a power of 85% for the Scott Keats experiment, and were anticipating a mean difference of 2.5 and a pooled standard deviation of 2.6. How many subjects should be used per group if a two-tailed test is planned?

<pre>&gt; power.t.test(delta=2.5, sd=2.6, sig.level=.05, power=.85,
+              type="two.sample", alternative="two.sided")

     Two-sample t test power calculation 

              n = 20.43001
          delta = 2.5
             sd = 2.6
      sig.level = 0.05
          power = 0.85
    alternative = two.sided

 NOTE: n is number in *each* group</pre>

So there you go!

* * *

**Homogeneity of Variance**

The standard, textbook, pooled-variance t-test assumes homogeneity of variance. The easiest way to deal with nonhomogeneity of variance is to allow R to do what it does by default anyway&#8211;run the t-test using the Welch correction for nonhomogeneity. Further discussion of nonhomogeneity of variance will occur in the ANOVA tutorial.

* * *

**Alternatives to the t Test**

If the normality assumption of the t-test is violated, and the sample sizes are two small to heal that via an appeal to the central limit theorem, then a nonparametric alternative test should be sought. The standard alternative to the independent samples t-test is what we old timers were taught to call the Mann-Whitney U test. For some reason, this name is now out of fashion, and the test goes by the name Wilcoxin-Mann-Whitney test, or Wilcoxin rank sum test, or some variant thereof. The syntax is very similar, and it will work with or without the formula interface&#8230;

<pre><span style="font-family: courier;">&gt; wilcox.test(nonsmokers,smokers)

	Wilcoxon rank sum test with continuity correction

data:  nonsmokers and smokers 
W = 76.5, p-value = 0.04715
alternative hypothesis: true location shift is not equal to 0 

Warning message:
In wilcox.test.default(nonsmokers, smokers) :
  cannot compute exact p-value with ties
&gt;
&gt; ### and now the formula interface...
&gt; wilcox.test(scores ~ groups, data=mj.data)

	Wilcoxon rank sum test with continuity correction

data:  scores by groups 
W = 76.5, p-value = 0.04715
alternative hypothesis: true location shift is not equal to 0 

Warning message:
In wilcox.test.default(x = c(18, 22, 21, 17, 20, 17, 23, 20, 22,  :
  cannot compute exact p-value with ties</span></pre>

The test assumes continuous variables without ties (and neither is the case here). And no, I don&#8217;t know why the warning message about that takes two different forms.

http://ww2.coastal.edu/kingw/statistics/R-tutorials/independent-t.html

\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\*****

The other statistical test for boxplot would be Kolmogorov-Smirnov(K-S) test if the groups have unequal amount of numbers.

&nbsp;

 [1]: http://ww2.coastal.edu/kingw/statistics/R-tutorials/singlesample.html