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
* 如果有`index.Rmd`，`index.Rmd`总是出现在第一个位置。通常index.Rmd里面也需要有一章节，如果不需要对这一章节编号的话，可以写作`# Preface {-}`, 关键是`{-}`。
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

  ```{r setup, include=FALSE}
  knitr::opts_chunk$set(echo = FALSE, fig.align="center", out.width="95%", fig.pos='H')
  # knitr::opts_chunk$set(cache = FALSE, autodep=TRUE)
  set.seed(0304)
  ```
  ~~~~~~~~~~

##### 插入并引用图片(外部图片)

插入图片最好使用`knitr::include_graphics`，可以同时适配HTML和PDF输出。另外当目录下同时存在`name1.png`和`name1.pdf`文件时，会自动选择在HTML展示`name1.png`文件，在`PDF`输出中引入`name1.pdf`格式的文件。

图的标签为`fig-name`(不能有下划线)，在引用时需使用如下格式`\@ref(fig:fig-name)`，且`fig.cap`也要设置内容。

多张图可以同时展示，图的名字以vector形式传给`include_graphics`，需要设置`out.width=1/number-pics` 和 `fig.show="hold"`。


~~~~
Insert a single pic and refer as Figure \@ref(fig:fig-name). `echo=FALSE` will hide the code block and display the output of `r` command only. These options can be set globally as indicated below.

```{r fig-name, fig.cap="Markdown supported string as caption", fig.align="center", echo=FALSE}
knitr::include_graphics("images/1.png")
```

Suppose we have 3 pictures in `images` folder with names as `Fig1_a`, `Fig1_b`,  `Fig1_c`,  we can refer to them using Figure \@ref(fig:fig1).

```{r fig1, fig.cap="3 sub-plots.", fig.align="center", out.width=33%, fig.show="hold"}
fig1 = list.files("images", pattern="Fig1_.*", full.names=T)
knitr::include_graphics(fig1)
```

Another way of including two pics.

```{r fig-name2,  out.width="49%", fig.show="hold", fig.cap="Markdown supported string as caption",  fig.align="center", echo=FALSE}
knitr::include_graphics(c("images/1.png", "images/2.png"))
```
~~~~~~~~~~~~~~~~~~~~

如果图或表的标题中有Markdown语法，输出为HTML时是可以正确解析的，但是输出为PDF时却不可以。这时可以使用`Text Reference`。当图或表的标题太长时，也可以使用`Text Reference`引用一段话作为图和表的标题。

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here is normal text.

(ref:pic-label) This line can be referred in **fig.cap** and markdown syntax is supported for both `HTML` and `PDF` output.

```{r pic-label, fig.cap="(ref:pic-label)"}
knitr::include_graphics("images/1.png")
```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

##### 插入并引用表格(外部表格)

外部表格的名字中必须包含`tab:`, 然后是表格的实际名字，格式为`(\#tab:table-name)`; 引用时使用`Table \@ref(tab:table-name)`。 表格名字中不能有下划线。

```
Check Table \@ref(tab:seq-sum) for detail.

Table: (\#tab:seq-sum) Summary of sequencing reads 测序量总结 (对于双端测序,  *\_1* 表示左端reads, *\_2* 表示右端reads) 

----------------------------------------------------------------------
Sample     Total reads     Total bases Sequence length (nt)     GC content (%) Encoding               
-------- ------------- --------------- ---------------------- ---------------- -----------------------
T8_1        37,106,941   5,566,036,721 138-150                              47 Sanger / Illumina 1.9  

T8_2        37,106,941   5,566,034,285 138-150                              47 Sanger / Illumina 1.9  
----------------------------------------------------------------------
```

##### 插入并引用表格(内部表格)

插入表格推荐使用`knitr::kable`，只要提供数据矩阵，用`r`读取就可以了。

~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check Table \@ref(tab:table-id) for detail.

```{r table-id, include=FALSE}
a <- as.data.frame(matrix(rnorm(20), nrow=4))
knitr::kable(a, caption="Test table",  booktabs=TRUE)
```
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

##### 插入脚注

`text^[footnote]` is used to get the footnote.

