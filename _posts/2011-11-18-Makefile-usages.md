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

1. 列出目录内所有文件

{% highlight bash %}
shell := /bin/bash
name=$(shell ls)
{% endhighlight %}

2. 使用多变量定义为命令名字

{% highlight bash %}
$(name):
    @echo $@
{% endhighlight %}

3. 命令名字中不能出现函数

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

4. make在ubuntu中默认使用dash执行脚本命令，因此可能会出一些问题，可以自己制定使用的shell类型

{% highlight bash %}
shell := /bin/bash

$(shell paste *.file)
{% endhighlight %}

5. 自定义隐式命令

{% highlight bash %}
%.protein:%.gene; 
    translate $< >$@
{% endhighlight %}

6. foreach的使用

{% highlight bash %} 
$(foreach <var>;,<list>;,<text>;)
$(line).map:
		echo $@
name=a b c
$(foreach var, $(nameL), make $(var).map line=$(var);) #将执行make a.map line=a; make b.map line=b; make c.map line=c
{% endhighlight %}

把参数<list>中的单词逐一取出放到参数<var>所指定的变量中，然后再执行<text>所包含的表达式。
每一次<text>会返回一个字符串，循环过程中，<text>的所返回的每个字符串会以空格分隔
最后当整个循环结束时，<text>所返回的每个字符串所组成的整个字符串（以空格分隔）将会是foreach函数的返回值。 
所以，<var>最好是一个变量名，<list>可以是一个表达式，而<text>中一般会使用<var>这个参数来依次枚举<list>中的单词。举个例子：
names := a b c d
files := $(foreach n,$(names),$(n).o)
上面的例子中，$(name)中的单词会被挨个取出，并存到变量“n”中，“$(n).o”每次根据“$(n)”计算出一个值，
这些值以空格分隔，最后作为foreach函数的返回，所以，$(files)的值是“a.o b.o c.o d.o”。

7. Make中增加判断语句，控制执行的命令

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


8. 在Makefile中使用重定向时要定义SHELL的类型

{% highlight bash %}
SHELL := /bin/bash -e -o pipefail

diff <(sort -u a) <(sort -u b)
{% endhighlight %}

9. 字符串操作函数
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

9. 获取文件路径
{% highlight bash %}
annovar_dir=$(dir $(shell which annotate_variation.pl))
{% endhighlight %}


10. Makefile处理多级目录
方法1. 在每个目录下建立Makefile文件,在最外面的Makefile中cd到指定目录中执行$(MAKE),也是可以加参数的

方法2:就是查找每个需要编译的文件,然后进行编译,下面是一个例子

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

http://linux.chinaunix.net/bbs/thread-988337-1-1.html


22. 参考资料

http://www.jfranken.de/homepages/johannes/vortraege/make.en.html【[make.en][2]】

 [1]: http://wiki.ubuntu.org.cn/%E8%B7%9F%E6%88%91%E4%B8%80%E8%B5%B7%E5%86%99Makefile:%E4%BD%BF%E7%94%A8%E6%9D%A1%E4%BB%B6%E5%88%A4%E6%96%AD
 [2]: http://210.75.224.29/wordpress/wp-content/uploads/2012/04/make.en_.pdf

