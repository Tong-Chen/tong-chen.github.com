---
title: R 学习 - 图形设置中英字体
author: ct
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

绘制生信宝典调查总结文中的柱状图时，出现了中文乱码，就搜索了下解决方案，记录如下。

### 修改图形的字体

ggplot2中修改图形字体。

```
# 修改坐标轴和legend、标题的字体
theme(text=element_text(family="Arial"))
# 或者
theme_bw(base_family="Arial")

# 修改geom_text的字体
geom_text(family="Arial")
```

### ggplot2支持中文字体输出PDF

`showtext`包可给定字体文件，加载到R环境中，生成新的字体家族名字，后期调用这个名字设定字体，并且支持中文写入pdf不乱码

```
library(showtext)
showtext.auto(enable=TRUE)

font_path = "FZSTK.TTF"
font_name = tools::file_path_sans_ext(basename(font_path))
font.add(font_name, font_path)

# 修改坐标轴和legend、标题的字体
theme(text=element_text(family=font_name))

# 修改geom_text的字体
geom_text(family=font_name)
```


### 系统可用字体

* Linux字体一般在 `/usr/share/fonts`下，也可以使用`fc-list`列出所以加载的字体。

* Windows字体在 `C:\Windows\Fonts\`下，直接可以看到，也可以拷贝到Linux下使用。

### 合并字体支持中英文

通常情况下，作图的字体都是英文，ggplot2默认的或按需求加载一种字体就可以了。但如果中英文混合出现时，单个字体只能支持一种文字，最好的方式是合并两种字体，类似于Word中设置中英文分别使用不同的字体。

软件[FontForge](https://github.com/fontforge/fontforge)可以方便的合并中英文字体，其安装也比较简单，直接 `yum install fontforge.x86_64`。

假如需要合并`FZSTK.TTF` (windows下获取)和`Schoolbell-Regular.ttf` (谷歌下载)，这两个都是手写字体。按如下，把字体文件和程序脚本`mergefont.pe`放在同一目录下，运行`fontforge -script mergefont.pe`即可获得合并后的字体`FZ_School.ttf`。

```
$ ls
FZSTK.TTF mergefont.pe Schoolbell-Regular.ttf
$ cat mergefont.pe
Open("FZSTK.TTF")
SelectAll()
ScaleToEm(1024)
Generate("temp.ttf", "", 0x14)
Close()

# Open English font and merge to the Chinese font
Open("Schoolbell-Regular.ttf")
SelectAll()
ScaleToEm(1024)

MergeFonts("temp.ttf")
SetFontNames("FZ_School", "FZST", "Schoolbel", "Regular", "")
Generate("FZ_School.ttf", "", 0x14)
Close()

$ fontforge -script mergefont.pe
$ ls
FZ_School.ttf FZSTK.TTF mergefont.pe Schoolbell-Regular.ttf
```

然后安装前面的介绍使用`showtext`导入即可使用。

### 一个示例

字体文件自己从Windows获取，School bell从Google fonts获取。

```r
library(showtext)
## Add fonts that are available on current path

# 方正字体+schoole bell (中英混合)
font.add("FZ_School", "FZ_School.ttf")
# 黑体
font.add("simhei", "simhei.ttf")
font.add("Arial","arial.ttf")

# 黑体和Arial的合体
font.add("HeiArial", "HeiArial.ttf")
showtext.auto()  ## automatically use showtext for new devices

library(ggplot2)


p = ggplot(NULL, aes(x = 1:10, y = 2^(1:10), group=1)) + geom_line() +
  theme(axis.title.y=element_text(family="Arial"), axis.title.x=element_text(family="HeiArial"), 
        plot.title=element_text(family="simhei")) +
  xlab("Days spent on 生信宝典") + 
  ylab("Things you have learned") +
  ggtitle("生信宝典，换个角度学生信") + 
  annotate("text", 7, 300, family = "FZ_School", size = 8,
           label = "收获曲线 (Harvest curve)", angle=15) 

# annotate指定的是文字的中间部分的位置

ggsave(p, filename="example-SXBD.pdf", width = 7, height = 4)  ## PDF device

```

![](http://blog.genesino.com/images/scbd_font.png)


### Reference

* 中英文字体混合 [http://www.voidcn.com/article/p-gnggkwmy-vn.html](http://www.voidcn.com/article/p-gnggkwmy-vn.html)
* 改变字体类型 [https://github.com/yixuan/showtext](https://github.com/yixuan/showtext)
* 获取文件名 [https://stackoverflow.com/questions/29113973/getting-filename-without-extension-in-r](https://stackoverflow.com/questions/29113973/getting-filename-without-extension-in-r)

### 生信宝典，换个角度学生信

* [R语言学习 - 图形设置中英字体](http://mp.weixin.qq.com/s/NAwyvtTS7t5rRU7KKBwHTA)



## 生信宝典，生物信息学习系列教程，转录组，宏基因组，外显子组，R作图，Python学习，Cytoscape视频教程

[http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg](http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg)

## 生信宝典，最好的生物信息培训课程，培训课程资料

[www.ehbio.com/Training](www.ehbio.com/Training)
