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

当有人把要查找的东西扔到群里后，看看群友们的反应吧。

(模仿微信群聊天界面，每个人不同头像，可以用我们绘图网站图标做头像，回答者的名字也可以用绘图网站每个图的名字，中英文都可，或者其它好的方面)

Q: 我安装了个软件，大家能告诉我装哪了吗？

A1: 装了啥？

A2: 在哪装的？

A3: 怎么装的？

A4: 来逗我们的吗？

A5: 我就默默地看你们猜

Q: 有没有人知道，新手，能帮帮吗？

A6: 建议看下如何提问(http://mp.weixin.qq.com/s/xCif04bqZB14Z4OvesK0SQ转成二维码，不保留链接，图上也点不了)

3分钟后

Q：我在Linux下用Conda安装了BWA，请问安装到什么地方了？

A1：试试 `whereis bwa`, 在我电脑上返回`/usr/bin/bwa`。 

Q: 我这输出结果是`bwa:`。

A2: 试试 `which bwa`，我这返回`/ehbio/bin/bwa`。`whereis`查找的是固定的几个路径。

Q: 也不可以，输出是`/usr/bin/which: no bwa in (/home/ct/bin:/bin)`。

A2: 如果你的可执行程序在环境变量中, `which`可以找到。如果不在，就得用`find`了。

A1: 可以看看这篇conda的介绍，顺藤摸瓜去查找。http://mp.weixin.qq.com/s/A4_j8ZbyprMr1TT_wgisQQ

A3: `find / -name bwa`可以搜索根目录下所有名字为bwa的文件

A4: 运行上面的命令时会输出很多`Permission denied`，怎么办？

A3: 作为普通用户，无权限访问一些目录，因此会有提示输出，可以使用`find / -name bwa 2>/dev/null`重定向标准错误到空设备，报错信息就被扔掉了，还不影响正常输出

A5: `find`在全局下搜索还是挺慢的，可以试试`locate bwa`。

A6: `locate`是快速查找定位文件的好方法，但其依赖于`updatedb`建立的索引。而`updatedb`一般是每天运行一次，所以今天的新文件估计是索引不到的，可以手动运行`updatedb`做个更新，然后再`locate bwa`。

Q: 谢谢大家，问题解决了。Linux下还有这么多查找命令呢。

A1：`find`的功能可强大了，还能做很多事呢。

A1: 我们开发的在线画图网站 (www.ehbio.com/ImageGP)，为了追踪每天用户使用时碰到了什么问题，需要每天定时去查看日志。这个命令`find . -name *.log -mmine -60`可以查看当前目录下(包括所有子目录)一小时内修改的日志文件。再配合`head`就可以查看每个日志文件的内容，以方便查看使用过程中出现了哪些错误，如何增加提示或修改画图程序。正事有了这个利器，我们在在前台的错误提示中才出现了这么一句话，**如果您核对后数据和参数没问题，请过1天再试一次。若是程序问题，我们通常会在1天内修复**。当然后台数据都是用时间戳存储的，不会泄露用户信息，这点大家不同担心。

A1: 现在画图网站越来越稳定，出现的问题越来越少，前台提示也越来越完善，查看日志的频率也少了，就使用`find . -name *.log -mtime -1`查看从现在起24小时内的日志了。

A1: 这个也有个问题，每次查看的时间可能不一致，会漏查或有重叠，于是在某次查看完日志后，使用`touch check`在当前目录下新建了个空文件。以后再查日志文件时，只要使用`find . -name *.log -newer check`就可以获得所有上次查看过之后的新日志。

A1: 慢慢发现有空日志文件, 使用`find . -name *.log -newer check -size +0`过滤掉, 只保留大小大于0的文件。就这样在小伙伴聪明勤奋地维持下，我们绘图网站为**3万**多用户提供了近**10万**次服务。

Q2: 如果我想得到当前目录下所有`png`和`jpg`照片呢？

A2: `find . \( -name "*.png" -o -name "*.jpg" \) | less`

A3: 楼上命令可以更简洁一些`find . -regex ".*\(\.png\|\.jpg\)$"`  

Q2: 系统越用越久，空间也越来越小，怎么查看都有哪些大文件？

A3: `find . -type f -size +100G`可以获取大小超过100G的文件。

Q3: find可以查找包含某句话的文件吗？

A1: 还是拿我们的日志说事吧，`find . -name *.log -exec grep -l 'Error' {} \;`就可以返回所有包含`Error`单词的文件名。

A3: `find . -name *.log | xargs grep -l 'Error'`也可以。

A2: `grep -rl 'Error' *`也可以，不加`-l`还可以顺便返回匹配的行。

Q2: 那如果还想看匹配行的前后行呢？

A2: `grep -A 5 -B 1 'Bioinfo' ehbio.log`可以查看匹配行的前1行(B, before)和后5行(A, after)。

A3: 不只能看到匹配，还可以看到匹配了多少次呢, `grep -c 'Bioinfo' ehbio.log`可以统计包含Bioinfo的行数。`grep -ci 'Bioinfo' ehbio.log`则会在匹配时忽略大小写。

A2: 楼上的方法可以用来统计FASTA序列中的序列数`grep '^>' ehbio.fa`或FASTQ序列中的序列数`grep '^+$' ehbio.fq`。(^表示以什么开头，$表示以什么结尾)。

Q3: 如果想要没匹配上的行呢？

A1: `grep -v 'Bioinfo' ehbio.log`，读读手册(`man grep`)，可以看到更多参数使用。

A2: 我有个基因列表，也有个单行序列的FASTA文件，能把这些基因对应的序列提出吗?

A3: 单行FASTA就简单了, 假设你的基因列表文件名是`id`, 运行如下命令`grep -A 1 -Fw -f id ehbio.fa | grep -v -- '--'`就可以了。`-f id`表示把id文件中的每一行作为一个匹配模式。`-F`表示匹配模式作为原始字符串，而非正则表达式，这是以防有特殊字符被解析。`-w`则表示作为一个单词匹配，即假如id中有`Sox2`，那么它会匹配`Sox2`，也会匹配`Sox21`；如果加了`-w`，则不会匹配`Sox21`。

A1: 楼上提醒的到位，还是使用`awk`更保险些。具体可看http://mp.weixin.qq.com/s/R1OHRhZoDJuAdyVdJr2xHg。

A4: grep强大的功能是支持正则匹配，默认使用基本正则表达式，`-E`使用扩展的正则表达式，`-P`使用perl格式的正则表达式。

比如想去掉文件中所有的空行`grep -v '^$' ehbio.fa >ehbio.clean.fa`;

从公众号文章中搜索跟文章写作相关的文章 `grep 'writ.*' *.md` (可以匹配write, writing等字)；

正则表达式就比较多了，具体可以看http://mp.weixin.qq.com/s/4lUiZ60-aXLilRk9--iQhA。

A5: find还有几个前面没提到的用法，如只看当前目录2层子目录内的文件`find . -maxdepth 2 -name *.log`。或者查看不是`log`结尾的文件`find . -not -name *.log`。还有更多组合操作，详见find文档。

