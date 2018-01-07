---
title: 一个函数抓取代谢组学权威数据库HMDB的所有表格数据
author: RPM
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---


爬虫是都不陌生的一个概念，比如百度、谷歌都有自己的爬虫工具去抓取网站、分析、索引，方便我们的查询使用。

在我们浏览网站、查询信息时，如果想做一些批量的处理，也可以去分析网站的结构、抓取网页、提取信息，然后就完成了一个小爬虫的写作。

网页爬虫需要我们了解`URL`的结构、`HTML`语法特征和结构，以及使用合适的抓取、解析工具。我们这篇先看一个简单的处理，给一个直观的感受：一个函数抓取网页的表格。以后再慢慢解析如何更加定制的获取信息。

HMDB (人类代谢组数据库)收录了很多代谢组的数据，用于代谢组学、临床化学、生物标志物开啊和基本教育等。数据联通化学、临床、分子生物学3个层次，共有**114,099**个代谢物。

网站提供了多种浏览和查询功能，可以关注不同的疾病、通路、BMI、年龄、性别相关代谢组学。

![](http://www.ehbio.com/ehbio_resource/hmdb_browse_search.png)

下图展示的是BMI相关代谢物的数据。

![](http://www.ehbio.com/ehbio_resource/hmdb_table.png)

如果我们想把这个表格下载下来，一个办法是一页页的拷贝，大约拷贝十几次，工作量不算太大，但有些无趣。另外一个办法就是这次要说的抓取网页。

R的`XML`包中有个函数`readHTMLTable`专用于识别HTML中的表格 (**table**标签)，从而提取元素。具体使用如下： 

```r
# Load the package required to read website
library(XML)

# wegpage address 
url <- "http://www.hmdb.ca/bmi_metabolomics"

# header=T, 使第一行或thead属性的内容为标题
df1 <- readHTMLTable(url, header=T, stringsAsFactors = F)

# 初次使用，不了解输出格式时可使用str查看
str(df1)
```

```
> str(df1)
List of 1
 $ NULL:'data.frame':	25 obs. of  7 variables:
  ..$ V1: chr [1:25] "Butyrylcarnitine (HMDB0002013)" "Alpha-ketoisovaleric acid (HMDB0000019)" "2-Hydroxy-3-methylbutyric acid (HMDB0000407)" "3-Methyl-2-oxovaleric acid (HMDB0000491)" ...
  ..$ V2: chr [1:25] "" "" "" "" ...
  ..$ V3: chr [1:25] "Increase" "Increase" "Increase" "Increase" ...
  ..$ V4: chr [1:25] "Blood" "Blood" "Blood" "Blood" ...
  ..$ V5: chr [1:25] "9.95e-10" "2.87e-08" "1.19e-05" "1.68e-05" ...
  ..$ V6: chr [1:25] "25254000" "25254000" "25254000" "25254000" ...
  ..$ V7: chr [1:25] "details" "details" "details" "details" ...
```

```r
# The readHTMLTable returns list, we need to extract our data frame. In this example, the first element is our data frame, so we can extract it like this:
head(df1[[1]])  # extract the first element of list
#df1[["NULL"]]  # extract list element based on element names (第一个元素的名字是NULL)
```

```
1               Butyrylcarnitine (HMDB0002013)    Increase Blood 9.95e-10
2      Alpha-ketoisovaleric acid (HMDB0000019)    Increase Blood 2.87e-08
3 2-Hydroxy-3-methylbutyric acid (HMDB0000407)    Increase Blood 1.19e-05
4     3-Methyl-2-oxovaleric acid (HMDB0000491)    Increase Blood 1.68e-05
5                    Ketoleucine (HMDB0000695)    Increase Blood 6.05e-05
6   (S)-3-Hydroxyisobutyric acid (HMDB0000023)    Increase Blood 6.88e-05
        V6      V7
1 25254000 details
2 25254000 details
3 25254000 details
4 25254000 details
5 25254000 details
6 25254000 details
```

这样我们就获得了第一页的表格，如果想获得随后的页的呢？鼠标移动经过分页的标签，可以看到**URL**的规律。

![](http://www.ehbio.com/ehbio_resource/hmdb_bmi_p4.png)

`http://www.hmdb.ca/bmi_metabolomics?page=`**num**,每一页就是变换下**num**；对首页来说，可以写`page=1`也可以省略，为了批量，一般写上。

```r
# 294是在网页直接看到的总条数，25是每页显示的条数。(也是可以自动解析判断的)
pages = 1:ceiling(294 / 25)

url <- "http://www.hmdb.ca/bmi_metabolomics?page="

# 获得URL集合
url_all <- paste(url, pages, sep="")

a = sapply(url, readHTMLTable, header=T, stringsAsFactors=F)

# 合并获得的结果
b = do.call("rbind",a)

# 重命名行
rownames(b) <- 1:nrow(b)
```

这样就获得了所有的表格。

有两点需要注意

1. 为了给被抓取的网站带去较大的访问压力，每抓取一次，最后间歇一段时间。这需要我们自定义一个函数，封装下`readHTMLTable`。
2. HMDB数据库提供了全数据下载功能，相比于抓取，下载下来数据，自己筛选合并是更好的方式。

![](http://www.ehbio.com/ehbio_resource/hmdb_downloads.png)

### 问题解决

可能是因为网速或其它问题，有时直接把`url`提供给`readHTMLTable`不一定可以获取结果，下面提供了2额外的方式，供使用。

```
# Load the package required to read website
library(XML)

# wegpage address 
url <- "http://www.hmdb.ca/bmi_metabolomics"

# method one: for people who is luckiest (not me, so sad)
df1 <- readHTMLTable(url, header=T, stringsAsFactors = F)
  # Error: failed to load external entity "url"

# method two: use RCurl package, for people who is much luckier (only work on my laptop, not the computer in the office, crying)
library(RCurl)
xmldoc <- getURL(url)
df2 <- readHTMLTable(xmldoc, stringsAsFactors = F)

# method three: use httr package, for people who is not lucky
library(httr)
tabs <- GET(url)
df3 <- readHTMLTable(rawToChar(tabs$content), as.data.frame = T, stringsAsFactors = F)
```


### 便捷链接 

* [R语言学习 - 基础概念和矩阵操作](http://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&amp;mid=2247483891&amp;idx=1&amp;sn=40daf6435398c4d9a41f332e9bba4915&amp;chksm=ec0dc479db7a4d6fec413bfb90a4660eb035b440d2bbee998114f7af29e3b3338a8adf62540a#rd)
* [VIM正则表达式获取生信宝典公众号的文章列表](https://mp.weixin.qq.com/s?__biz=MzI5MTcwNjA4NQ==&mid=2247484250&idx=1&sn=d4759dc05a55643549646c77318c4f96&chksm=ec0dc6d0db7a4fc64791896914547b5ce818e8bd3cca98f0fb7bf6ebd9029fe6fd08a4d55255#rd)
* [R Error using readHTMLTable](https://stackoverflow.com/questions/17045107/r-error-using-readhtmltable) 
* [Extract web pages](http://chenyuan.date/2017/10/Extract-data-from-webpage/)
