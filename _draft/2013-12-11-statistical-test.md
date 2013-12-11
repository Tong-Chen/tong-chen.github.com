If you entered data with two rows and two columns, you must choose the chi-square test or Fisher's exact test.

Chi-square and Yates correction

In the days before computers were readily available, people analyzed contingency tables by hand, or using a calculator, using chi-square tests. This test works by computing the expected values for each cell if the relative risk (or odds' ratio) were 1.0. It then combines the discrepancies between observed and expected values into a chi-square statistic from which a P value is computed.

The chi-square test is only an approximation. The Yates continuity correction is designed to make the chi-square approximation better, but it over corrects so gives a P value that is too large (too 'conservative'). With large sample sizes, Yates' correction makes little difference, and the chi-square test works very well. With small sample sizes, chi-square is not accurate, with or without Yates' correction. Statisticians seem to disagree on whether or not to use Yates correction. Prism gives you the choice.

If the observed and expected values are all very close (within 0.25), the Yates correction sort of works backwards, and actually increases the value of chi-square and thus lowers the P value, rather than decreasing chi-square and increasing P. This is a rare occurrence, and only happens when the relative risk or odds ratio is very close to 1.0. If you asked for the Yates correction, Prism does the Yates correction even in this case.

Fisher's test. Exactly correct answer to wrong question?

Fisher's exact test, as its name implies, always gives an exact P value and works fine with small sample sizes. Fisher's test (unlike chi-square) is very hard to calculate by hand, but is easy to compute with a computer. Most statistical books advise using it instead of chi-square test.  If you choose Fisher's test, but your values are huge, Prism will override your choice and compute the chi-square test instead, which is very accurate with large values.

As its name implies, Fisher's exact test, gives an exactly correct answer no matter what sample size you use. But some statisticians conclude that Fisher's test gives the exact answer to the wrong question, so its result is also an approximation to the answer you really want. The problem is that the Fisher's test is based on assuming that the row and column totals are fixed by the experiment. In fact, the row totals (but not the column totals) are fixed by the design of a prospective study or an experiment, the column totals (but not the row totals) are fixed by the design of a retrospective case-control study, and only the overall N (but neither row or column totals) is fixed in a cross-sectional experiment. Ludbrook (1) points out that Fisher designed his exact test to analyze a unique experiment, and that experimental design is extremely rare.

Since the design of your study design is extremely unlikely to match the constraints of Fisher's test, you could question whether the exact P value produced by Fisher's test actually answers the question you had in mind.

An alternative to Fisher's test is the Barnard test. Fisher's test is said to be 'conditional' on the row and column totals, while Barnard's test is not. Mehta and Senchaudhuri explain the difference and why Barnard's test has more power (2). Berger modified this test to one that is easier to calculate yet more powerful.  Ludbrook discusses other exact methods that are appropriate to common experimental designs (1).

At this time, we do not plan to implement Bernard's or Berger's test in Prism or the exact tests mentioned by Ludbrook (1). There certainly does not seem to be any consensus that these tests are preferred. But let us know if you would like to see these tests in a future version of Prism. Here is an online calculator that performs Berger's test.

http://graphpad.com/guides/prism/6/statistics/index.htm?stat_chi-square_or_fishers_test.htm

http://www.r-statistics.com/2010/02/barnards-exact-test-a-powerful-alternative-for-fishers-exact-test-implemented-in-r/
