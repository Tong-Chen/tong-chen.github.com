---
title: 小学生都学Python了，你还不知道怎么开始
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

最近Python又火了一把，一是我大山东省**小学六年级**的教材中加入了Python的内容;二是从2018年起，Python也将成为浙江**高考**的内容之一；三是计算机二级考试加入了Python科目。

早先常常看到新闻，国外4-5岁的小孩开发APP，给MM开发游戏之类的。可以看到，国外对小孩编程的教育还是比较早的，通常也会使用**python**来编程，因为它简洁易用。亚马逊上早早的就有了`Python for kids`和`Python Bytes: An ABC Introduction to Programming for Toddlers`系列面向小孩编程的丛书。**Andrew Ng**9月14在Quora上对问题（[I have a toddler. How should she prepare herself for the job market 15 years from now in the world of AI? Should I teach her Python as soon as she is willing to learn?](https://www.quora.com/I-have-a-toddler-How-should-she-prepare-herself-for-the-job-market-15-years-from-now-in-the-world-of-AI-Should-I-teach-her-Python-as-soon-as-she-is-willing-to-learn)）回答到"Yes, do teach her to code. More importantly, cultivate in her the ability to **keep learning**."，后面说"I think almost **everyone** should learn to code in the same way that almost everyone should learn to read/write." 不过在这个回答里面，并没看到ANdrew Ng说的自己小孩一旦会说话就要学编程。不过会加减运算应该就可以编程了。

Python是[Guido van Rossum](https://gvanrossum.github.io//index.html)在1989年为了打发无聊的圣诞节 (假期少，也是我们缺少创造力的一个原因)时开始编写的，到1991年第一个版本正式释放，其设计正是顺应了计算机的快速发展，希望能有更易于编写的语言。名字来源于英国肥皂剧《Monty python and the Flying Circus》。标志物是大蟒蛇，虽然有些吓人，但也慢慢越来越可爱。而且因为这个名字还受到同名成人网站的混淆，导致其主页会间断性打不开。

2017年，也是Python排名又上一个新台阶的一年，在ranked.com的排名中，Python是2017年**最受欢迎人工智能**编程语言（第二是C++）。根据Stack Overflow流量统计，2017年6月，Python第一次成为高收入国家Stack Overflow访问量最大的标签，照此发展，到了2018年，Python肯定会成为最受欢迎的标签。在GitHub 2017年度报告中，Python超越Java成**第二受欢迎**语言。

这些排名，跟它强大的功能是分不开的。小到数据格式转换，大到人工智能，都有Python的一席之地。几大公司, Google, NASA, Facebook, Yahoo, Youtube, Quora, Dropbox, BitTorrent等等都在大量使用。著名的包有：

1. 科学计算 `Numpy`, `SciPy` (也是安装python包的拦路虎直到有了[conda](http://mp.weixin.qq.com/s/A4_j8ZbyprMr1TT_wgisQQ)
2. 类比于R的数据框操作包 [Pandas](http://mp.weixin.qq.com/s/1h-_J2NKjD1KyymPAeHPOg)
3. 可视化工具 `Seaborn` (配合pandas), `matplotlib` (类比MATLAB), `plotly` (交互式绘图), `ggplot` (类比ggplot2)
4. 网站开发 `web.py`, `Django`, `Flask`
5. 任务调度和流程管理 `Airflow` (pipeline首选)
6. 机器学习 `scikit-learn` (经典), `PyML`, `Tensorflow` (谷歌释放), `pylearn2`, `Orange` (图形界面的机器学习包)
7. 网页抓取 `Beautiful Soup`，`requests`, 
8. 可重复编程 `Jupyter`
9. 正则表达式 `re`

简洁的特性和丰富的包，既可以快速上手，又可以使用更多高阶功能解决问题。所以，ANSI C++ Committee member Bruce Eckel说 **Life is short (You need Python)**。

另外相传：Guido van Rossum去谷歌面试，带一份简历，上输三个字`I wrote Python`，就不需要面试了。想不想也给自己的简历加点料呢。

### 如何学习编程

编程就像拼乐高，需要我们知道每个组分的特征以便在需要时可以使用，也需要脑袋中有个蓝图知道每一步要做什么，二者结合，就可以拼出你想要的世界。

第一步就是读一本书，反复多读几遍，后面提到的**简明Python教程**就适合多读几遍，看的懂的记住，看不懂的多看几遍，还看不懂的就忽略。然后就可以了。生信方面可以参考[生信宝典出品的Python简明教程](https://mp.weixin.qq.com/s/9BNrq8Lu7hjtO2BAKOIXOA)，经过了培训的检测。

第二步就是做题，[12个生信练习题](http://mp.weixin.qq.com/s/478DiO0RdO9zEGSZ0NzsiA)，三个维度的训练，作出来就会了。

### 如何快速学习编程

之前提到的教程是关于Python2.X系列的，到2020年Python社区全面转向Python 3系列 (2和3的比较见后面资源列表的帖子)。在2018年即将到来之际，也没什么纠结的了，果断选择**Python 3**。之前的教程就不合适了，生信宝典联合北大计算机系本科毕业后转生信的中科院博士和301医院临床博士推出**应用Python处理生物信息数据和作图**培训班，全面升级**Python 3**，定位于生信入门的编程基础课。**不管你有没有基础，都可以报名参加**。

培训的意义在于帮你**跨越从概念到行动**这一步。基本的Python编程语法是了解乐高积木的每个元件，拼出什么形状是对生信问题的分析，衔接这两段的是如何去实践。初学者，最困难的是转化想法为代码；进阶后，最困难的是有更好的想法。这些我们都涵盖，如何入门，如何体味Python的强大，如何特异地应用于生信分析。

相比于自己阅读，培训提供专业的人士指导、集中的学习氛围，让你远离纷扰，静下心来体会编程的乐趣。一旦集中精力迈进了这个门，以后任何环境、任何碎片时间都可以利用起来提高编程能力了。所以，长按[二维码](http://www.ehbio.com/Training)塑造一个更好的自己吧。


### 资源列表

* Guido van Rossum 个人主页，查看大牛的博客和访谈 https://gvanrossum.github.io//index.html
* Beginner's guide for python https://wiki.python.org/moin/BeginnersGuide
* Python2 or 3 https://wiki.python.org/moin/Python2orPython3
* Quick and Dirty python scripts http://sebsauvage.net/python/programs.html
* ActiveState收录的流行Python代码段 http://code.activestate.com/recipes/langs/python/ 此链接可下载打包版本 http://sebsauvage.net/python/recipes.zip
* XKCD plot http://nbviewer.jupyter.org/url/jakevdp.github.com/downloads/notebooks/XKCD_plots.ipynb
* 以色列特拉维夫大学python教程 Tel-Aviv https://github.com/yoavram/CS1001.py
* 一篇pandas使用notebook  http://nbviewer.jupyter.org/github/phelps-sg/python-bigdata/blob/master/src/main/ipynb/pandas.ipynb
* 有趣的Jupyter notebook ，涉及多个领域、包(代码、解释、图形、表格都在一起，数百份教程，快速学习的首选) https://github.com/jupyter/jupyter/wiki/A-gallery-of-interesting-Jupyter-Notebooks
* 另一个详细的教程 http://nbviewer.jupyter.org/github/lijin-THU/notes-python/blob/master/index.ipynb
* 小抄大全 http://blog.csdn.net/qazplm12_3/article/details/78782797
* Python从新手到专家 http://www.kuqin.com/docs/diveintopythonzh-cn-5.4b/html/toc/
* 哈佛大学的算法课 (前面主要是python基本使用，回答问题，老教授会给发糖，现在好像找不到了，不过这个链接给了很多好的课) https://github.com/prakhar1989/awesome-courses
* Python MOOC集锦 http://coursegraph.com/search_results/python
* 简明python教程 (翻看3遍即可) http://www.kuqin.com/abyteofpython_cn/
* Google的Python课 https://blog.hartleybrody.com/google-python/
* 廖雪峰的Python教程 https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000
* 父与子的编程 (上到88岁，下到8岁，都可以阅读本书。它不仅以一种有趣的方式介绍了Python编程的知识，其中的最佳实践还适用于其他编程语言的学习。) http://www.ituring.com.cn/book/1353
* 哈佛计算机基础课 (基础概念，加深理解) http://open.163.com/special/opencourse/cs50.html
