---
title: bash数组操作
author: 悟道
layout: post
categories:
  - bash
---

1.数组声明和赋值

<pre class="brush: bash; title: ; notranslate" title="">&gt;&gt;&gt;declare -a array  # unnecessary
#The following 3 lines all can define an array and give values
&gt;&gt;&gt;array=(0 1 2)
&gt;&gt;&gt;array=([0]=0 [1]=1 [2]=v2)
&gt;&gt;&gt;array[0]=0

#以空白作为分隔符拆分字符串为数组
&gt;&gt;&gt;str="1 2 3"
&gt;&gt;&gt;array=($str)

#使用declare -p array 来查看是否数组和数组的结构
&gt;&gt;&gt;declare -p array  #输出为 declare -a arr='([0]="1" [1]="2" [2]="3")'

#使用其它分隔符拆分字符串为数组，需指定IFS
&gt;&gt;&gt;IFS=: array=($PATH)

#使用read -a 拆分字符串为数组
&gt;&gt;&gt;read -a array &lt;&lt;&lt;$str
&gt;&gt;&gt;declare -p array #输出为 declare -a arr='([0]="1" [1]="2" [2]="3")'

&gt;&gt;&gt;IFS=/ read -r -a PARTS &lt;&lt;&lt;$PWD 
</pre>

2.引用数组元素：

<pre class="brush: bash; title: ; notranslate" title="">$array  ${array}  ${array[0]}  #第0个元素
${array[n]}  #第n个元素（n从0开始计算）
</pre>

3.引用整个数组

<pre class="brush: bash; title: ; notranslate" title="">${array[*]}  ${array[@]}   这两种方式等同，会把数组展开。

${array[*]}  表示把数组拼接在一起的整个字符串，如果作为参数传递，
               会把整个字符串作为一个参数。

${array[@]}  如果作为参数传递，表示把数组中每个元素作为一个参数，
               数组有多少个元素，就会展开成多少个参数。
</pre>

3.计算数组元素长度：

<pre class="brush: bash; title: ; notranslate" title="">${#array[*]}  ${#array[@]}   不是 ${#array}，因为它等同于 ${#array[0]}
</pre>

4.遍历数组

<pre class="brush: bash; title: ; notranslate" title="">for i in "${array[@]}"; do echo $i; done
</pre>

5.

6.

参考：http://codingstandards.iteye.com/blog/1164910
