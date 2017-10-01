---
title: 学习生信的系列教程
author: ct
layout: post
categories:
  - Bioinfo
tags:
  - Bioinfo
---


生信的作用越来越大，想学的人越来越多，不管是为了以后发展，还是为了解决眼下的问题。但生信学习不是一朝一夕就可以完成的事情，也许你可以很短时间学会一个交互式软件的操作，却不能看完程序教学视频后就直接写程序。也许你可以跟着一个测序分析流程完成操作，但不懂得背后的原理，不知道什么参数需要修改，结果可以出来，却把我不住对还是错。

学习生信从来就不是一个简单的事，需要做好持久战的心理准备。

在学习时，我们都希望由浅入深的逐步深入，不断地练习和实践，这就是为什么我们需要一本书，因为书很系统。但生信发展的历史短于计算机编程的历史，如果想要一门程序设计的入门数据，每种语言都可以找到几本。但想要一个囊括生信的书，就有些难了。本身生信跨领域，需要多学科的知识，而其内部又有不少分子，都囊括了太大，包括的少又有些隔靴搔痒的感觉。

我们当时都是零基础下自学Linux, 自学Python，自学R，自学高通量测序；这些学习经历，之前都零星地记录在博客里。现在回头去看几年前自己记录的东西，觉得好简单，而当时却费了很大的力气。这些零星的随手记，当时也只是为了自己看，到现在确实只有自己能看得懂，不便惠及更多的人。

因此我们创建了生信宝典，希望从不同的角度传播知识。这个不同有三点含义，一是形式上的不同，摒弃之前主编们单人作战想写啥就写啥，而是有组织有计划的内容聚合，提供一系列的教程，由入门到提高。二是内容的不同，不去用网上现有教程的通用数据做例子，而是拿实际生物数据，讲述如何解释生信中普遍碰到的问题，讲述如何处理自己的数据。三是立足点不同。在写作时，我们回到了当年，在回忆中用整个阶段的学习去指导当初的那个小白，从那些会了的人觉得微不足道而不会的人又迈不过的坎入手，直击痛点。知识点的收录依据不是是否炫酷，是否难，而是是否必要。如果必要，再简单，也要提及；如果不必要，再炫酷，也暂不纳入。

通过大量的生信例子、关键的注释和浓缩的语句形成下面的一系列学习教程。每一篇内容都不多，可以当做小说阅读，也可以跟着去练，反复几遍，每读一次都会有不同的收获和体会。


### 程序学习心得

