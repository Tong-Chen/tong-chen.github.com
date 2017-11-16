---
title: Record of circos usage 
layout: post
categories:
  - circos
  - letter
tags:
  - circos
---

`Circos`是绘制圈图的神器，在<http://circos.ca/images/>页面有很多CIRCOS可视化的示例。

![](http://circos.ca/img/panel-genomic.png)

![](http://circos.ca/img/panel-general.png)

Circos可以在线使用，在线使用时是把表格转为圈图，不过只允许最大75行和75列；做一些简单的示意图会比较好，最后时会介绍下在线的`tableviewer`的使用。

也可以安装在本地，在本地可以绘制基于基因组的更复杂的图。

Circos由Perl写成，安装相对简单，只要Perl的包都装好了就可以了。

### Circos安装

* 从<http://circos.ca/software/download/circos/>下载Circos安装包，并解压，把安装包内的bin目录加载到[环境变量](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247483872&idx=1&sn=7fb7e57b3ff5c06ebaff344370c8b4c8&chksm=ec0dc46adb7a4d7cc125ab3cf8361bf3e3fcf858edca7d7987d52bce3e9e3aa0b7d8f8f2adfa#rd)。

  ```bash
  wget http://circos.ca/distribution/circos-0.69-6.tgz
  tar xvzf circos-0.69-6.tgz
  ln -s `pwd`/circos-0.69-6/bin/* ~/bin #make sure ~/bin is in $PATH

  or
  # 注意pwd两侧的反引号
  export PATH=$PATH:`pwd`/circos-0.69/bin
  ```

* 安装依赖的Perl包
    * 配置CPANM (CPANM是一个文件，下载下来，增加可执行属性，放到环境变量中即可使用)
      
      ```bash
      # 若无根用户权限，也可放入自己家目录下在环境变量内的目录中就可以 
	  wget https://raw.githubusercontent.com/miyagawa/cpanminus/master/cpanm -O /sbin/cpanm
      chmod +x /sbin/cpanm
      ```

    * 获得依赖的Perl包，`circos -module`
      
      ```bash
      ok       1.11 Carp
      missing            Clone
      missing            Config::General
      ok        3.3 Cwd
      ok      2.124 Data::Dumper
      ok       2.55 Digest::MD5
      ok       2.77 File::Basename
      ok        3.3 File::Spec::Functions
      ok       0.22 File::Temp
      ok       1.50 FindBin
      missing            Font::TTF::Font
      missing            GD
      missing            GD::Polyline
      ok       2.38 Getopt::Long
      ok       1.14 IO::File
      missing            List::MoreUtils
      ok       1.21 List::Util
      missing            Math::Bezier
      ok       1.60 Math::BigFloat
      missing            Math::Round
      missing            Math::VecStat
      ok    1.01_03 Memoize
      ok       1.17 POSIX
      missing            Params::Validate
      ok       1.36 Pod::Usage
      missing            Readonly
      missing            Regexp::Common
      missing            SVG
      missing            Set::IntSpan
      missing            Statistics::Basic
      ok       2.20 Storable
      ok       1.11 Sys::Hostname
      ok      2.0.0 Text::Balanced
      missing            Text::Format
      ok     1.9721 Time::HiRes
      ```

    * 获取缺失模块并安装
      
      ```bash
      # 第一句话的目的只是查看需要运行的命令，直接运行第二句就好
      circos -module | grep 'missing' | awk '{a=a" "$2;}END{print "cpanm"a}'
      circos -module | grep 'missing' | awk '{a=a" "$2;}END{system("cpanm"a);}'
      ```

    * 再运行`circos -module`发现`GD`和`GD::Polyline`没安装上，查看错误信息是`No package 'gdlib' found`
    
      ```bash
      # 根用户
      yum install gd-devel
      ```

    * 然后再用`cpanm`安装`GD`和`GD::Polyline`。 

### 最简单出图

把下面的内容存储到任意目录下的任意文件比如`ehbio.conf`下，然后运行`circos -conf ehbio.conf`就可以获得circos的图`circos.png`和`circos.svg`。

```
karyotype = data/karyotype/karyotype.human.txt

<ideogram>

<spacing>
default = 0.005r
</spacing>

radius    = 0.9r
thickness = 20p
fill      = yes

</ideogram>

################################################################
# The remaining content is standard and required. It is imported 
# from default files in the Circos distribution.
#
# These should be present in every Circos configuration file and
# overridden as required. To see the content of these files, 
# look in etc/ in the Circos distribution.

<image>
# Included from Circos distribution.
<<include etc/image.conf>>
</image>

# RGB/HSV color definitions, color lists, location of fonts, fill patterns.
# Included from Circos distribution.
<<include etc/colors_fonts_patterns.conf>>

# Debugging, I/O an dother system parameters
# Included from Circos distribution.
<<include etc/housekeeping.conf>>
```

![](images/circos.png)
	
上述命令是怎么运行的呢？

```
# karyotype定义染色体的名字、ID、起始位置信息，是绘制图的根本
karyotype = data/karyotype/karyotype.human.txt

# 必须的部分，控制染色体信息显示
<ideogram>

# 定义染色体之间的间距，为图形半径的5% (r代表radius，半径)
<spacing>
default = 0.005r
</spacing>

# 染色体区域的绘制位置，默认所有染色体都处于远离圆心同样距离的位置
# 这里设置的是图形半径的0.9倍的位置
# 也可以设置绝对像素值
radius    = 0.9r
# 染色体区域的宽度，可以是相对图形半径，也可以说绝对像素值
thickness = 20p

# 染色体区域填充颜色
fill      = yes

</ideogram>

################################################################
# The remaining content is standard and required. It is imported 
# from default files in the Circos distribution.
#
# These should be present in every Circos configuration file and
# overridden as required. To see the content of these files, 
# look in etc/ in the Circos distribution.

# 这些都是引用文件，暂时不去管什么意思，后面用到再逐个解释。
# 但是绘图时这些必须引用。下面会解释下最关键的引用位置。
<image>
# Included from Circos distribution.
<<include etc/image.conf>>
</image>

# RGB/HSV color definitions, color lists, location of fonts, fill patterns.
# Included from Circos distribution.
<<include etc/colors_fonts_patterns.conf>>

# Debugging, I/O an dother system parameters
# Included from Circos distribution.
<<include etc/housekeeping.conf>>
```
	
最开始看CIRCOS的配置文件时，不理解其是如何查找用到的数据和配置目录时，不过上面配置文件中被注释掉的一句话泄露了天机`look in etc/ in the Circos distribution`。配置文件和数据文件默认先在当前目录查找，若没有则去CIRCOS的安装目录下查找。

下面列出了CIRCOS搜索配置文件时查找的目录(搜索数据时也类似)

```
.
./etc
/MPATHB/soft/circos-0.69-6/bin/etc
/MPATHB/soft/circos-0.69-6/bin/../etc
/MPATHB/soft/circos-0.69-6/bin/..
/MPATHB/soft/circos-0.69-6/bin
```

不得不敢写CIRCOS的日志输出，很详细，每次都刷屏。当我们运行CIRCOS失败时，看下日志信息，会得到很多提示。

数据和配置文件都在CIRCOS安装目录下，那么先看看它的目录结构吧。

### circos安装目录介绍

`bin`: 目录下是`circos`可执行程序，加入环境变量即可

`data`: 目录下有一个文件夹`karyotype`，里面收录了几个物种染色体信息文件。

```
karyotype.chimp.txt karyotype.arabidopsis.tair10.txt
karyotype.human.hg38.txt karyotype.human.hg19.txt
karyotype.mouse.mm10.txt karyotype.yeast.txt karyotype.zeamays.txt
```

这个是绘制CIRCOS图所必须的一个文件 (文件的内容虽然通常是染色体的信息，但不局限于染色体信息，其它的区域信息、时间序列信息都可以使用)

文件内容如下 (`#`后面是注释，会被忽略)

前两列是固定的，`chr -`。`chr`表示定义一条染色体；`-`表示指定这个区域的父区域，染色体没有父区域，用`-`代替。

`ID`是当前区域的名字，其子区域的父区域列都使用这个名字。如果同时绘制多个物种，可在ID中包含物种的代号。

`LABEL`是当前区域显示的名字。

`START END`是当前区域的范围，必须是整个的区域。如果想显示部分区域，可在后续配置中修改。

`COLOR`是当前区域的颜色，CIRCOS为每个染色体有定义好的颜色，存储于`etc/colors.conf`。除了预先定义了染色体的颜色，还定义了一些颜色变量可以直接使用。

```
#chr - ID LABEL START END COLOR
chr - hs1 1 0 248956422 chr1
chr - hs2 2 0 242193529 chr2
chr - hs3 3 0 198295559 chr3
chr - hs4 4 0 190214555 chr4
chr - hs5 5 0 181538259 chr5
chr - hs6 6 0 170805979 chr6
chr - hs7 7 0 159345973 chr7
chr - hs8 8 0 145138636 chr8
chr - hs9 9 0 138394717 chr9
```

`etc`目录下是配置文件，前面引用到了3个。

`image.conf`内容如下

```
<<include image.generic.conf>>
<<include background.white.conf>>
```

`image.generic.conf`内容如下，定义了输出的图形的名字、格式、大小等，这些都可以在自定义配置文件，即前面提到的`ehbio.conf`中覆盖。

```
dir   = . 
#dir  = conf(configdir)
file  = circos.png
png   = yes
svg   = yes

# radius of inscribed circle in image
radius         = 1500p

# by default angle=0 is at 3 o'clock position
angle_offset      = -90

#angle_orientation = counterclockwise

auto_alpha_colors = yes
auto_alpha_steps  = 5
```

`background.white.conf`只定义了背景是白色。

`colors_fonts_patterns.conf`引用了颜色、字体、预定义的图形文件信息的配置

```
<colors>
<<include etc/colors.conf>>
</colors>
<fonts>
<<include etc/fonts.conf>>
</fonts>
<patterns>
<<include etc/patterns.conf>>
</patterns>
```

`colors.conf`及其引用文件内容摘录如下，利用RGB组合设置了颜色变量、系列颜色和染色体的颜色。(染色体的名字全部使用小写)

```
dpblue   = 0,153,237
vdpblue  = 0,136,220
vvdpblue = 0,120,204

vvlpurple = purples-7-seq-1
vlpurple  = purples-7-seq-2

gpos100 = 0,0,0
gpos    = 0,0,0
gpos75  = 130,130,130

chr1  = 153,102,0
chr2  = 102,102,0
chr3  = 153,153,30
```

`patterns.conf`定义特殊小图形的信息

```
# pattern fills for PNG files

vline        = tiles/vlines.png
vline-sparse = tiles/vlines-sparse.png

hline        = tiles/hlines.png
hline-sparse = tiles/hlines-sparse.png

checker        = tiles/checkers.png
checker-sparse = tiles/checkers-sparse.png

dot        = tiles/dots.png
dot-sparse = tiles/dots-sparse.png
solid      = tiles/solid.png
```

`housekeeping.conf`必须在最上层自定义配置文件中(也就是`ehbio.conf`)中引用。这个文件名字起的很生物，持家配置，必须要，而且不建议修改。具体内容就不列出了，感兴趣的自己去看。

### 展示染色体染色数据 

把前面的配置文件再拓展一些，给染色体加上名字，并且按照染色深浅上色。

`karyotype`变量指定了绘制CIRCOS图所必须的一个文件 (文件的内容虽然通常是染色体的信息，但不局限于染色体信息，其它的区域信息、时间序列信息都可以使用)

文件内容如下 (`#`后面是注释，会被忽略)

前两列是固定的，`chr -`。`chr`表示定义一条染色体；`-`表示指定这个区域的父区域，染色体没有父区域，用`-`代替。

`ID`是当前区域的名字，其子区域的父区域列都使用这个名字。如果同时绘制多个物种，可在ID中包含物种的代号。

`LABEL`是当前区域显示的名字。

`START END`是当前区域的范围，必须是整个的区域。如果想显示部分区域，可在后续配置中修改。

`COLOR`是当前区域的颜色，CIRCOS为每个染色体有定义好的颜色，存储于`etc/colors.conf`。除了预先定义了染色体的颜色，还定义了一些颜色变量可以直接使用。

```
#chr - ID LABEL START END COLOR
chr - hs1 1 0 248956422 chr1
chr - hs2 2 0 242193529 chr2
chr - hs3 3 0 198295559 chr3
chr - hs4 4 0 190214555 chr4
chr - hs5 5 0 181538259 chr5
chr - hs6 6 0 170805979 chr6
chr - hs7 7 0 159345973 chr7
chr - hs8 8 0 145138636 chr8
chr - hs9 9 0 138394717 chr9
```

如果有`cytogenetic band`信息，则写到文件末尾。`band`是固定的，`DOMAIN`指定从属信息，对应于上面染色体的`ID`信息。其它列与上面解释相同。

```
#band DOAMIN ID LABEL START END COLOR
band hs1 p36.33 p36.33 0 2300000 gneg
band hs1 p36.32 p36.32 2300000 5400000 gpos25
band hs1 p36.31 p36.31 5400000 7200000 gneg
band hs1 p36.23 p36.23 7200000 9200000 gpos25
band hs1 p36.22 p36.22 9200000 12700000 gneg
band hs1 p36.21 p36.21 12700000 16200000 gpos50
```

![](http://www.ehbio.com/ehbio_resource/circos_label_band.png)

```
# karyotype定义染色体的名字、ID、起始位置信息，是绘制图的根本
karyotype = data/karyotype/karyotype.human.txt

# 必须的部分，控制染色体信息显示
# http://circos.ca/documentation/tutorials/reference/ideogram/
<ideogram>

# 定义显示的染色体之间的间距，为图形半径的0.5% (r代表radius，半径)
<spacing>
default = 0.005r
</spacing>

# 染色体区域的绘制位置，默认所有染色体都处于远离圆心同样距离的位置
# 这里设置的是图形半径的0.9倍的位置
# 也可以设置绝对像素值
radius    = 0.9r
# 染色体区域的宽度，可以是相对图形半径，也可以说绝对像素值
thickness = 20p

# 染色体区域填充颜色
fill      = yes

# 染色体边的颜色和宽度
stroke_thickness = 2
stroke_color = black

# 显示染色体标签名字
# 更多label的调整见 
# http://circos.ca/documentation/tutorials/ideograms/labels/lesson
show_label = yes
label_font = default
# ideogram外圈再加总半径的0.05
label_radius = dims(ideogram,radius_outer) + 0.005r

# 如果想把label标记在圈里可以写，外圈半径+内圈半径除以2
# label_rdius = (dims(ideogram,radius_outer)+dims(ideogram,radius_inner))/2
label_size = 24
# label与圈平行
label_parallel   = yes
label_case = upper

# 显示karyotype中定义的细胞遗传学条带
# fill_bands=yes 表示使用预先定义的颜色
show_bands            = yes
fill_bands            = yes
band_transparency     = 4


</ideogram>

################################################################
# The remaining content is standard and required. It is imported 
# from default files in the Circos distribution.
#
# These should be present in every Circos configuration file and
# overridden as required. To see the content of these files, 
# look in etc/ in the Circos distribution.

# 这些都是引用文件，暂时不去管什么意思，后面用到再逐个解释。
# 但是绘图时这些必须引用。下面会解释下最关键的引用位置。
<image>
# Included from Circos distribution.
<<include etc/image.conf>>
file* = circos_label_band.png
</image>

# RGB/HSV color definitions, color lists, location of fonts, fill patterns.
# Included from Circos distribution.
<<include etc/colors_fonts_patterns.conf>>

# Debugging, I/O an dother system parameters
# Included from Circos distribution.
<<include etc/housekeeping.conf>>
```

显示染色体刻度信息，`chromosome_units`定义染色体一个单位的大小，缩写为`u`。若`chromosome_units=1000000`, 则`10u=10000000`。

![](http://www.ehbio.com/ehbio_resource/circos_label_band_tick.png)

```
# karyotype定义染色体的名字、ID、起始位置信息，是绘制图的根本
karyotype = data/karyotype/karyotype.human.txt

# 必须的部分，控制染色体信息显示
# 更多解释见
# http://circos.ca/documentation/tutorials/reference/ideogram/
<ideogram>

# 定义显示的染色体之间的间距，为图形半径的0.5% (r代表radius，半径)
<spacing>
default = 0.005r
</spacing>

# 染色体区域的绘制位置，默认所有染色体都处于远离圆心同样距离的位置
# 这里设置的是图形半径的0.9倍的位置
# 也可以设置绝对像素值
radius    = 0.9r

# 染色体区域的宽度，可以是相对图形半径，也可以说绝对像素值
thickness = 20p

# 染色体区域填充颜色
fill      = yes

# 染色体边的颜色和宽度
stroke_thickness = 2
stroke_color = black

# 显示染色体标签名字
# 更多label的调整见 
# http://circos.ca/documentation/tutorials/ideograms/labels/lesson
show_label = yes
label_font = default
# ideogram外圈再加总半径的0.05
label_radius = dims(ideogram,radius_outer) + 0.05r

# 如果想把label标记在圈里可以写，外圈半径+内圈半径除以2
# label_rdius = (dims(ideogram,radius_outer)+dims(ideogram,radius_inner))/2
label_size = 24
# label与圈平行
label_parallel   = yes
label_case = upper

# 显示karyotype中定义的细胞遗传学条带
# fill_bands=yes 表示使用预先定义的颜色
show_bands            = yes
fill_bands            = yes
band_transparency     = 4
</ideogram>

chromosomes_units           = 1000000
show_ticks          = yes
show_tick_labels    = yes

<ticks>
# ticks块定义了全局水平的tick的属性
# 更多解释见http://circos.ca/documentation/tutorials/ticks_and_labels/basics/
# ticks出现的位置
radius           = dims(ideogram,radius_outer)
# The label multiplier is the constant used to multiply the tick value to obtain the tick label. For example,  if the multiplier is 1e-6,  then the tick mark at position 10, 000, 000 will have a label of 10. The multiplier is applied to the raw tick value,  regardless of the value of chromosomes_unit. 
# multiplier是用于获得ticks label的，当前ticks对应的染色体位置乘以multiplier就得到ticks label
# 这个值的设置与chromosomes_units是没有任何关系的
# 比如当前位置是10,000,000, 乘以multiplier (1e-6)就是10
multiplier       = 1e-6
# ticks颜色、粗细、大小
color            = black
thickness        = 2p
size             = 15p
# 默认所有染色体都显示, 放置在ticks块中全局有效
chromosomes_display_default=yes
# 不在任何染色体显示, 放置在tick块中单个tick有效
# 单词拼错无效
#chromosomes_display_default=no

# 每个tick定义一种间隔，20u, 5u, 还可增加3u，4u等, 大的刻度会覆盖小的刻度
# 20u的间隔，定义大的ticks，并显示ticks_label
<tick>
# spacing定义多大间距一个tick
spacing        = 20u
show_label     = yes
label_size     = 20p
# label的偏移量
label_offset   = 10p
# %d, %.nf
format         = %d
</tick>

# 5u的间隔，定义小的ticks
<tick>
spacing        = 5u
color          = grey
size           = 10p
# 定义在哪些染色体显示ticks，哪些区域不显示
chromosomes=-hs1;-hs2:0-100;-hs3:100-)
</tick>


# 30u的间隔，定义中等的ticks
<tick>
chromosomes_display_default=no
spacing        = 30u
color          = red
size           = 15p
chromosomes=hs1
</tick>

</ticks>

################################################################
# The remaining content is standard and required. It is imported 
# from default files in the Circos distribution.
#
# These should be present in every Circos configuration file and
# overridden as required. To see the content of these files, 
# look in etc/ in the Circos distribution.

# 这些都是引用文件，暂时不去管什么意思，后面用到再逐个解释。
# 但是绘图时这些必须引用。下面会解释下最关键的引用位置。
<image>
# Included from Circos distribution.
<<include etc/image.conf>>
file* = circos_label_band_tick.png
</image>

# RGB/HSV color definitions, color lists, location of fonts, fill patterns.
# Included from Circos distribution.
<<include etc/colors_fonts_patterns.conf>>

# Debugging, I/O an dother system parameters
# Included from Circos distribution.
<<include etc/housekeeping.conf>>
```

在CIRCOS中`chromosome`表示`karyotype`文件中定义的染色体的序列结构信息。`ideogram`是`chromosome`信息的展示方式。一个染色体可以不展示，也有可能分成多段展示，可以选择图的位置，设置每个染色体的位置、相对大小。


```
# karyotype定义染色体的名字、ID、起始位置信息，是绘制图的根本
karyotype = data/karyotype/karyotype.human.txt

# 必须的部分，控制染色体信息显示
# 更多解释见
# http://circos.ca/documentation/tutorials/reference/ideogram/
<ideogram>

# 定义显示的染色体之间的间距，为图形半径的0.5% (r代表radius，半径)
<spacing>
default = 0.005r
</spacing>

# 染色体区域的绘制位置，默认所有染色体都处于远离圆心同样距离的位置
# 这里设置的是图形半径的0.9倍的位置
# 也可以设置绝对像素值
radius    = 0.9r

# 改变染色体在circos环中内半径大小
# 染色体区域的宽度，可以是相对图形半径，也可以说绝对像素值
thickness = 20p

# 染色体区域填充颜色
fill      = yes

# 染色体边的颜色和宽度
stroke_thickness = 2
stroke_color = black

# 显示染色体标签名字
# 更多label的调整见 
# http://circos.ca/documentation/tutorials/ideograms/labels/lesson
show_label = yes
label_font = default
# ideogram外圈再加总半径的0.05
label_radius = dims(ideogram,radius_outer) + 0.05r

# 如果想把label标记在圈里可以写，外圈半径+内圈半径除以2
# label_rdius = (dims(ideogram,radius_outer)+dims(ideogram,radius_inner))/2
label_size = 24
# label与圈平行
label_parallel   = yes
label_case = upper

# 显示karyotype中定义的细胞遗传学条带
# fill_bands=yes 表示使用预先定义的颜色
show_bands            = yes
fill_bands            = yes
band_transparency     = 4
</ideogram>

# 染色体大小调整
chromosomes_scale   = hs1=0.1r;hs14=0.06r;hs6=0.06r
# 个别染色体位置调整
chromosomes_radius  = hs14:0.8r;hs6:0.8r;hs1:0.7r

chromosomes_units           = 1000000
show_ticks          = yes
show_tick_labels    = yes

<ticks>
# ticks块定义了全局水平的tick的属性
# 更多解释见http://circos.ca/documentation/tutorials/ticks_and_labels/basics/
# ticks出现的位置
radius           = dims(ideogram,radius_outer)
# The label multiplier is the constant used to multiply the tick value to obtain the tick label. For example,  if the multiplier is 1e-6,  then the tick mark at position 10, 000, 000 will have a label of 10. The multiplier is applied to the raw tick value,  regardless of the value of chromosomes_unit. 
# multiplier是用于获得ticks label的，当前ticks对应的染色体位置乘以multiplier就得到ticks label
# 这个值的设置与chromosomes_units是没有任何关系的
# 比如当前位置是10,000,000, 乘以multiplier (1e-6)就是10
multiplier       = 1e-6
# ticks颜色、粗细、大小
color            = black
thickness        = 2p
size             = 15p
# 默认所有染色体都显示, 放置在ticks块中有效
chromosomes_display_default=yes
# 不在任何染色体显示, 放置在ticks块中有效
#chromosomes_display_default=no

# 每个tick定义一种间隔，20u, 5u, 还可增加3u，4u等, 大的刻度会覆盖小的刻度
# 20u的间隔，定义大的ticks，并显示ticks_label
<tick>
# spacing定义多大间距一个tick
spacing        = 20u
show_label     = yes
label_size     = 20p
# label的偏移量
label_offset   = 10p
# %d, %.nf
format         = %d
chromosomes=-hs1;-hs14;-hs6
</tick>

# 5u的间隔，定义小的ticks
<tick>
spacing        = 5u
color          = grey
size           = 10p
# 定义在哪些染色体显示ticks，哪些区域不显示
chromosomes=-hs1;-hs14;-hs6;-hs2:0-100;-hs3:100-)
</tick>


# 30u的间隔，定义中等的ticks
<tick>
chromosomes_display_default=no
spacing        = 30u
color          = red
size           = 15p
chromosomes=hs1
</tick>

</ticks>

################################################################
# The remaining content is standard and required. It is imported 
# from default files in the Circos distribution.
#
# These should be present in every Circos configuration file and
# overridden as required. To see the content of these files, 
# look in etc/ in the Circos distribution.

# 这些都是引用文件，暂时不去管什么意思，后面用到再逐个解释。
# 但是绘图时这些必须引用。下面会解释下最关键的引用位置。
<image>
# Included from Circos distribution.
<<include etc/image.conf>>
file* = circos_label_band_tick_chromove.png
#画图起始的位置，相对于三点钟方向
angle_offset* = 74
</image>

# RGB/HSV color definitions, color lists, location of fonts, fill patterns.
# Included from Circos distribution.
<<include etc/colors_fonts_patterns.conf>>

# Debugging, I/O an dother system parameters
# Included from Circos distribution.
<<include etc/housekeeping.conf>>
```

![](http://www.ehbio.com/ehbio_resource/circos_label_band_tick_chromove.png)

## CIRCOS错误信息

1. Dimension [$DIMS->{'ideogram'}{'default'}{`' radius_outer'`}] is `not defined` in expression [dims(ideogram, default,  radius_outer) + 0.05r]
	* `radius_outer`前面多了个空格

2. CONFIGURATION FILE ERROR; Circos could `not find` the configuration file [simple.confy]]
	* 配置文件不存在，或名字、路径写错了

3. Config::General: Block "<ticks>" has no EndBlock statement (level: 2, chunk 4191)!
	* 区块标签不成对

4. 设置的效果没有显示也没报销
    * 确认单词拼写是否有问题
	* 确认是否写入了正确的语句块内

5. Circos::Error::fatal_error('configuration', 'multivalue', 'angle_offset', 'image')
    * 没有强制覆盖默认值

## 生信宝典，一起学生信

[http://mp.weixin.qq.com/s/i71OMaUu6QtcY0pt1njHQA](http://mp.weixin.qq.com/s/i71OMaUu6QtcY0pt1njHQA)


## 生信宝典，生物信息学习系列教程，转录组，宏基因组，外显子组，R作图，Python学习，Cytoscape视频教程

[http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg](http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg)

## 生信宝典，最好的生物信息培训课程，培训课程资料

[www.ehbio.com/Training](www.ehbio.com/Training)
