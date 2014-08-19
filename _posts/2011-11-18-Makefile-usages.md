---
title: Tips for Makefile usages
layout: post
categories:
    - Makefile
    - letter
tags:
    - bash
    - Makefile
---

* 列出目录内所有文件
{% highlight bash %}
shell := /bin/bash
name=$(shell ls)
{% endhighlight %}

* 使用多变量定义为命令名字
{% highlight bash %}
$(name):
	@echo $@
{% endhighlight %}

* 命令名字中不能出现函数

正确的：

{% highlight bash %}
nameN=$(addsuffix .N, $(name))

$(nameN):
    @echo $@
{% endhighlight %}

错误的：

{% highlight bash %}
$(addsuffix .N, $(name)):
    @echo $@
{% endhighlight %}

* make在ubuntu中默认使用dash执行脚本命令，因此可能会出一些问题，可以自己制定使用的shell类型

{% highlight bash %}
shell := /bin/bash

$(shell paste *.file)
{% endhighlight %}

* 自定义隐式命令

{% highlight bash %}
%.protein:%.gene; 
    translate $< >$@
{% endhighlight %}

* foreach的使用

{% highlight bash %} 
$(foreach <var>;,<list>;,<text>;)
$(line).map:
		echo $@
name=a b c
$(foreach var, $(nameL), make $(var).map line=$(var);) #将执行make a.map line=a; make b.map line=b; make c.map line=c
{% endhighlight %}


* Make中增加判断语句，控制执行的命令

{% highlight bash %}
ifeq ($(gcc),cc )  
    <> 
else 
    <> 
endif
ifdef $gcc 
    <> 
endif
ifndef $gcc 
    <>   
endif
{% endhighlight %}


* 在Makefile中使用重定向时要定义SHELL的类型

{% highlight bash %}
SHELL := /bin/bash -e -o pipefail

diff <(sort -u a) <(sort -u b)
{% endhighlight %}

* 字符串操作函数
{% highlight bash %}
nameL=a b c
#计算单词个数
$(words $(nameL)) #返回值为3
$(words a b c) #返回值为3
#测试输出返回值
count=$(words a b c)
echo_count:
		echo $(count)
#取出特定单词
$(word 2, $(nameL)) #取出第二个单词 b
#排序多个单词
$(sort $(nameL)) #排序
$(sort c b a) #输出为a b c
{% endhighlight %}

* Substitute blank with comma in Makefile
{% highlight bash %}
#define a variable represent comma
comma:= ,
#define an empty variable
empty:=
#define a space by two empty variable and one blank
space:= $(empty) $(empty)
foo:= a b c
#no space after each comma especially the last one
bar:= $(subst $(space),$(comma),$(foo))
# bar is now `a,b,c'.
{% endhighlight %}

* 获取文件路径
{% highlight bash %}
annovar_dir=$(dir $(shell which annotate_variation.pl))
{% endhighlight %}


* Makefile处理多级目录

    * 方法1. 在每个目录下建立Makefile文件,在最外面的Makefile中cd到指定目录中执行$(MAKE),也是可以加参数的

    * 方法2:就是查找每个需要编译的文件,然后进行编译,下面是一个例子

{% highlight bash %}
MW_DIR=$(PWD)  
INCLUDE = -I$(MW_DIR)/include  
INCLUDE+= -I.  
#LIBPATH=-L $(MW_DIR)/lib     //如果有库文件,可以这样指定  
#LIB= -lpthread                        //libpthread.a  
CC=gcc  
CFLAGS=-DHI_DEBUG -g -Wall

//加入内部的头文件  
SAMDIR=$(MW_DIR)/src  
SAMINCH=$(shell find $(SAMDIR) -name &#8216;*.h&#8217;)  
SAMINCDIR=$(dir $(SAMINCH))  
INCLUDE+= $(foreach temp,$(SAMINCDIR), -I$(temp))

//查找到需要编译的C文件  
SRC=$(shell find $(SAMDIR) -name &#8216;*.c&#8217;)  //子目录的C文件  
SRC+=$(wildcard *.c)  //当前目录中的C文件

APP=$(SRC:%.c=%)  //得到AP文件

all  :  $(APP)

$(APP): %: %.c  
$(CC) $(CFLAGS) -o  $@ $< $(INCLUDE) $(LIBPATH) $(LIB)  
clean:  
rm -fr $(APP)

{% endhighlight %}


* 参考资料

http://www.jfranken.de/homepages/johannes/vortraege/make.en.html

http://linux.chinaunix.net/bbs/thread-988337-1-1.html

[1]: http://wiki.ubuntu.org.cn/%E8%B7%9F%E6%88%91%E4%B8%80%E8%B5%B7%E5%86%99Makefile:%E4%BD%BF%E7%94%A8%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD
[2]: http://210.75.224.29/wordpress/wp-content/uploads/2012/04/make.en_.pdf