```
where `type` may be `article`,  `book`,  `manual`,  and so on.^[The type name is case-insensitive,  so it does not matter if it is `manual`,  `Manual`,  or `MANUAL`.]
```

##### 插入引文

假如我们的`bib`文件中内容如下，如果我们要引用这个文章，只要写 `[@chen_m6a_2015]`就可以了。

```

@article{chen_m6a_2015,
	title = {m6A {RNA} {Methylation} {Is} {Regulated} by {MicroRNAs} and {Promotes} {Reprogramming} to {Pluripotency}},
	volume = {16},
	issn = {1934-5909, 1875-9777},
	url = {http://www.cell.com/cell-stem-cell/abstract/S1934-5909(15)00017-X},
	doi = {10.1016/j.stem.2015.01.016},
	language = {English},
	number = {3},
	urldate = {2016-12-08},
	journal = {Cell Stem Cell},
	author = {Chen, Tong and Hao, Ya-Juan and Zhang, Ying and Li, Miao-Miao and Wang, Meng and Han, Weifang and Wu, Yongsheng and Lv, Ying and Hao, Jie and Wang, Libin and Li, Ang and Yang, Ying and Jin, Kang-Xuan and Zhao, Xu and Li, Yuhuan and Ping, Xiao-Li and Lai, Wei-Yi and Wu, Li-Gang and Jiang, Guibin and Wang, Hai-Lin and Sang, Lisi and Wang, Xiu-Jie and Yang, Yun-Gui and Zhou, Qi},
	month = mar,
	year = {2015},
	pmid = {25683224},
	pages = {289--301},
}
```

#### 准备YML配置文件

##### _bookdown.yml

配置输入和输出文件参数。

```
book_filename: "输出文件的名字" 
output_dir: "输出目录的名字，默认_book"
language:
  ui:
      chapter_name: "" 
```

##### _output.yml

配置产生输出文件的命令行参数。

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

* 配置全局变量自适应`HTML`和`PDF`输出

  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  ```{r setup, include=FALSE}
  library(knitr)
  output <- opts_knit$get("rmarkdown.pandoc.to")
  html = FALSE
  latex = FALSE
  opts_chunk$set(echo = FALSE, fig.align="center", fig.show="hold")
  if (output=="html") {
  	html = TRUE
  }
  if (output=="latex") {
  	opts_chunk$set(out.width="95%", out.height='0.7\\textheight', out.extra='keepaspectratio', fig.pos='H')
  	latex = TRUE
  }
  #knitr::opts_chunk$set(cache = FALSE,  autodep=TRUE)
  set.seed(0304)
  ```
  
  Below text will only appear in HTML output.

  ```{asis, echo=html}
  
  # EHBIO Gene Technology {-}
  
  ```
  
  Below command will only be executed and displayed in HTML output.

  ```{r cover, eval=html, out.width="99%"}
  knitr::include_graphics("ehbio/cover.png")
  ```
  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* 保留生成的markdown文件

  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  # add below lines to last Rmd file
  ```{r, include=FALSE}
  file.rename(from="bookdown_file_name.md",  to="bookdown_file_name.saved.md")
  ```
  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### 预览生成的WEB文件

如果没有安装Rstudio，可以在生成的book目录(有`index.html`的目录)下运行`python -m SimpleHTTPServer 11521`(11521为端口号，一般选较大值避免冲突), 然后就可以在浏览器输入网址`http://server-ip:11521`来访问了。

### A template Rmd

Use [bookdown_init_general.py -o test -t '我的文档' -a " 作者1 - 北京;2 - 南京;1521082" -b a.bib](https://github.com/Tong-Chen/NGS/blob/master/bookdown_init_general.py) to generate a minimal template.

### References

* <https://bookdown.org/yihui/bookdown/get-started.html>
* <https://github.com/rstudio/bookdown/tree/master/inst/examples>
* <http://stackoverflow.com/questions/25236850/how-to-set-different-global-options-in-knitr-and-rstudio-for-word-and-html>
* Multiple output with different configs <https://github.com/yihui/knitr/issues/1145>
* Multiple output with different configs <https://github.com/yihui/knitr/issues/114://github.com/rstudio/rmarkdown/issues/614>
* Citation style <http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html>