* [生物信息之程序学习](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483927&amp;idx=1&amp;sn=23adf2b9d13400f2081f790e674e2cba&amp;chksm=ec0dc79ddb7a4e8b5bb7a413744319a90f425371b30e2c85224b7c183cc4ad4bbd5d9749bb7b#rd"})
* [如何优雅的提问](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483955&amp;idx=1&amp;sn=946438376f94af6e8861b2b42701914e&amp;chksm=ec0dc7b9db7a4eafbef28fac1fb260f6f876f0ba674828784ac827dd23f9317f5a2d59d38bc0#rd)
* [生信宝典视频教程](http://mp.weixin.qq.com/s/C4EBufEtFF6bhBKrH8NXng)
* [好色之旅-画图三字经](https://mp.weixin.qq.com/s/bsvB1k17Izom2ldgdwXrdg)


### Linux 学习

* [文件和目录](http://mp.weixin.qq.com/s/yKP1Kboji9N4p2Sl1Ovj0Q)
* [文件操作](http://mp.weixin.qq.com/s/4bYMzJclf_xHpqdrlbvAdA)
* [文件内容操作](http://mp.weixin.qq.com/s/QFgINAYcQA9kYYSA28wK-Q)
* [环境变量和可执行属性](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483872&amp;idx=1&amp;sn=7fb7e57b3ff5c06ebaff344370c8b4c8&amp;chksm=ec0dc46adb7a4d7cc125ab3cf8361bf3e3fcf858edca7d7987d52bce3e9e3aa0b7d8f8f2adfa#rd)
* [管道、标准输入输出](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483923&amp;idx=1&amp;sn=eb764e59cfc12b98e3eb4240ac350330&amp;chksm=ec0dc799db7a4e8f9dc3a64760253a554d3241446005040ad721070bafb237f405b173c11ef4#rd)
* [命令运行监测和软件安装](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483954&amp;idx=1&amp;sn=11247591a6ef98a4d25404278d577ed0&amp;chksm=ec0dc7b8db7a4eaeb7ae3fd2fa2fbfa7bfd13f5e90d7a42d405f6f8e8783761de048f7ccbc58#rd)
* [常见错误和快捷操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483873&amp;idx=1&amp;sn=6e2b9ddb6ba61c49d834bcfba6703c5c&amp;chksm=ec0dc46bdb7a4d7d6d1232390f6f8843607b37ecca7938d19c20404dff0cf01aebfff77a0cdd#rd)
* [文件列太多，很难识别想要的信息在哪列？](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483952&amp;idx=1&amp;sn=5312e0bab13182b118376018cb69674b&amp;chksm=ec0dc7badb7a4eacb5d96d971df6ccd940435b7525962963e625736efd2a413ae76844c3ee48#rd)
* [文件排序和FASTA文件操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483823&amp;idx=1&amp;sn=ac62450f0475dc9513e75009f0670f45&amp;chksm=ec0dc425db7a4d3300f547caeaee709425dd0a41c86be18aab44d41619a4d18944289b0deaf8#rd"})
* [用了Docker，妈妈再也不担心我的软件安装了 - 基础篇](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483840&amp;idx=1&amp;sn=f87f6dd703cd8c109f6dc5b8d12ffb7c&amp;chksm=ec0dc44adb7a4d5c9ff2422c730b1d7bb18dcb6947c0e7449f1678aee492c3193302174930b4#rd)
* [Linux服务器数据定期同步和备份方式](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483950&amp;idx=1&amp;sn=6f4dbc46a064638d7c95b9f99cb1de70&amp;chksm=ec0dc7a4db7a4eb20751dd6567b1c97be7d536671af07707eb57bb1ea7865cbde17a0226a6e0#rd)
* [不用Linux也可以的强大文本处理方法](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484250&amp;idx=1&amp;sn=d4759dc05a55643549646c77318c4f96&amp;chksm=ec0dc6d0db7a4fc64791896914547b5ce818e8bd3cca98f0fb7bf6ebd9029fe6fd08a4d55255#rd)
* [又双叒叕一个软件安装方法](http://mp.weixin.qq.com/s/A4_j8ZbyprMr1TT_wgisQQ)
* [查看服务器配置信息](http://mp.weixin.qq.com/s/xq0JfkHJJeHQk1acjOAJUQ)

### R统计和作图

* [入门环境Rstudio](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483882&amp;idx=1&amp;sn=e16903b4b745a1ef51855be3824149f6&amp;chksm=ec0dc460db7a4d76a70bd4ca2d250f147225252ee963d3e577affaebeeb81dea1ff639d5e9aa#rd)
* [热图绘制 (heatmap)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483889&amp;idx=1&amp;sn=9c9970cb120ac1e976713aca558ac9bf&amp;chksm=ec0dc47bdb7a4d6d6441e36055aa075b03d5592862eae01c05761e5972b39a62cf2228b19787#rd)
* [基础概念和矩阵操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483891&amp;idx=1&amp;sn=40daf6435398c4d9a41f332e9bba4915&amp;chksm=ec0dc479db7a4d6fec413bfb90a4660eb035b440d2bbee998114f7af29e3b3338a8adf62540a#rd)
* [热图简化](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483921&amp;idx=1&amp;sn=8326bc566e945386cad27250a33a1bf6&amp;chksm=ec0dc79bdb7a4e8d28bb909994432dab9bf09346b6f64a35ec1e657cbb298f10ca20c6838ca7#rd)
* [热图美化](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483901&amp;idx=1&amp;sn=5770a863352acd8f8aec3e157131bef8&amp;chksm=ec0dc477db7a4d61e5ee49323529d5b406941f0b2ebb63a8a8e7f35b28b97ada059692671c5b#rd)
* [线图绘制](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483937&amp;idx=1&amp;sn=8368c9346ccce10121c8a7b574c12f88&amp;chksm=ec0dc7abdb7a4ebd859713b8740b53f148e3ebb5047776e9cf42f2306ab082b6b968568f2f23#rd)
* [线图一步法](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483947&amp;idx=1&amp;sn=7cf0252efff5433447507b977fcaff97&amp;chksm=ec0dc7a1db7a4eb77a269709bdf2c8ab51bcad89aa780ec0be171a333e1cb8f3cc27eff277a1#rd)
* [箱线图（小提琴图、抖动图、区域散点图）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483964&amp;idx=1&amp;sn=ee52ac37fb9a919f5c75c0abe2a49ad4&amp;chksm=ec0dc7b6db7a4ea0a51306347fc43265c41fda3eeaf4764ddc3795546371327579676cd74a38#rd)
* [箱线图一步法](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483971&amp;idx=1&amp;sn=1b40a1137ccb8b2fa1ab3eb1d0f05de9&amp;chksm=ec0dc7c9db7a4edf16ea4966b9acb7f23cd23bd6a2e59450ae11bdac899fa2fceb124264dcf4#rd)
* [火山图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483996&amp;idx=1&amp;sn=9a29d52e78e9acffeb0a78077a14f9f2&amp;chksm=ec0dc7d6db7a4ec0163259e81e4ded54875a5dd8adaafbc6975a86c71223d863627ba37801e5#rd)
* [富集分析泡泡图 （文末有彩蛋）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483978&amp;idx=1&amp;sn=e0c158c0e92375553036cc37f4987e40&amp;chksm=ec0dc7c0db7a4ed6ac593493b7d8b52f11f2feb92d24fa00d19527fbb6f95b24f7e313ef9440#rd")
* [散点图绘制](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484056&amp;idx=1&amp;sn=f9b2b4f7495b432e9294b7cbf42eaf33&amp;chksm=ec0dc712db7a4e04769d322558364b4b401b0a8153097c7252e83170e9201a31c2a7abbaf101#rd)
* [一文看懂PCA主成分分析](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484036&amp;idx=1&amp;sn=22ee356d0c9680d56dada1b777985ed2&amp;chksm=ec0dc70edb7a4e182a21475e9ddcde35b907c291549cc8c2e767be260af445ff5455aa358b04#rd)
* [富集分析DotPlot，可以服](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484063&amp;idx=1&amp;sn=f4e93d428e4910b4abbee9c0430cd170&amp;chksm=ec0dc715db7a4e0318b388ba2ab3d51677741421c42ada474a0ac6046a0699283014eae84b6f#rd)
* [韦恩图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484076&idx=1&sn=fa5af19a2a4db4b0c5c7f145bf93ca57&chksm=ec0dc726db7a4e30fe7a0492ed9ea8eb5fa1c34641b1442a2da003efde0546b30c48fde3f118#rd)
* [柱状图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484134&amp;idx=1&amp;sn=ffb41298eae74834af2f5dad05d37921&amp;chksm=ec0dc76cdb7a4e7a852ac0670532c12c690399f140a2335f640eaf01f7da26bc5480941686a9#rd)
* [图形设置中英字体](http://mp.weixin.qq.com/s/NAwyvtTS7t5rRU7KKBwHTA)
* [教师节献礼 - 文章用图的修改和排版](https://mp.weixin.qq.com/s/IJNyhinakY0lSXgCN7b9ug)
* [非参数法生存分析](http://mp.weixin.qq.com/s/_Dy9Yn8fc8I0rASGxH5x9A)
* [文章用图的修改和排版(2)](http://mp.weixin.qq.com/s/HTsufk71U3wf14OOWSKEeQ)

### NGS基础

* [NGS基础 - FASTQ格式解释和质量评估](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484047&amp;idx=1&amp;sn=3e2a79d9f56040a57ac2e16cf1923b54&amp;chksm=ec0dc705db7a4e133e6e91de9ac11a6c0690f03d7b3b760b358e9b0d1a2d57974599419d9fff#rd)
* [NGS基础 - 高通量测序原理](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484034&amp;idx=1&amp;sn=e7680ee935f8603214227b37eeb2c567&amp;chksm=ec0dc708db7a4e1eca4e38845381f328c49c84a90ad6580c3ba3761511772636e5ec0f185931#rd)
* [NGS基础 - 参考基因组和基因注释文件](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484148&amp;idx=1&amp;sn=525233898721a9c3ebdf275babf14944&amp;chksm=ec0dc77edb7a4e686440e0cbe5fbf39f554c4183dc30e7870ab7584e285f4e018dd94b680f79#rd)
* [NGS基础 - GTF/GFF文件格式解读和转换](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484166&amp;idx=1&amp;sn=417e155672bd718def86003b16bf0078&amp;chksm=ec0dc68cdb7a4f9a6bcb62c18797a69040173e2b0af20f1cf87d3e0d75e3adee03c7ff524dc5#rd)
* [本地安装UCSC基因组浏览器](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484167&amp;idx=1&amp;sn=ef9699899164d23013d92b61331c6562&amp;chksm=ec0dc68ddb7a4f9bfb83b9942196622f8b8f52b041d3f4a12786e6464752fbeaf64c9a640e39#rd)
* [测序数据可视化 (一)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483946&amp;idx=1&amp;sn=3f95769229f28a91ed8bf5889e2181be&amp;chksm=ec0dc7a0db7a4eb64d08c7799cfe698a1662e6d0d935a8b91c6c969aae86900df4decc469a0d#rd)
* [测序文章数据上传找哪里](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483843&amp;idx=1&amp;sn=43770d21f6c2da2393c31cd55fdbe31e&amp;chksm=ec0dc449db7a4d5f723842286bf7feab7830eba5d9778d351569810a069e5ace76040f94a6bd#rd)

### NGS分析工具评估

* [39个转录组分析工具，120种组合评估(转录组分析工具哪家强-导读版)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484106&idx=1&sn=687a0def51f6ea91a335754eb3dc9ca9&chksm=ec0dc740db7a4e564e5b1e93a36e5d9447581e262eec9c2983d1d4e76788d673c9c07dec8f8e#rd)
* [39个转录组分析工具，120种组合评估(转录组分析工具大比拼 （完整翻译版）)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484106&idx=2&sn=a09fa127d625c4072ae0343795346c56&chksm=ec0dc740db7a4e56821f32f60700027c85db46e81089721d1bbe23ceefa86160d9661c2f2d4c#rd)
* [无参转录组分析工具评估和流程展示](http://mp.weixin.qq.com/s/4HANWJY4oL7jGziroHfEpQ)

### 癌症数据库

* [UCSC XENA - 集大成者(TCGA, ICGC)](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484383&amp;idx=1&amp;sn=09c58de206f409fa375fb7af94d0084c&amp;chksm=ec0dc655db7a4f438cb7e53f281cb5c6bf2484619b3c72d7eafe064ea6a342f69587353531af#rd)
* [ICGC数据库使用](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484378&amp;idx=1&amp;sn=eb6a0f890326898b2fb0867c58f0cf90&amp;chksm=ec0dc650db7a4f46a0a265ec96b73f367d45f86318087507eef7dde117a369cb7ad427bebb1e#rd)
* [TCGA数据库在线使用](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484304&amp;idx=1&amp;sn=6ad44dafdc7613e33e13aac48edb32aa&amp;chksm=ec0dc61adb7a4f0c504f3aeb207132aef479572ea756ce15868cbc57f88e9ea25102752b646a#rd)
	
### Python学习

* [Python学习极简教程 （一）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483866&amp;idx=1&amp;sn=310341a1c8d348958c304df03dfd06a0&amp;chksm=ec0dc450db7a4d46e369637cd2867b0e56389bf4f2e1d0dce409bba38882e61e5063308a13af#rd)
* [Python学习教程（二）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483866&amp;idx=2&amp;sn=bf3c07ee1b2936c7ea06b5d4ca820545&amp;chksm=ec0dc450db7a4d469f4f625babfb595b068137ea2b25a7682f9fb58ff771db6543f43def7950#rd)
* [Python学习教程（三）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483866&amp;idx=3&amp;sn=dec66c5f3f12919ce1b0bfbb545e3935&amp;chksm=ec0dc450db7a4d46e91b65446d6a192056ab6ff27c019fe3770cc32816b0ae3f16659ebba0a5#rd)
* [Python学习教程 （四）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483866&amp;idx=4&amp;sn=3a0b0c5c0f736ddeadc4524bae8b2a91&amp;chksm=ec0dc450db7a4d465602b74e0fa968519a3a085a1901b5cca97ff886163422a24089378ff8f0#rd)
* [Python学习教程（五）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483866&amp;idx=5&amp;sn=fd3526e11c4adf8194e1f92cd6d1749c&amp;chksm=ec0dc450db7a4d468c7d114352153eecbaedd7d37065f681caa28b74258a92038d1d2030056b#rd)
* [Python学习教程 （六）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483866&amp;idx=6&amp;sn=ef7a0972abc002cfeba27815020e83aa&amp;chksm=ec0dc450db7a4d46f61328946fe257a1516785fb9a1f7c1663e86e4255ae6b616e3c07ac1cb0#rd)
* [Pandas，让Python像R一样处理数据，但快](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483865&amp;idx=1&amp;sn=a2e1474bbebce343ff4262e38653f4c4&amp;chksm=ec0dc453db7a4d45349076b1627eff5e292abceada59e832a46553f4ca614d62df96e097f871#rd)
* [Python解析psiBlast输出的JSON文件结果](http://mp.weixin.qq.com/s/BN6u2aJkoMzffPv7rvbm8g)

### NGS软件

* [Rfam 12.0+本地使用 （最新版教程）](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483831&amp;idx=1&amp;sn=718242148bb1cfe03140f4d8c3c3005f&amp;chksm=ec0dc43ddb7a4d2bb6e3c5c9169dbd9883fc4b68d9f68e4931e6b8a709f5265ad0ddeab68e04#rd)
* [轻松绘制各种Venn图](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483853&amp;idx=1&amp;sn=b3350a1c2e2f3ea66f2891d3521a90aa&amp;chksm=ec0dc447db7a4d516eb1255d09ce53cfa1f1dcda9de610193ea900c2f39b882e595d2e0f10e7#rd)
* [ETE构建、绘制进化树](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483988&amp;idx=1&amp;sn=d87d8f70ee4098a1f8340a753c8cbb56&amp;chksm=ec0dc7dedb7a4ec8da9143e0ef8e8c11d44ad54e7fb145e60f65fa09a431a26ec1971916af06#rd)
* [psRobot：植物小RNA分析系统](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484159&amp;idx=1&amp;sn=81dc70116b26b363ea2efeb7d6034dff&amp;chksm=ec0dc775db7a4e6330ae462efe39f174257dae34e76fec91715da3b8a09bc694abbab9c3f5c8#rd)
* [生信软件系列 - NCBI使用](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484235&amp;idx=1&amp;sn=1afa3b9b954e9f8bb99d954a5305681c&amp;chksm=ec0dc6c1db7a4fd7098a872b887f8e077aa2d1fcf101614df050524d945eceda54150ecebc72#rd)
* [去东方，最好用的在线GO富集分析工具](https://mp.weixin.qq.com/s/l6j2encDfEQkt2UeNCMFhg)

### Cytoscape网络图

* [Cytoscape教程1](http://mp.weixin.qq.com/s/m9uJm8GwSXb3xaRxtod08Q)
* [Cytoscape之操作界面介绍](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484184&amp;idx=1&amp;sn=2384ba8a6a6ea3ed7dac1b42217c710a&amp;chksm=ec0dc692db7a4f84a03feb4de092aa0712b1bca2975f1cee8fac8342d0a65f836f5f94e9d877#rd)
* [新出炉的Cytoscape视频教程](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484194&amp;idx=1&amp;sn=61bcbe1c48e195c5c830396865789723&amp;chksm=ec0dc6a8db7a4fbeaa9cdd7245127edd382f3e4d13a61636c2cbc52062b32d7565bf282fca5e#rd)

### 分子对接

* [来一场蛋白和小分子的风花雪月](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483842&amp;idx=1&amp;sn=653e97fb32eaa73ce9f26b22306cc369&amp;chksm=ec0dc448db7a4d5ef15d62d62df9e3a243a7e304c816c2a6ac3f878b07ede52010900e7c9136#rd)
* [不是原配也可以-对接非原生配体](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483842&amp;idx=3&amp;sn=caa5bb8ab6c868b8644c5f532b12adf2&amp;chksm=ec0dc448db7a4d5e9827d5419b08a8930b27c53d80d21c207f15be3a27eedc6fa1088de709f7#rd)
* [简单可视化-送你一双发现美的眼睛](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483842&amp;idx=2&amp;sn=c3c3f80b2e24ee5287678e4a853fb657&amp;chksm=ec0dc448db7a4d5e3a023a2067552d29ee5fca143192771d8d8570f9c9c8f65b13829360f487#rd)
* [你需要知道的那些前奏](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483842&amp;idx=4&amp;sn=8b7918a98e5e34f78263f248620d8311&amp;chksm=ec0dc448db7a4d5ec2a83703149caed48fa5afbe4822e855785448008e34a9991d9f428d8fec#rd)

### 生信宝典之傻瓜式

* [生信宝典之傻瓜式 (一) 如何提取指定位置的基因组序列](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484030&amp;idx=1&amp;sn=0d369c99fd49ebafefe60c00efe647b1&amp;chksm=ec0dc7f4db7a4ee241beb0fb8a3e5d8bf7e9ac69899db9b6b6522093bda21e5a2202ddf1edda#rd)
* [生信宝典之傻瓜式 (二) 如何快速查找指定基因的调控网络](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483852&amp;idx=1&amp;sn=d419fa404b987b4d70f789eb2de8478c&amp;chksm=ec0dc446db7a4d50e4700d88f42d3991ea622a058f1529586b533648dcee994e08f742133abe#rd)
* [生信宝典之傻瓜式 (三) 我的基因在哪里发光 - 如何查找基因在发表研究中的表达](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483864&amp;idx=1&amp;sn=c1df1a797a4c2e4cf5f0e0524664bebd&amp;chksm=ec0dc452db7a4d44a97031725ae4630bdbec7e37076144d60dfd83e17d04cd8a7003f039ecc0#rd)

### 生信人写程序

* [生信人写程序1. Perl语言模板及配置](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483837&amp;idx=1&amp;sn=660358a38b7fa6d3de2c95280f7a4535&amp;chksm=ec0dc437db7a4d21368b312ac43ceae552e1544570639c949e96bf488113a55f67fa2306008e#rd)
* [生信人写程序2. Editplus添加Perl, Shell, R, markdown模板和语法高亮](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483910&amp;idx=1&amp;sn=7813eaa4841d90b0bfc3982bb901de81&amp;chksm=ec0dc78cdb7a4e9a866f3e0cade3096a13366cac18c873820434f066fdba9bd22a7b5b3d210d#rd)

### 小技巧系列

* [参考文献中杂志名字格式混乱问题一次解决](http://mp.weixin.qq.com/s/Diwevx-TVe0Vq_rdgzIkrw)

### 友情链接流程

#### 宏基因组 - 扩增至分析流程

* [质控,实验设计,双端序列合并](https://mp.weixin.qq.com/s/lrHTX_zn3aNC8HMiV5yaZQ) 查看原始数据的质量，编写合格的实验设计用于分析，双端序列合并为单端的扩增子序列；
* [提取barcode,质控及样品拆分,切除扩增引物](https://mp.weixin.qq.com/s/S5_BmKlbVhKL-qZf6V69Xw) 将Barcode序列从序列中拆除，筛选高质量的测序结果并标记文库中每条序列中的样品来源，最后切除扩增时使用的引物；
* [格式转换,去冗余,聚类](http://mp.weixin.qq.com/s/XREEDvbLZSPVlv52rhjKzA) 转换QIIME生成fasta格式为Usearch要求格式；使用Usearch对序列去冗余并筛选高丰度，极大降低下游计算量和去除噪音；最后使用用Usearch聚类生成OTU，默认会组内自动去除大量嵌合体；
* [去嵌合体,非细菌序列,生成代表性序列和OTU表](http://mp.weixin.qq.com/s/HFD_1fNHBfGRLBhm9PPhcA) 本讲详细讲了嵌合体的概念，并使用参考数据库去除嵌合体；学习基于参数数据库筛选细菌序列，这些都是可选的操作，根据实际情况决定是否需要，最终生成高质量的OTU序列作为参考序列；
* [物种注释,OTU表操作](https://mp.weixin.qq.com/s/5FxwDj2aWTl3Ip2n4dfd2g) 这部分采于不同数据库进行细菌或真菌注释；同时根据实际情况，对OTU表进一步按样品、丰度、物种等条件筛选；
* [进化树,Alpha,Beta多样性](http://mp.weixin.qq.com/s/FGvj_jLiGiiMcHZq4dQq5w) 将OTU多序列比对生成进化树，为依赖进化关系的计算方法提供输入文件；再进行多种Alpha和Beta多样性的计算；
* [物种分类统计,筛选进化树和其它](https://mp.weixin.qq.com/s/VUAp2tmQc8-W1gz1mGU2fA) 对物种进行分类统计,筛选高丰度结果用于进化树展示，和其它用于R统计分析的结果生成。

#### 生信媛 - Biostar handbook

* [手把手教你入门生信——The Biostar Handbook](http://mp.weixin.qq.com/s/_1gIvdnxRSzYoQaGOiIVMA)
*[课程1、2-Linux中生信分析常用命令入门](http://mp.weixin.qq.com/s/e0pskjQvzytpdBSrIwEwfA)
*[课程3、4-NCBI的Entrez Direct和SRA toolkit的安装及使用](http://mp.weixin.qq.com/s/pwHDf16rU-eMiS5RWT5X3A)
*[课程5、6-编写可重复使用的脚本](https://mp.weixin.qq.com/s/eeWtoNGqqBiBZsak0gpnnQ)
*[课程7、8-二代测序质控：fastqc、prinseq、trimmomatic、seqtk](http://mp.weixin.qq.com/s/_1nCjk3ACJyy1MLiISwuCg)
*[课程9、10-测序文件的质控&在线序列比对](http://mp.weixin.qq.com/s/OVd-2T_6_4EgmjPe3oxZCg)
*[课程11、12-下载序列，建blast数据库以及本地blast](http://mp.weixin.qq.com/s/q7yT0Z-8d2nD8bjleJHpsw)
*[课程13、14-常用的mapping软件bwa & sam格式简介](http://mp.weixin.qq.com/s/yK1OyJHrePg6bWl41JCpvA)
*[课程15、16-samtools简介&利用readseq对GenBank文件格式转换](http://mp.weixin.qq.com/s/vqpmV45m_7T3bkKG41xSEw)
*[课程17、18-awk进行简单的编程&序列比对软件bwa和bowtie2](http://mp.weixin.qq.com/s/NZCt2SR3WmCnqpb2FGcbsQ)
*[课程19、20-利用samtools mpileup和bcftools进行SNP calling](http://mp.weixin.qq.com/s/XHkyqHWw3uParQPeMAEaEQ)
*[课程21、22-使用samtools和FreeBayes进行变异的calling并用snpEff注释](http://mp.weixin.qq.com/s/vR6gPWiTRmkonuaN6K_Xaw)
*[课程23、24-SNP calling](http://mp.weixin.qq.com/s/VY1XnNE8GBRewI90V2KRxw)
*[课程25、26-bedtools的安装和使用](http://mp.weixin.qq.com/s/Gx7edC6re8gb2ffuZhP4GA)
*[课程27、28-RNAseq分析](http://mp.weixin.qq.com/s/4gN24W5Ngomzffxb3u6sLA)
*[课程29、30（大结局）-差异表达分析以及用ErmineJ做GO](http://mp.weixin.qq.com/s/QMIfwPNPo6uCebvf1EOyIQ)

### Biobabble - ChIP-seq

+ [CS0: ChIPseq从入门到放弃](https://mp.weixin.qq.com/s?__biz=MzI5NjUyNzkxMg==&mid=2247483886&idx=1&sn=cb76891dff5787025f6b99cdcc723d86&chksm=ec43b0a9db3439bfcec1c9ac3c0d00e6190cf4d3d02d9d3dc767007e0ff68b4fbd8064bb0f77#rd)
+ [CS1: ChIPseq简介](https://mp.weixin.qq.com/s?__biz=MzI5NjUyNzkxMg==&mid=2247483980&idx=1&sn=4106c9341d0a048a9fb8042c7ac328d5&chksm=ec43b30bdb343a1ddc6ed772ed25e82362595a11d82f2fb20f85106722bca381ba328ea4bb60#rd)
+ [CS2: BED文件](https://mp.weixin.qq.com/s/D06NEG7blksGugb0srL7KQ) 
+ [CS3: peak注释](https://mp.weixin.qq.com/s?__biz=MzI5NjUyNzkxMg==&mid=2247484023&idx=1&sn=affbe46869290ffc4f2be2c73209bdad&chksm=ec43b330db343a262602f57156578195011ae6ef3d61ad928d60ef919811678bf605b5048a64#rd)
+ [CS4：关于ChIPseq注释的几个问题](https://mp.weixin.qq.com/s?__biz=MzI5NjUyNzkxMg==&mid=2247484084&idx=1&sn=b3fb1b88a9f73e26278688dfbce60679&chksm=ec43b3f3db343ae5ea5a657b22bd0ed427c928f75c45484badaf6a6714777d8239cb0b1997b5#rd)
+ [CS5: 吃着火锅，唱着歌，还把分析给做了](https://mp.weixin.qq.com/s?__biz=MzI5NjUyNzkxMg==&amp;mid=2247484728&amp;idx=1&amp;sn=68894d1621c317499fdfd8d313402c73&amp;chksm=ec43b47fdb343d69250c4027b7ad668cfd2963a4a842a41e17d481d2ac7a660bdea02605698d#rd)

### 招聘

* [易汉博欢迎您加入](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247484036&amp;idx=5&amp;sn=bb1007d2c3d60e7a2bcf2d6fc7a9a2bb&amp;chksm=ec0dc70edb7a4e185bafd0f49440bf1a032915c7e8d8fc2cb37c70a81ce3446a4ae990df89a5#rd)


## 联系我们

![](http://blog.genesino.com/images/ehbio/ehbio_RNAseq.jpg)


![](http://blog.genesino.com/images/ehbio/EHBIO_hire_bioinfo1.jpg)


![](http://blog.genesino.com/images/ehbio/shengxinbaodian_gognzhonghao.jpg)
