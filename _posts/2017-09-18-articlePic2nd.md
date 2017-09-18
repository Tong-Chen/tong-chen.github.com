---
title: 文章用图的修改和排版(2)
author: ct
layout: post
categories:
  - Bioinfo
tags:
  - Bioinfo
---

教师节时，我们推出了[文章用图的修改和排版](http://mp.weixin.qq.com/s/IJNyhinakY0lSXgCN7b9ug)视频教程，演示了如何利用`Adobe Illustrator`修改分析获得的矢量图和实验获得的标量图。并整理了一系列的视频教程在 [生信宝典视频教程R TCGA Cytoscape](http://mp.weixin.qq.com/s/C4EBufEtFF6bhBKrH8NXng)

在录制那期视频时，翻阅了之前准备文章期间做的图形排版教程。当时每天都在不断的调整图和排版，心得体会比现在更多些，也录制了视频，但是无声版，录制完之后为`EXE`格式。如果您已观看过[文章用图的修改和排版](http://mp.weixin.qq.com/s/IJNyhinakY0lSXgCN7b9ug)视频教程，也自己操作过，有了一定基础，还想进一步的了解，可以看看这份无声版的记录是否能有些帮助。

### 矢量图和标量图

**矢量图**是使用直线和曲线来描述图形，这些图形的元素是一些点、线、矩形、多边形、圆和弧线等等，它们都是通过数学公式计算获得的。矢量图形最大的优点是无论放大、缩小或旋转等不会失真；最大的缺点是难以表现色彩层次丰富的逼真图像效果。常见的矢量图有`PDF`, `SVG`, `EPS`等格式。如果图形中有文字，并且文字可以复制，则可初步判断为矢量图。

与矢量图相对应的就是**标量图**了，常见的`png`, `jpg`, `gif`格式等，是由像素点构成，放大到一定程度会出现马赛克效果。图中的文字不可复制，元素不可拆分。

### 矢量图的制作

* 常规图：
    * `Excel`，生成的图可以直接拷贝到`AI`里面修改
    * `R`，`Perl`，`Python`等程序语言输出`pdf`, `eps`格式的图 (详见公众号中[R作图系列](http://mp.weixin.qq.com/s/zUS5dSa6cAQqR48XVJrt-g))

* 常用工具的出图
    * 二代测序出图  `UCSC` – `PDF`; `IGV` – `SVG`; `epigenomegateway` - `SVG`; 在高通量数据可视化文章中也有介绍。    
    * Motif   `Weblogo` - `eps` 
    * 作图软件 Graphpad


	
### 矢量图编辑工具

主要有 `Gimp`, `Adobe illustrator`, `Inkscape`, `image magik`, `photoshop`, `latex`。适用之后，从稳定性还是易用性来讲，`Adobe illustrator`是最好的一款。但是是收费软件，在线会有一些测试版，供测试时用。


### 作图基本原则

* 图形中文字的字体保持统一，一般使用`Helevetica`或`Arial`
* 符号一般使用`Symbol`字体，常见符号有 `′`, `β`等
* Panel的字号(A,B,C,D)一般比其余的文字大一号，上下左右对齐
* 文字特别密集的地方字体可适当缩小，原则是看着协调
* 图和图之间的距离在空间允许的情况下尽可能的大

![](http://blog.genesino.com/images/articlePic2nd_1.png)

* 一篇文稿所有柱状图理论上柱子的宽度保持一致
* 柱状图的`Error bar`宽度一致
* 坐标轴上的刻度尺宽度，长度一致
* 坐标轴的宽度、颜色一致
* 胶图的泳道对齐

![](http://blog.genesino.com/images/articlePic2nd_2.png)

### 作图中的要点注意

* 标准化，便于位置调整
    * 从最开始作图，到文章投稿、修改、定稿，中间会不断调整，子图会根据文章需要不断删减，调整位置。因此标准化之后，就可以很简单的互换位置就可以了。
    * 每个子图的长宽尽量一致
    * 每个相似子图内部元素的特征一致，比如柱子的宽度 (`6 mm`)，柱子之间的距离，坐标轴的刻度的宽度 (`0.7 mm`)，误差线的宽度 (`1 mm`)，P-value连接线宽度 (`6 mm`)，胶图泳道的宽度等。

* 合理利用对齐工具，左右对齐、横向分布、纵向分布等, 即保证对齐效果，又免去人为调整的繁琐
* 在选择单个元素时尽量使用直接选择工具
* 作图要做到自己满意，自己对自己负责；当你觉得一个地方不合适需要调整时，一定要及时修改；如果怕麻烦现在没调整，过几天别人发现或自己觉得不舒服也还是会再调整的。所有要做好充足的准备和充足的工作。
* 保留备份，保留备份,保留备份.每次大的修改都要保留原始版本，因为不知道明天是否还会改回来。


### 视频教程

左边是修改前的，右边是成品或近成品截图。

1. AI编辑线图.exe

![](http://blog.genesino.com/images/articlePic2nd_3_line.png)

2. AI_柱状图.exe

![](http://blog.genesino.com/images/articlePic2nd_4_bar.png)

3. AI_UCSC.exe

![](http://blog.genesino.com/images/articlePic2nd_5_ucsc.png)

4. AI_设计.exe

![](http://blog.genesino.com/images/articlePic2nd_6_model.png)

5. 图形导出

可以导出为PDF、TIFF格式；最好用**PhotoShop**导出，分辨率高，文件小。

6. 视频文件统一下载地址：链接: <https://pan.baidu.com/s/1dFcWadV> 密码: (后台回复 `AI`或`拼图`获取密码)



