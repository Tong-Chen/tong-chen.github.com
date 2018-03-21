---
title: Linux下那些查找命令
author: ct
layout: post
categories:
  - Linux
tags:
  - Linux
  - Bioinfo
---

查找是我们每天都在做的事情，早上醒来找下手机，出门之前查下公交，坐下之后查下资料，分析数据查下模式。

查找文件，查找信息，查找错误是应用起来更为具体的一些工作，而Linux命令行为我们提供了很多快捷强大的查找方式。

## 命令/可执行程序查找

`whereis program_name`: 会在系统默认安装目录(一般是有root权限时默认安装的软件)查找二进制文件、源码、文档中包含给定查询关键词的文件。(默认目录有 `/bin`, `/sbin`, `/usr/bin`, `/usr/lib`, `/usr/local/man`等类似路径)

`which program_name`: 会给出所有在[环境变量](http://mp.weixin.qq.com/s/poFpNHQgHDr0qr2wqfVNdw)中的程序的路径，一来方便知道运行的程序在哪，二来方便修改。比如[vim \`which sp_pheatmap.sh\`](https://mp.weixin.qq.com/s/_9LKs6t6rcjzokF_0gneSA)就可以直接修改绘制热图的脚本，`cp \`which sp_pheatmap.sh\` .`可以直接把源码拷贝到当前目录，省去了写全路径的麻烦。

如果运行`which bwa`，系统返回是 `/usr/bin/which: no bwa in (/home/usr/bin:/bin)`则说明bwa没有放置在环境变量中，不可以直接写名字调用。

## 普通文件快速定位 locate

`locate`是快速查找定位文件的好方法，但其依赖于`updatedb`建立的索引。而`updatedb`一般是每天运行一次，所以当天的新文件是索引不到的。如果有根用户权限，可以手动运行`updatedb`做个更新，然后再`locate bwa`。(个人用户也可以构建自己的updatedb, 使用locate在局部环境中查找。)

## 普通文件多条件查找 find

`find / -name bwa`可以搜索根目录下所有名字为bwa的文件

运行上面的命令时会输出很多`Permission denied`，是因为 作为普通用户，无权限访问一些目录，因此会有提示输出，可以使用`find / -name bwa 2>/dev/null`重定向标准错误到空设备，报错信息就被扔掉了，还不影响正常输出。

**按时间查找**

我们开发的在线画图网站 ([www.ehbio.com/ImageGP](http://mp.weixin.qq.com/s/pTHHqxuf0y1MCCCBaZjt9A))，为了追踪每天用户使用时碰到了什么问题，需要每天定时去查看日志。

这个命令`find . -name *.log -mmine -60`可以查看当前目录下(包括所有子目录)一小时内修改的日志文件。再配合`head`就可以查看每个日志文件的内容，以方便查看使用过程中出现了哪些错误，如何增加提示或修改画图程序。

正是有了这个利器，前台的错误提示中才出现了这么一句话，**如果您核对后数据和参数没问题，请过1天再进行尝试。若是程序问题，我们通常会在1天内修复。**。

当然后台数据都是用时间戳存储的，而且若无报错，数据会直接删掉，有报错的才会保留日志，不会泄露用户信息，这点大家不同担心。

现在画图网站越来越稳定，出现的问题越来越少，前台提示也越来越完善，查看日志的频率也少了，就使用`find . -name *.log -mtime -1`查看从现在起24小时内的日志了。

 这个也有个问题，每次查看的时间可能不一致，会漏查或有重叠，于是在某次查看完日志后，使用`touch check`在当前目录下新建了个空文件。以后再查日志文件时，只要使用`find . -name *.log -newer check`就可以获得所有上次查看过之后的新日志。每次查看完之后，都做个书签，就方便多了。

慢慢发现有空日志文件, 使用`find . -name *.log -newer check -size +0`过滤掉, 只保留大小大于0的文件。就这样在小伙伴聪明勤奋地维持下，我们绘图网站为**3万**多用户提供了近**10万**次服务。

近来绘图网站新增了**曼哈顿图**，**PcOA**, **CPcOA**和**桑基图**的绘制，近日会推出一份更新文档，欢迎使用。

**按类型和大小查找**

如果我想得到当前目录下所有`png`和`jpg`照片呢？ 

使用 `find . \( -name "*.png" -o -name "*.jpg" \) | less`

或 `find . -regex ".*\(\.png\|\.jpg\)$"`  


`find . -type f -size +100G`可以获取大小超过100G的文件。

**限制查找深度**

只看当前目录2层子目录内的文件`find . -maxdepth 2 -name *.log`。

查看不是`log`结尾的文件`find . -not -name *.log`。还有更多组合操作，详见find文档。

## 按文件内容查找 grep

find可以查找包含某句话的文件吗？ 还是拿我们的日志说事吧，`find . -name *.log -exec grep -l 'Error' {} \;`就可以返回所有包含`Error`单词的文件名。

`find . -name *.log | xargs grep -l 'Error'`也可以。

`grep -rl 'Error' *`也可以，不加`-l`还可以顺便返回匹配的行。

**匹配行的前后行**

`grep -A 5 -B 1 'Bioinfo' ehbio.log`可以查看匹配行的前1行(B, before)和后5行(A, after)。

**匹配次数**

`grep -c 'Bioinfo' ehbio.log`可以统计包含Bioinfo的行数

`grep -ci 'Bioinfo' ehbio.log`则会在匹配时忽略大小写。

统计FASTA序列中的序列数 `grep '^>' ehbio.fa`

统计FASTQ序列中的序列数 `grep '^+$' ehbio.fq`。(^表示以什么开头，$表示以什么结尾)。

**获取未匹配行**

`grep -v 'Bioinfo' ehbio.log`，读读手册(`man grep`)，可以看到更多参数使用。

**序列提取**

假设有个基因列表文件 (ID)，有个单行序列的FASTA文件 (ehbio.fa)， 运行如下命令`grep -A 1 -Fw -f id ehbio.fa | grep -v -- '--'`就可以批量提取序列了。

`-f id`表示把id文件中的每一行作为一个匹配模式。`-F`表示匹配模式作为原始字符串，而非正则表达式，这是以防有特殊字符被解析。`-w`则表示作为一个单词匹配，即假如id中有`Sox2`，那么它会匹配`Sox2`，也会匹配`Sox21`；如果加了`-w`，则不会匹配`Sox21`。

更好的序列批量提取见 [awk的使用](http://mp.weixin.qq.com/s/R1OHRhZoDJuAdyVdJr2xHg)。

**模式匹配**

grep强大的功能是支持正则匹配，默认使用基本正则表达式，`-E`使用扩展的正则表达式，`-P`使用perl格式的正则表达式。

比如想去掉文件中所有的空行`grep -v '^$' ehbio.fa >ehbio.clean.fa`;

从公众号文章中搜索跟文章写作相关的文章 `grep 'writ.*' *.md` (可以匹配write, writing等字)；

正则表达式就比较多了，具体可以看<http://mp.weixin.qq.com/s/4lUiZ60-aXLilRk9--iQhA>。

## 总结

Linux命令是生信学习的基本功，需要长时间的积累和实验。现在有个让您快速学习的方法，想不想知道呢？

生信宝典在**3月24日**安排了Linux培训，快速学习Linux基本命令和常用生物信息学软件。Linux学好了虽然不能立即处理转录组、ChIP-seq分析，但如果不被这些基础知识绊住脚，你可以花更多精力在解决你的生物问题上，磨刀不误砍材工。如果你要做好生信，这块是必不可少的，学得好，也会事半功倍。

请阅读原文查看更多信息。


如果你更喜欢自学或想提前了解下，请阅读下面文章。


* [Linux-总目录](http://mp.weixin.qq.com/s/hEYU80fPf1eD5OWL3fO4Bg)
* [Linux-文件和目录](http://mp.weixin.qq.com/s/yKP1Kboji9N4p2Sl1Ovj0Q)
* [Linux-文件操作](http://mp.weixin.qq.com/s/4bYMzJclf_xHpqdrlbvAdA)
* [Linux文件内容操作](http://mp.weixin.qq.com/s/QFgINAYcQA9kYYSA28wK-Q)
* [Linux-环境变量和可执行属性](http://mp.weixin.qq.com/s/poFpNHQgHDr0qr2wqfVNdw)
* [Linux - 管道、标准输入输出](http://mp.weixin.qq.com/s/zL9Mw_2ig48gHrIjKM0CMw)
* [Linux - 命令运行监测和软件安装](http://mp.weixin.qq.com/s/TNU7X2mhfVVffaJ7NRBuNA)
* [Linux-常见错误和快捷操作](http://mp.weixin.qq.com/s/cDIN4_R4nETEB5irmIGFAQ)
* [Linux-文件列太多，很难识别想要的信息在哪列；别焦急，看这里。](http://mp.weixin.qq.com/s/1QaroFE7AH1pREuq-k2YAw)
* [Linux-文件排序和FASTA文件操作](http://mp.weixin.qq.com/s/R1OHRhZoDJuAdyVdJr2xHg)
* [Linux-应用Docker安装软件](http://mp.weixin.qq.com/s/HLHiWMLaWtB7SOJe_jP3mA)
* [Linux服务器数据定期同步和备份方式](http://mp.weixin.qq.com/s/c2cspK5b4sQScWYMBtG63g)
* [VIM的强大文本处理方法](https://mp.weixin.qq.com/s/4lUiZ60-aXLilRk9--iQhA)
* [Linux - Conda软件安装方法](http://mp.weixin.qq.com/s/A4_j8ZbyprMr1TT_wgisQQ)
* [查看服务器配置信息](http://mp.weixin.qq.com/s/xq0JfkHJJeHQk1acjOAJUQ)
* [Linux - SED操作，awk的姊妹篇](http://mp.weixin.qq.com/s/cywkIeRbhkYTZvkwTeIVSA)
* [Linux - 常用和不太常用的实用awk命令](http://mp.weixin.qq.com/s/8wD14FXt7fLDo1BjJyT0ew)
* [Bash概论 - Linux系列教程补充篇](http://mp.weixin.qq.com/s/lWNp_6W_jLiogmtlk9nO2A)


