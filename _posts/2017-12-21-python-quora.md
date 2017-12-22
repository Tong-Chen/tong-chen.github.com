---
title: 一个月学会Python的Quora指南和资料放送
author: ct
layout: post
categories:
  - Python
tags:
  - Python
  - Bioinfo
---

如何一个月学会使用Python

文章翻译自Quora上的回帖，略有改动。原文链接：<https://www.quora.com/What-are-the-best-tips-for-learning-Python-within-one-month>

### 第1周

谷歌搜索“Python programming fundamentals” (Python编程基础)，选择一个较好的网站，并针对其中的教程部分进行阅读和练习。这需要一周**每天8小时**的学习和练习来加强你的理解。记住：不要死记句法规则，每当你需要某个句法并使用时，会自然而然地记住。不过，最开始，多看几遍也不为过。**书读多遍，其义自见。**

如果不想搜索，我们在[小学生都学Python了，你还不知道怎么开始](http://mp.weixin.qq.com/s/1JlAROpOCBwaG574EwvkVw)提供了不少教程。而且还有自写的[Python系列简明教程](https://mp.weixin.qq.com/s/9BNrq8Lu7hjtO2BAKOIXOA)，精简版。可以作为小册子读用。

语法查找的话有Python cookbook,这里有中文翻译版本<http://python3-cookbook.readthedocs.io/zh_CN/latest/preface.html> (书中的所有源代码也可在此书的前言页面获取)。


### 第2、3、3.5 周

选择一个课题并试着完成它。

有以下建议：

1. 不要想的太多，选择一个基础的项目，或者google搜索“beginner python projects” (新手python课题)。[Python生信练习题](http://mp.weixin.qq.com/s/478DiO0RdO9zEGSZ0NzsiA)。

2. 不必记住句法规则，当遇到困难时上网搜索便可得到提示。

3. 使用IDE (Integrated Development Environment) (可以更简单的debug以及运行程序)。如PyCharm、Jupyter notebook。

4. 将项目拆分为几个小的部分。

   例如如果你要做一个计算器，那么：

   （1）先设想界面，在深入到各个按钮。
   
   （2）将加减乘除等功能放入到相应按钮中。

5. 可以借助Stackoverflow等网站。请在**理解内容**的基础上进行复制粘贴。

6. 这个过程会比较艰辛，需要有毅力来强迫自己解决遇到的问题。

   当遇到难题时：
   
   （1）使用搜索引擎，注意输入更明确的搜索字段。

   （2）如果不没能搜索出答案，可以把问题放到论坛上去。[如何提问](https://mp.weixin.qq.com/s/xCif04bqZB14Z4OvesK0SQ)

7. 编程时适当休息，转换心情。

8. 花时间学一下版本控制 (version control) 的基础，推荐git这个网站。

9. 慢慢学习如何**debug**。个人认为最好的debug，是**打印出程序运行的关键过程**，查看每一步是否符合预期。

10. 在编写程序前，确保自己已经有了实际理论解决方案。可以事先笔头画出问题的解决方案流程。
11. 编写完程序后，试着花几个小时来测试并从中改进学习。**在一个小问题上，不断拓展，就可以深入。**
12. 当一个难题解决不了时，不要气馁。先去做别的部分，再返回来重新思考。

### 第3.5/4 周

首先保证程序没有**运行BUG**，然后再看有没有**结果BUG**。

如果你还没有完成此项目：

（1）给自己更多的时间。

（2）优先处理重要的编程部分。

恭喜你，对于只是通过读tutorial学习python却收获甚少的人来说，你已经超越他们了，或许比1、2年级的CS本课程还要领先。

之后可以通过学习数据库的工作原理以及python构架来提高自己的手法。

学习的过程大部分是程序写作和调试，想不想有个后盾呢？

<http://www.ehbio.com/Training>

回复中推荐的网络资源比较多，这就不列出来了。因为大部分我也没看过，适不适合初学也不好评价。

今天收到**Coursera**的邮件，列出了**2017年最高评分的系列课程**，计算机系列有三个，都跟Python有关：**Fundamentals of Computing** (编程语言使用Python，前两部分都是关于Python交互式编程), **Algorithms** (Python作为一个必修语言), **Python for Everybody**, 有时间的可以去看看 (<https://www.coursera.org>)。

搜索资料的过程中，不小心发现了这么一个神奇的Github库，里面包含了很多免费，大部分优质的书籍，部分相关的列举如下 (可点击的都是生信宝典之前发过的文章)，读过的付一点心得体会。可直接访问最后的网址跳到原网页，或点击阅读原文，每个链接都可点。

### Awk

* [Linux学习 - 常用和不太常用的实用awk命令](http://mp.weixin.qq.com/s/8wD14FXt7fLDo1BjJyT0ew)
* [A User's Guide for GNU AWK](http://www.math.utah.edu/docs/info/gawk_toc.html)
* [An Awk Primer](https://en.wikibooks.org/wiki/An_Awk_Primer)
* [Awk](http://www.grymoire.com/Unix/Awk.html) - Bruce Barnett
* [awk中文指南](http://awk.readthedocs.org/en/latest/index.html)
* [awk程序设计语言](https://github.com/wuzhouhui/awk)

### Sed

* [Linux学习 - SED操作，awk的姊妹篇](http://mp.weixin.qq.com/s/cywkIeRbhkYTZvkwTeIVSA)
* [Sed - An Introduction and Tutorial](http://www.grymoire.com/Unix/Sed.html)

### Bash

*  [Linux学习-总目录](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484606&idx=1&sn=c5f2654e3ede87f534bc352f286a6357&chksm=ec0dc134db7a48228044e720eff4cc39ea2b9258db7d20faafbcae29a47ef7de334678fad35a#rd)
* [Bash概论 - Linux系列教程补充篇](http://mp.weixin.qq.com/s/lWNp_6W_jLiogmtlk9nO2A)
* [用了Docker，妈妈再也不担心我的软件安装了 - 基础篇](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483840&amp;idx=1&amp;sn=f87f6dd703cd8c109f6dc5b8d12ffb7c&amp;chksm=ec0dc44adb7a4d5c9ff2422c730b1d7bb18dcb6947c0e7449f1678aee492c3193302174930b4#rd)
* [Docker —— 从入门到实践](https://github.com/yeasy/docker_practice)
* [鸟哥的 Linux 私房菜 基础学习篇 (学的人应该比较多，但没读过)](http://cn.linux.vbird.org/linux_basic/linux_basic.php)
* [鸟哥的 Linux 私房菜 服务器架设篇](http://cn.linux.vbird.org/linux_server/)
* [shell-book](http://me.52fhy.com/shell-book/)
* [Shell 编程基础](http://wiki.ubuntu.org.cn/Shell%E7%BC%96%E7%A8%8B%E5%9F%BA%E7%A1%80)
* [Shell 脚本编程30分钟入门](https://github.com/qinjx/30min_guides/blob/master/shell.md)
* [The Linux Command Line 中文版](http://billie66.github.io/TLCL/book/zh)
* [Advanced Bash-Scripting Guide (很不错的书)](http://tldp.org/LDP/abs/html/) - M. Cooper
* [Bash Guide for Beginners](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/) - M. Garrels
* [BASH Programming](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)
* [Bash Reference Manual](http://www.gnu.org/software/bash/manual/bashref.html)

### Vim

* [不用Linux也可以的强大文本处理方法-vimc操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484250&amp;idx=1&am
p;sn=d4759dc05a55643549646c77318c4f96&amp;chksm=ec0dc6d0db7a4fc64791896914547b5ce818e8bd3cca98f0fb7bf6ebd9029fe6fd08a4
d55255#rd)
* [Vim Manual(中文版)](http://man.chinaunix.net/newsoft/vi/doc/help.html)
* [大家來學 VIM](http://www.study-area.org/tips/vim/index.html)
* [A Byte of Vim](http://www.swaroopch.com/notes/vim/)
* [Learn Vim Progressively](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)
* [Learn Vimscript the Hard Way](http://learnvimscriptthehardway.stevelosh.com)
* [Use Vim Like A Pro](https://leanpub.com/VimLikeAPro) - Tim Ottinger
* [Vi Improved -- Vim](http://www.truth.sk/vim/vimbook-OPL.pdf) - Steve Oualline (PDF)
* [Vim Recipes](https://web.archive.org/web/20130302172911/http://vim.runpaint.org/vim-recipes.pdf) (PDF)
* [Vim Regular Expressions 101](http://vimregex.com)

### C

* 个人认为最好的还是The C Programming Language，经典中的经典。
* [A Tutorial on Pointers and Arrays in C](http://home.netcom.com/~tjensen/ptr/pointers.htm) - Ted Jensen [(PDF, Zipped HTML)](http://pweb.netcom.com/~tjensen/ptr/cpoint.htm)
* [Beej's Guide to C Programming](http://beej.us/guide/bgc/) - B. Hall
* [Beej's Guide to Network Programming - Using Internet Sockets](http://beej.us/guide/bgnet/) - B. Hall
* [Build Your Own Lisp](http://www.buildyourownlisp.com)
* [C for Python Programmers - Carl Burch (Python用户可读，比较着学，更有利于提高)](http://www.toves.org/books/cpy/)
* [C Programming](https://en.wikibooks.org/wiki/Programming%3AC) - Wikibooks
* [C Programming Boot Camp - Paul Gribble](http://www.gribblelab.org/CBootCamp/)
* [Deep C](http://www.slideshare.net/olvemaudal/deep-c)
* [Essential C](http://cslibrary.stanford.edu/101/EssentialC.pdf) (PDF)
* [Everything you need to know about pointers in C - Peter Hosey](http://boredzo.org/pointers/)
* [Functional C (1997)](https://research.utwente.nl/files/5128727/book.pdf) - Pieter H. Hartel, Henk Muller (PDF)
* [Learn to Code With C - The MagPi Essentials](https://www.raspberrypi.org/magpi-issues/Essentials_C_v1.pdf) (PDF)
* [Modern C](http://icube-icps.unistra.fr/img_auth.php/d/db/ModernC.pdf) (PDF)


### Markdown

* 应该学习的标记语言，写文档，很方便。
* [Learn Markdown](https://www.gitbook.com/book/gitbookio/markdown/details) - Sammy P., Aaron O. (PDF) (EPUB) (MOBI)
* [Markdown 快速入门](http://wowubuntu.com/markdown/basic.html)
* [Markdown 简明教程](http://www.jianshu.com/p/7bd23251da0a)
* [Markdown 语法说明](http://wowubuntu.com/markdown/)
* [献给写作者的 Markdown 新手指南](http://www.jianshu.com/p/q81RER)

### Octave

* [Octave Programming (Andrew Ng的机器学习课使用的语言，开源版MatLab，学一点当个乐子)](https://en.wikibooks.org/wiki/Octave_Programming_Tutorial)

### Python

* [Python学习极简教程 （一）(我的教程尽快更新到Python3)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483866&amp;idx=1&amp;sn=310
341a1c8d348958c304df03dfd06a0&amp;chksm=ec0dc450db7a4d46e369637cd2867b0e56389bf4f2e1d0dce409bba38882e61e5063308a13af#r
d)
* [Django 1.8 中文文档](http://python.usyiyi.cn/documents/django_182/index.html)
* [Django book 2.0](http://djangobook.py3k.cn/2.0/)
* [Python 3 文档(简体中文) 3.2.2 documentation](http://docspy3zh.readthedocs.org/en/latest/)
* [Python Cookbook第三版](http://python3-cookbook.readthedocs.io/zh_CN/latest/) (作者：David Beazley, Brian K.Jones 翻译：熊能)
* [Python 中文学习大本营](http://www.pythondoc.com)
* [Python之旅](http://funhacks.net/explore-python) (作者：Ethan)
* [Python教程 - 廖雪峰的官方网站](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)
* [像计算机科学家一样思考Python (Downey教授的Think系列书都是不错的，讲解简单清晰)](https://www.ctolib.com/docs/sfile/think-python-2e/0.html) (中英对照版 作者：Allen B. Downey 翻译：大胖哥)
* [深入 Python 3](https://github.com/jiechic/diveintopython3)
* [笨办法学 Python](http://old.sebug.net/paper/books/LearnPythonTheHardWay/)
* [简明 Python 教程 (很方便的小册子)](https://bop.molun.net) (作者：Swaroop C H 译者：沈洁元、漠伦)
* [20 Python Libraries You Aren't Using (But Should)](http://www.oreilly.com/programming/free/20-python-libraries-you-arent-using-but-should.csp) *(Just fill the fields with any values)*
* [A Beginner's Python Tutorial](https://en.wikibooks.org/wiki/A_Beginner%27s_Python_Tutorial)
* [A Byte of Python](https://python.swaroopch.com) (3.x) (HTML, PDF, EPUB, Mobi)
* [A Guide to Python's Magic Methods](https://github.com/RafeKettler/magicmethods) - Rafe Kettler
* [A Whirlwind Tour of Python](http://www.oreilly.com/programming/free/files/a-whirlwind-tour-of-python.pdf) - Jake VanderPlas (PDF) [(EPUB, MOBI)](http://www.oreilly.com/programming/free/a-whirlwind-tour-of-python.csp?download=yes)
* [Automate the Boring Stuff](http://automatetheboringstuff.com/chapter0/) - Al Sweigart
* [Biopython (用到了查查就好)](http://biopython.org/DIST/docs/tutorial/Tutorial.pdf) (PDF)
* [Build applications in Python the antitextbook](http://github.com/thewhitetulip/build-app-with-python-antitextbook) (3.x) (HTML, PDF, EPUB, Mobi)
* [Building Machine Learning Systems with Python](https://www.packtpub.com/packt/free-ebook/python-machine-learning-algorithms) - Willi Richert & Luis Pedro Coelho, Packt. *(Just fill the fields with any values)*
* [Building Skills in Object-Oriented Design (Python)](http://www.itmaybeahack.com/book/oodesign-python-2.1/latex/BuildingSkillsinOODesign.pdf) (PDF) (2.1.1)
* [Building Skills in Python](http://www.itmaybeahack.com/book/python-2.6/latex/BuildingSkillsinPython.pdf) (PDF) (2.6)
* [Code Like a Pythonista: Idiomatic Python](http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html)
* [CodeCademy Python](https://www.codecademy.com/learn/python)
* [Composing Programs](http://composingprograms.com) (3.x)
* [Data Structures and Algorithms in Python](https://web.archive.org/web/20161016153130/http://www.brpreiss.com/books/opus7/html/book.html) - B. R. Preiss (PDF)
* [Dive into Python 3](http://getpython3.com/diveintopython3/) - Mark Pilgrim (3.0)
* [From Python to NumPy](http://www.labri.fr/perso/nrougier/from-python-to-numpy/)
* [Full Stack Python](http://www.fullstackpython.com)
* [Functional Programming in Python](http://www.oreilly.com/programming/free/functional-programming-python.csp) *(Just fill the fields with any values)*
* [Fundamentals of  Python Programming](http://python.cs.southern.edu/pythonbook/pythonbook.pdf) - Richard L. Halterman (PDF) (3.2)
* [Google's Python Style Guide](https://google.github.io/styleguide/pyguide.html)
* [Hacking Secret Cyphers with Python](http://inventwithpython.com/hacking/chapters/) - Al Sweigart (3.3)
* [Hadoop with Python](http://www.oreilly.com/programming/free/hadoop-with-python.csp) *(Just fill the fields with any values)*
* [High Performance Python](http://ianozsvald.com/HighPerformancePythonfromTrainingatEuroPython2011_v0.2.pdf) (PDF)
* [Hitchhiker's Guide to Python!](http://docs.python-guide.org/en/latest/) (2.6)
* [How to Make Mistakes in Python](http://www.oreilly.com/programming/free/files/how-to-make-mistakes-in-python.pdf) - Mike Pirnat (PDF) (1st edition)
* [How to Think Like a Computer Scientist: Learning with Python, Interactive Edition (推荐)](http://interactivepython.org/courselib/static/thinkcspy/index.html) (3.2)
* [Think Python (Think系列)](http://www.greenteapress.com/thinkpython/) - Allen B. Downey (2.x & 3.0)
* [Intermediate Python](http://book.pythontips.com/en/latest/index.html#) - Muhammad Yasoob Ullah Khalid (1st edition)
* [Introduction to Programming with Python](http://opentechschool.github.io/python-beginners/en/) (3.3)
* [Introduction to Python](http://kracekumar.com/post/71171551647/introduction-to-python) - Kracekumar (2.7.3)
* [Learn Python, Break Python](http://learnpythonbreakpython.com)
* [Learn Python in Y minutes](https://learnxinyminutes.com/docs/python/)
* [Learn Python The Hard Way](http://learnpythonthehardway.org/book/) (2.5 - 2.6)
* [Learn to Program Using Python](https://www.ida.liu.se/~732A47/literature/PythonBook.pdf) - Cody Jackson (PDF)
* [Learning Python](https://www.packtpub.com/packt/free-ebook/learning-python) - Fabrizio Romano, Packt. *(Just fill the fields with any values)*
* [Lectures on scientific computing with python](https://github.com/jrjohansson/scientific-python-lectures) - J.R. Johansson (2.7)
* [Modeling Creativity: Case Studies in Python](http://www.clips.ua.ac.be/sites/default/files/modeling-creativity.pdf) - Tom D. De Smedt (PDF)
* [Natural Language Processing with Python](http://www.nltk.org/book/) (3.x)
* [Non-Programmer's Tutorial for Python 3](https://en.wikibooks.org/wiki/Non-Programmer%27s_Tutorial_for_Python_3) (3.3)
* [Python Cookbook](http://chimera.labs.oreilly.com/books/1230000000393/index.html) - David Beazley
* [Python Data Science Handbook](https://github.com/jakevdp/PythonDataScienceHandbook) - Jake VanderPlas (HTML, Jupyter Notebooks)
* [Python for Everybody Exploring Data Using Python 3](http://py4e.com/book.php) - Charles Severance (PDF, EPUB, HTML)
* [Python for you and me](http://pymbook.readthedocs.org/en/py3/) (3.x)
* [Snake Wrangling For Kids](http://www.briggs.net.nz/snake-wrangling-for-kids.html) (3.x)
* [Suporting Python 3: An In-Depth Guide](http://python3porting.com) (2.6 - 2.x & 3.1 - 3.x)
* [The Standard Python Library](http://effbot.org/librarybook/) - Fredrik Lundh
* [Think Complexity](http://greenteapress.com/complexity/) - Allen B. Downey (2nd Edition) (PDF, HTML)
* [Pandas，让Python像R一样处理数据，但快](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483865&amp;idx=1&amp;sn=a2e1474bbebce343ff4262e38653f4c4&amp;chksm=ec0dc453db7a4d45349076b1627eff5e292abceada59e832a46553f4ca614d62df96e097f871#rd)
* [Learn Pandas (版本老了，有新的付费书(Python for data analysis)，网上也许有电子版)](https://bitbucket.org/hrojas/learn-pandas) - Hernan Rojas (0.18.1)

### R

* [在R中赞扬下努力工作的你，奖励一份CheetShet](http://mp.weixin.qq.com/s/x3tWrQPriLRFXO8ZaD93EQ)
* [R语言学习 - 入门环境Rstudio](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483882&amp;idx=1&amp;sn=e
16903b4b745a1ef51855be3824149f6&amp;chksm=ec0dc460db7a4d76a70bd4ca2d250f147225252ee963d3e577affaebeeb81dea1ff639d5e9aa
#rd)
* [R语言学习 - 热图绘制 (heatmap)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483889&amp;idx=1&amp;s
n=9c9970cb120ac1e976713aca558ac9bf&amp;chksm=ec0dc47bdb7a4d6d6441e36055aa075b03d5592862eae01c05761e5972b39a62cf2228b19
787#rd)
* [R语言学习 - 基础概念和矩阵操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483891&amp;idx=1&amp;s
n=40daf6435398c4d9a41f332e9bba4915&amp;chksm=ec0dc479db7a4d6fec413bfb90a4660eb035b440d2bbee998114f7af29e3b3338a8adf625
40a#rd)
* [153分钟学会 R](http://cran.r-project.org/doc/contrib/Liu-FAQ.pdf) (PDF)
* [R 导论](http://cran.r-project.org/doc/contrib/Ding-R-intro_cn.pdf) (《An Introduction to R》中文版) (PDF)
* [用 R 构建 Shiny 应用程序](http://yanping.me/shiny-tutorial/) (《Building 'Shiny' Applications with R》中文版)
* [统计学与 R 读书笔记](http://cran.r-project.org/doc/contrib/Xu-Statistics_and_R.pdf) (PDF)
* [Advanced R Programming (大神之作)](http://adv-r.had.co.nz) - Hadley Wickham
* [An Introduction to Statistical Learning with Applications in R](http://www-bcf.usc.edu/~gareth/ISL/) - Gareth James, Daniela Witten, Trevor Hastie and Robert Tibshirani (PDF)
* [Cookbook for R](http://www.cookbook-r.com) - Winston Chang
* [Introduction to Probability and Statistics Using R](http://cran.r-project.org/web/packages/IPSUR/vignettes/IPSUR.pdf) - G. Jay Kerns (PDF)
* [Learning Statistics with R](https://web.archive.org/web/20170625184412/http://health.adelaide.edu.au/psychology/ccs/teaching/lsr/) - Daniel Navarro
* [Machine Learning with R](https://www.packtpub.com/packt/free-ebook/r-machine-learning) - Brett Lantz, Packt. *(Just fill the fields with any values)*
* [ModernDive](https://ismayc.github.io/moderndiver-book/) - Chester Ismay and Albert Y. Kim
* [Practical Regression and Anova using R](http://cran.r-project.org/doc/contrib/Faraway-PRA.pdf) - Julian J. Faraway (PDF)
* [R for Data Science](http://r4ds.had.co.nz) - Garrett Grolemund and Hadley Wickham
* [R Language for Programmers](http://www.johndcook.com/blog/r_language_for_programmers) - John D. Cook
* [R Packages](http://r-pkgs.had.co.nz) - Hadley Wickham
* [R Practicals](http://www.columbia.edu/~cjd11/charles_dimaggio/DIRE/resources/R/practicalsBookNoAns.pdf) (PDF)
* [R Programming](https://en.wikibooks.org/wiki/R_Programming)
* [R Programming for Data Science](https://leanpub.com/rprogramming) (Needs valid email)
* [R Succinctly, Syncfusion](https://www.syncfusion.com/resources/techportal/ebooks/rsuccinctly) (PDF, Kindle) *(Just fill the fields with any values)*
* [The caret Package](http://topepo.github.io/caret/index.html) - Max Kuhn
* [The R Inferno (短小精悍)](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf) - Patrick Burns (PDF)
* [The R Language](http://stat.ethz.ch/R-manual/R-patched/doc/html)
* [The R Manuals](http://cran.r-project.org/manuals.html)
* [Tidy Text Mining with R](http://tidytextmining.com) - Julia Silge and David Robinson

#### Regular Expressions

* [Learn Regex The Hard Way](http://regex.learncodethehardway.org/book/) - Zed. A. Shaw
* [RexEgg](http://www.rexegg.com)
* [The 30 Minute Regex Tutorial](http://www.codeproject.com/Articles/9099/The-Minute-Regex-Tutorial) - Jim Hollenhorst
* [The Bastards Book of Regular Expressions: Finding Patterns in Everyday Text](https://leanpub.com/bastards-regexes) - Dan Nguyen
* [正则表达式-菜鸟教程](http://www.runoob.com/regexp/regexp-tutorial.html)
* [正则表达式30分钟入门教程](https://web.archive.org/web/20161119141236/http://deerchao.net:80/tutorials/regex/regex.htm)


#### Cloud Computing

* [Monitoring Modern Infrastructure](https://www.datadoghq.com/ebook/monitoring-modern-infrastructure/) *(account required)*
* [Multi-tenant Applications for the Cloud, 3rd Edition](http://www.microsoft.com/en-us/download/details.aspx?id=29263)
* [OpenStack Operations Guide](https://docs.openstack.org/ops-guide/index.html)

#### Datamining

* [A Programmer's Guide to Data Mining](http://guidetodatamining.com) - Ron Zacharski (Draft)
* [Data Jujitsu: The Art of Turning Data into Product](http://www.oreilly.com/data/free/data-jujitsu.csp) *(Just fill the fields with any values)*
* [Data Mining Algorithms In R](https://en.wikibooks.org/wiki/Data_Mining_Algorithms_In_R)
* [Internet Advertising: An Interplay among Advertisers, Online Publishers, Ad Exchanges and Web Users](http://arxiv.org/pdf/1206.1754v2.pdf) (PDF)
* [Introduction to Data Science](https://docs.google.com/file/d/0B6iefdnF22XQeVZDSkxjZ0Z5VUE/edit?pli=1) - Jeffrey Stanton
* [Mining of Massive Datasets](http://www.mmds.org)
* [School of Data Handbook](http://schoolofdata.org/handbook/)
* [Theory and Applications for Advanced Text Mining](http://www.intechopen.com/books/theory-and-applications-for-advanced-text-mining)

#### Machine Learning

* 一部分，还有其他比较适合初级学习的，如集体智慧编程 (Programming Collective Intelligence)
* [A Brief Introduction to Neural Networks](http://www.dkriesel.com/en/science/neural_networks)
* [A Course in Machine Learning](http://ciml.info/dl/v0_9/ciml-v0_9-all.pdf) (PDF)
* [A First Encounter with Machine Learning](https://www.ics.uci.edu/~welling/teaching/ICS273Afall11/IntroMLBook.pdf) (PDF)
* [An Introduction to Statistical Learning](http://www-bcf.usc.edu/~gareth/ISL/) - Gareth James, Daniela Witten, Trevor Hastie and Robert Tibshirani
* [Bayesian Reasoning and Machine Learning](http://web4.cs.ucl.ac.uk/staff/D.Barber/pmwiki/pmwiki.php?n=Brml.HomePage)
* [Deep Learning](http://www.deeplearningbook.org) - Ian Goodfellow, Yoshua Bengio and Aaron Courville
* [Gaussian Processes for Machine Learning](http://www.gaussianprocess.org/gpml/)
* [Information Theory, Inference, and Learning Algorithms](http://www.inference.phy.cam.ac.uk/itila/)
* [Introduction to Machine Learning](http://arxiv.org/abs/0904.3664v1) - Amnon Shashua
* [Learn Tensorflow](https://bitbucket.org/hrojas/learn-tensorflow) - Jupyter Notebooks
* [Learning Deep Architectures for AI](http://www.iro.umontreal.ca/~bengioy/papers/ftml_book.pdf) (PDF)
* [Machine Learning](http://www.intechopen.com/books/machine_learning)
* [Machine Learning, Neural and Statistical Classification](http://www1.maths.leeds.ac.uk/~charles/statlog/)
* [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com)
* [Probabilistic Models in the Study of Language](http://idiom.ucsd.edu/~rlevy/pmsl_textbook/text.html) (Draft, with R code)
* [Reinforcement Learning: An Introduction](http://incompleteideas.net/sutton/book/the-book.html)
* [The Elements of Statistical Learning](https://web.stanford.edu/~hastie/ElemStatLearn/) - Trevor Hastie, Robert Tibshirani, and Jerome Friedman
* [The LION Way: Machine Learning plus Intelligent Optimization](http://www.e-booksdirectory.com/details.php?ebook=9575)
* [The Python Game Book](http://thepythongamebook.com/en%3Astart)


#### Competitive Programming

* [Competitive Programmer's Handbook](https://cses.fi/book.html) - Antti Laaksonen (PDF)
* [Competitive Programming, 1st Edition](https://cpbook.net/#CP1details) (PDF)


#### Algorithms & Data Structures

* 算法部分还是了解都有什么，找一下比较有意思的帖子看起，刘未鹏的http://mindhacks.cn/是很好的入口，很好的思维，也推荐了很多心理、逻辑的书。
* [A Field Guide To Genetic Programming](http://dces.essex.ac.uk/staff/rpoli/gp-field-guide/toc.html)
* [Algorithmic Graph Theory](http://code.google.com/p/graphbook/)
* [Algorithms, 4th Edition](http://algs4.cs.princeton.edu/home/) - Robert Sedgewick and Kevin Wayne
* [Algorithms and Automatic Computing Machines (1963)](https://archive.org/details/Algorithms_And_Automatic_Computing_Machines) - B. A. Trakhtenbrot
* [Algorithms and Complexity](https://www.math.upenn.edu/~wilf/AlgoComp.pdf) (PDF)
* [Algorithms Course Materials](http://jeffe.cs.illinois.edu/teaching/algorithms/) - Jeff Erickson
* [Analysis and Design of Algorithms](http://www.cse.iitd.ernet.in/~ssen/csl356/admin356.html) - Sandeep Sen, IIT Delhi
* [Animated Algorithm and Data Structure Visualization](http://visualgo.net) (Resource)
* [Annotated Algorithms in Python: Applications in Physics, Biology, and Finance](https://github.com/mdipierro/nlib) - Massimo di Pierro
* [Binary Trees](http://cslibrary.stanford.edu/110/BinaryTrees.pdf) (PDF)
* [Clever Algorithms](http://www.cleveralgorithms.com/nature-inspired/)
* [CS Unplugged: Computer Science without a computer](http://csunplugged.org/books/)
* [Data Structures](http://www.cse.iitd.ernet.in/~suban/cs130/index.html) - Prof. Subhashis Banerjee, IIT Delhi
* [Data Structures (Into Java) - Paul N. Hilfinger](http://www-inst.eecs.berkeley.edu/~cs61b/fa14/book2/data-structures.pdf) (PDF)
* [Data Structures and Algorithms: Annotated Reference with Examples](http://lib.mdp.ac.id/ebook/Karya%20Umum/Dsa.pdf) - G. Barnett and L. Del Tongo (PDF)
* [Data Structures Succinctly Part 1, Syncfusion](https://www.syncfusion.com/resources/techportal/ebooks/datastructurespart1) (PDF, Kindle) *(Just fill the fields with any values)*
* [Data Structures Succinctly Part 2, Syncfusion](https://www.syncfusion.com/resources/techportal/ebooks/datastructurespart2) (PDF, Kindle) *(Just fill the fields with any values)*
* [Elementary Algorithms](https://github.com/liuxinyu95/AlgoXY) - Larry LIU Xinyu
* [Foundations of Computer Science](http://infolab.stanford.edu/~ullman/focs.html) - Al Aho and Jeff Ullman
* [Handbook of Graph Drawing and Visualization](https://cs.brown.edu/~rt/gdhandbook/)
* [Lectures Notes on Algorithm Analysis and Computational Complexity (Fourth Edition)](https://larc.unt.edu/ian/books/free/license.html) - Ian Parberry (use form at bottom of license)
* [LEDA: A Platform for Combinatorial and Geometric Computing](http://people.mpi-inf.mpg.de/~mehlhorn/LEDAbook.html)
* [Linked List Basics](http://cslibrary.stanford.edu/103/LinkedListBasics.pdf) (PDF)
* [Linked List Problems](http://cslibrary.stanford.edu/105/LinkedListProblems.pdf) (PDF)
* [Matters Computational: Ideas, Algorithms, Source Code](http://www.jjj.de/fxt/fxtbook.pdf) (PDF)
* [Open Data Structures: An Introduction](http://opendatastructures.org) - Pat Morin
* [Planning Algorithms](http://planning.cs.uiuc.edu)
* [Problems on Algorithms (Second Edition)](https://larc.unt.edu/ian/books/free/license.html) - Ian Parberry (use form at bottom of license)
* [Purely Functional Data Structures](http://www.cs.cmu.edu/~rwh/theses/okasaki.pdf) (PDF)
* [Sequential and parallel sorting algorithms](http://www.inf.fh-flensburg.de/lang/algorithmen/sortieren/algoen.htm)
* [Text Algorithms](http://igm.univ-mlv.fr/~mac/REC/text-algorithms.pdf) (PDF)
* [The Algorithm Design Manual](http://www8.cs.umu.se/kurser/TDBAfl/VT06/algorithms/BOOK/BOOK/BOOK.HTM)
* [The Art of Computer Programming](http://www.cs.utsa.edu/~wagner/knuth/) - Donald Knuth (fascicles, mostly volume 4)
* [The Design of Approximation Algorithms](http://www.designofapproxalgs.com/book.pdf) (PDF)
* [The Great Tree List Recursion Problem](http://cslibrary.stanford.edu/109/TreeListRecursion.pdf) (PDF)
* [Think Complexity](http://greenteapress.com/complexity/) (PDF)


免费书地址：<https://github.com/EbookFoundation/free-programming-books>


