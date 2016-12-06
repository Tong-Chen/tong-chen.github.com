---
title: Bookdown usage
author: ct
layout: post
description:
modified:
categories: [Bioinformatics]
tags: [bookdown]
---

Here lists the usage of [`bookdown`](https://bookdown.org/yihui/bookdown/get-started.html) for writing documents.

### Get required information

#### Install required software

`Rstudio`或`Pandoc`二选一, `bookdown`必须安装。

* Install [`Rstudio (version>1.0.0)`](https://www.rstudio.com/products/rstudio/download/)

* Install [`Pandoc (version>1.17.0.2)`](http://www.pandoc.org)或者参照[here]({{ site.url }}/collections/Linux_tips)

* In R `install.packages("bookdown")`

#### Get a demo example

Clone or download en example from <https://github.com/rstudio/bookdown-demo>.

#### Build the book

run `bash _build.sh` in the downloaded demo example, then the books will be in `_book` dir.

The content of `_build.sh` is:

```
#!/bin/sh
Rscript -e "bookdown::render_book('index.Rmd', 'bookdown::gitbook')"
Rscript -e "bookdown::render_book('index.Rmd', 'bookdown::pdf_book')"
```

### Customize our bookdown

#### 准备`Rmd`文件

##### 基本规则

* 一个典型的`bookdown`文档包含多个章节，每个章节在一个`R Markdown`文件里面 (文件的语法可以是`pandoc`支持的`markdown`语法，但后缀必须为`Rmd`)。
* 每一个章节都必须以`# Chapter title`开头。后面可以跟一段概括性语句，概述本章的内容，方便理解，同时也防止二级标题出现在这一页。默认系统会按照文件名的顺序合并`Rmd`文件。
* 另外章节的顺序也可在`_bookdown.yml`文件中通过`rmd_files:["file1.Rmd", "file2.Rmd", ..]`指定。
* 如果有`index.Rmd`，`index.Rmd`总是出现在第一个位置。通常index.Rmd里面也需要有一章节，如果不需要对这一章节编号的话，可以写作`# Preface {-}`。
* 在第一个出现的`Rmd`文件中，可以定义`Pandoc`相关的`YAML metadata`, 比如标题、作者、日期等(去掉#及其后的内容)。
  
  ~~~~
  ```
  title: "My book"
  author: #可以写多行信息，都会被当做Author处理
  - "CT"
  - "CY"
  - "chentong_biology@163.com"
  date: "`r Sys.Date()`"
  documentclass: article #可以为book或article
  # 如果需要引用参考文献，则添加下面三行内容
  bibliography: [database.bib]  #指定存储参考文献的bib文件，endote或zotero都可以导出这种引文格式
  biblio-style: apalike  #设定参考文献显示类型
  link-citations: yes
  ```

  ```{r setup,   include=FALSE}
  knitr::opts_chunk$set(echo = FALSE, fig.align="center", out.width="95%", fig.pos='H')
  # knitr::opts_chunk$set(cache = FALSE, autodep=TRUE)
  set.seed(0304)
  ```
  ~~~~~~~~~~

##### 插入并引用图片(外部图片)

插入图片最好使用`knitr::include_graphics`，可以同时适配HTML和PDF输出。另外当目录下同时存在`png`和`pdf`文件时，会自动选择在HTML展示`png`文件，在`PDF`输出中引入`pdf`格式的文件。

图的名字为`fig-name`，在引用时需使用如下格式`\@ref(fig:<here is fig-name>)`。名字中不能有下划线。

多张图可以同时展示，图的名字以vector形式传给`include_graphics`，需要设置`out.width=1/number-pics` 和 `fig.show="hold"`。

~~~~
Ref Figure \@ref(fig:fig-name).
# Single pic
```{r fig-name,  fig.cap="Markdown supported string as caption",  fig.align="center", echo=FALSE}
knitr::include_graphics("images/1.png")
```

# Multiple pics
```{r fig-name2,  out.width="49%", fig.show="hold", fig.cap="Markdown supported string as caption",  fig.align="center", echo=FALSE}
knitr::include_graphics(c("images/1.png", "images/2.png"))
```
~~~~~~~~~~~~~~~~~~~~

##### 插入并引用表格(外部表格)

外部表格的名字中必须包含`tab:`, 后面跟着的是表格的实际名字，格式未`(\#tab:table-name)`; 引用时使用`Table \@ref(tab:table-name)`。 表格名字中不能有下划线。

```
Check Table \@ref(tab:label) for detail.

Table: (\#tab:label) Summary of sequencing reads 测序量总结 (对于双端测序,  *\_1* 表示左端reads, *\_2* 表示右端reads) 

----------------------------------------------------------------------
Sample     Total reads     Total bases Sequence length (nt)     GC content (%) Encoding               
-------- ------------- --------------- ---------------------- ---------------- -----------------------
T8_1        37,106,941   5,566,036,721 138-150                              47 Sanger / Illumina 1.9  

T8_2        37,106,941   5,566,034,285 138-150                              47 Sanger / Illumina 1.9  
----------------------------------------------------------------------
```

##### 插入并引用表格(内部表格)

~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```{r table-id, include=FALSE}
a <- as.data.frame(matrix(rnorm(20), nrow=4))
knitr::kable(a, caption="Test table",  booktabs=TRUE)
```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

##### 插入引文

假如我们的`bib`文件中内容如下，如果我们要引用这个文章，只要写 `[@guo_transcriptome_2015]`就可以了。

```

@article{guo_transcriptome_2015,
	title = {The {Transcriptome} and {DNA} {Methylome} {Landscapes} of {Human} {Primordial} {Germ} {Cells}},
	volume = {161},
	issn = {1097-4172},
	doi = {10.1016/j.cell.2015.05.015},
	language = {eng},
	number = {6},
	journal = {Cell},
	author = {Guo, Fan and Yan, Liying and Guo, Hongshan and Li, Lin and Hu, Boqiang and Zhao, Yangyu and Yong, Jun and Hu, Yuqiong and Wang, Xiaoye and Wei, Yuan and Wang, Wei and Li, Rong and Yan, Jie and Zhi, Xu and Zhang, Yan and Jin, Hongyan and Zhang, Wenxin and Hou, Yu and Zhu, Ping and Li, Jingyun and Zhang, Ling and Liu, Sirui and Ren, Yixin and Zhu, Xiaohui and Wen, Lu and Gao, Yi Qin and Tang, Fuchou and Qiao, Jie},
	month = jun,
	year = {2015},
	pmid = {26046443},
	pages = {1437--1452}
}
```

#### 准备YML配置文件

##### _bookdown.yml

```
book_filename: "输出文件的名字" 
output_dir: "输出目录的名字，默认_book"
language:
  ui:
      chapter_name: "" 
```

##### _output.yml

```
bookdown::pdf_book:
  template: ehbio.tex #使用自己定制的pandoc latex模板
  includes: # or only customize part latex module
    in_header: preamble.tex
    before_body: latex/before_body.tex
    after_body: latex/after_body.tex
  latex_engine: xelatex
  citation_package: natbib
  keep_tex: yes
  pandoc_args: --chapters
  toc_depth: 3
  toc_unnumbered: no
  toc_appendix: yes
  quote_footer: ["\\VA{", "}{}"]
bookdown::epub_book:
  stylesheet: css/style.css
bookdown::gitbook:
  css: style.css
  split_by: section
  config:
    toc:
      collapse: none
      before: | #设置toc开头和结尾的链接
          <li><a href="http://www.ehbio.com"><img src="ehbio_logo.png" width="100%"></a></li>
      after: |
          <li><a href="mailto:ct@ehbio.com" target="blank">ct@ehbio.com</a></li>
    download: [pdf, epub, mobi]
    edit: https://github.com/rstudio/bookdown/edit/master/inst/examples/%s
    sharing:
	  twitter: no
      github: no
      facebook: no
```


#### 其它定制

* 不同的文件分别用于`html`和`pdf`输出
 
  ```
  # in _bookdown.yml 
  rmd_files:
    html: ["index.Rmd", "file2.Rmd"]
	latex: ["index_pdf.Rmd", "file3.Rmd"]
  # Different render way

  #!/bin/sh
  Rscript -e "bookdown::render_book('index.Rmd', 'bookdown::gitbook')"
  Rscript -e "bookdown::render_book('index_pdf.Rmd', 'bookdown::pdf_book')"
  ```

### 预览生成的WEB文件

如果没有安装Rstudio，可以在生成的book目录下(有`index.html`)的目录下运行`python -m SimpleHTTPServer 11521`(11521为端口号，一般选较大值避免冲突), 然后就可以在浏览器输入网址`http://server-ip:11521`来访问了。


### References

* <https://bookdown.org/yihui/bookdown/get-started.html>
* <https://github.com/rstudio/bookdown/tree/master/inst/examples>
