---
title: Use AWK
layout: post
categories:
  - bash
  - letter
tags:
  - awk
  - bash
---

awk提供了许多强大的字符串函数，见下表：  
awk内置字符串函数

<table border="0" cellspacing="0" cellpadding="3">
  <tr>
    <td width="50%">
      gsub(r,s)
    </td>
    
    <td width="50%">
      在整个$0中用s替代r
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      gsub(r,s,t)
    </td>
    
    <td width="50%">
      在整个t中用s替代r
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      index(s,t)
    </td>
    
    <td width="50%">
      返回s中字符串t的第一位置
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      length(s)
    </td>
    
    <td width="50%">
      返回s长度
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      match(s,r)
    </td>
    
    <td width="50%">
      测试s是否包含匹配r的字符串
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      split(s,a,fs)
    </td>
    
    <td width="50%">
      在fs上将s分成序列a
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      sprint(fmt,exp)
    </td>
    
    <td width="50%">
      返回经fmt格式化后的exp
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      sub(r,s)
    </td>
    
    <td width="50%">
      用$0中最左边最长的子串代替s
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      substr(s,p)
    </td>
    
    <td width="50%">
      返回字符串s中从p开始的后缀部分
    </td>
  </tr>
  
  <tr>
    <td width="50%">
      substr(s,p,n)
    </td>
    
    <td width="50%">
      返回字符串s中从p开始长度为n的后缀部分
    </td>
  </tr>
</table>

详细说明一下各个函数的使用方法。

gsub函数有点类似于sed查找和替换。它允许替换一个字符串或字符为另一个字符串或字符，并以正则表达式的形式执行。第一个函数作用于记录$0，第二个gsub函数允许指定目标，然而，如果未指定目标，缺省为$0。  
index(s,t)函数返回目标字符串s中查询字符串t的首位置。length函数返回字符串s字符  
长度。match函数测试字符串s是否包含一个正则表达式r定义的匹配。split使用域分隔符fs将  
字符串s划分为指定序列a。sprint函数类似于printf函数(以后涉及)，返回基本输出格式fmt的  
结果字符串exp。sub(r,s)函数将用s替代$0中最左边最长的子串，该子串被(r)匹配。  
sub(s,p)返回字符串s在位置p后的后缀。substr(s,p,n)同上，并指定子串长度为n。  
现在看一看awk中这些字符串函数的功能。

1.gsub  
要在整个记录中替换一个字符串为另一个，使用正则表达式格式，/目标模式/，替换模式  
/。例如改变学生序号4842到4899：

$ awk &#8216;gsub(&#8217;4842/, 4899) {print $0}&#8217; grade.txt  
J.Troll 07/99 4899 Brown-3 12 26 26

2.index  
查询字符串s中t出现的第一位置。必须用双引号将字符串括起来。例如返回目标字符串  
Bunny中ny出现的第一位置，即字符个数。

$ awk &#8216;BEGIN {print index(&#8220;Bunny&#8221;, &#8220;ny&#8221;)} grade.txt  
4

3.length  
返回所需字符串长度，例如检验字符串J.Troll返回名字及其长度，即人名构成的字符个  
数。

$ awk &#8216;$1==&#8221;J.Troll&#8221; {print length($1) &#8221; &#8220;$1}&#8217; grade.txt  
7 J.Troll

还有一种方法，这里字符串加双引号。

$ awk &#8216;BEGIN {print length(&#8220;A FEW GOOD MEN&#8221;)}&#8217;  
14

4.match  
match测试目标字符串是否包含查找字符的一部分。可以对查找部分使用正则表达式,返  
回值为成功出现的字符排列数。如果未找到,返回0,第一个例子在ANCD中查找d。因其不  
存在,所以返回0。第二个例子在ANCD中查找D。因其存在,所以返回ANCD中D出现的首位  
置字符数。第三个例子在学生J.Lulu中查找u。

$ awk &#8216;{BEGIN {print match(&#8220;ANCD&#8221;, /d/)}&#8217;  
  
$ awk &#8216;{BEGIN {print match(&#8220;ANCD&#8221;, /C/)}&#8217;  
3  
$ awk &#8216;$1==&#8221;J.Lulu&#8221; {print match($1, &#8220;u&#8221;)} grade.txt  
4

5.split  
使用split返回字符串数组元素个数。工作方式如下：如果有一字符串,包含一指定分隔  
符-,例如AD2-KP9-JU2-LP-1,将之划分成一个数组。使用split,指定分隔符及数组名。此  
例中,命令格式为(&#8220;AD2-KP9-JU2-LP-1&#8243;,parts_array,&#8221;-&#8221;),split然后返回数组下标数,这  
里结果为4。  
还有一个例子使用不同的分隔符。

$ awk &#8216;{BEGIN {print split(&#8220;123#456#678&#8243;, myarray, &#8220;#&#8221;)}&#8217;  
3

这个例子中,split返回数组myarray的下标数。数组myarray取值如下：

Myarray[1]=&#8221;123&#8243;  
Myarray[2]=&#8221;456&#8243;  
Myarray[3]=&#8221;789&#8243;

6.sub  
使用sub发现并替换模式的第一次出现位置。字符串STR包含‘popedpopopill’,执行下  
列sub命令sub(/op/,&#8221;op&#8221;,STR)。模式op第一次出现时,进行替换操作,返回结果如下：  
‘pOPedpopepill’。  
假如grade.txt文件中,学生J.Troll的记录有两个值一样,“目前级别分”与“最高级别分”。只  
改变第一个为29,第二个仍为24不动,操作命令为sub(/26/,&#8221;29&#8243;,$0),只替换第一个出现  
24的位置。

$ awk &#8216;$1==&#8221;J.Troll&#8221; sub(/26/, &#8220;29&#8243;, $0)&#8217; grade.txt  
L.Troll 07/99 4842 Brown-3 12 29 26  
L.Transley 05/99 4712 Brown-2 12 30 28

7.substr  
substr是一个很有用的函数。它按照起始位置及长度返回字符串的一部分。例子如下：

$ awk &#8216;$1==&#8221;L.Transley&#8221; {print substr($1, 1,5)}&#8217; grade.txt  
L.Tan  
上面例子中,指定在域1的第一个字符开始,返回其前面5个字符。  
如果给定长度值远大于字符串长度， awk将从起始位置返回所有字符，要抽取L.Tansley的姓,只需从第3个字符开始返回长度为7。可以输入长度99,awk返回结果相同。

$ awk &#8216;{$1==&#8221;L.Transley&#8221; {print substr($1, 3,99)}&#8217; grade.txt  
Transley

substr的另一种形式是返回字符串后缀或指定位置后面字符。这里需要给出指定字符串及其返回字串的起始位置。例如,从文本文件中抽取姓氏,需操作域1,并从第三个字符开始：

$ awk &#8216;{print substr($1, 3)}&#8217; grade.txt  
Troll  
Transley

还有一个例子,在BEGIN部分定义字符串,在END部分返回从第t个字符开始抽取的子串。

$ awk &#8216;{BEGIN STR=&#8221;A FEW GOOD MEN&#8221;} END {print substr(STR,7)) grade.txt  
GOOD MEN

8.从shell中向awk传入字符串  
awk脚本大多只有一行,其中很少是字符串表示的,这一点通过将变量传入awk命令行会变得很容易。现就其基本原理讲述一些例子。  
使用管道将字符串stand-by传入awk,返回其长度。

$ echo &#8220;Stand-by&#8221; | awk &#8216;{print length($0)}&#8217;  
8

设置文件名为一变量,管道输出到awk,返回不带扩展名的文件名。

$ STR=&#8221;mydoc.txt&#8221;  
$ echo $STR | awk &#8216;{print subst($STR, 1, 5)}&#8217;  
mydoc

设置文件名为一变量,管道输出到awk,只返回其扩展名。  
$ STR=&#8221;mydoc.txt&#8221;  
$ echo $STR | awk &#8216;{print substr($STR, 7)}&#8217;  
txt

&nbsp;

转载：<http://hi.baidu.com/zzztou/blog/item/c09b9a31c5d65013ebc4af8c.html>

&nbsp;

http://www.ibm.com/developerworks/cn/linux/l-cn-awkinwork/index.html

## 

## awk读取多个文件

了解了FNR和NR这两个awk内置变量的意义就很容易知道这两种方法是如何运作的  
FNR     The input record number in the current input file.  #已读入当前文件的记录数

NR      The total number of input records seen so far.      #已读入的总记录数

next    Stop processing the current input record. The next input record is  
read and processing starts over with the first pattern in the AWK  
program. If the end of the input data is reached, the END block(s),  
if any, are executed.  
awk &#8216;NR==FNR{&#8230;}NR>FNR{&#8230;}&#8217; file1 file2  
\# 读入file1的时候，已读入file1的记录数FNR一定等于awk已读入的总记录数NR，因为file1是awk读入的首个文件，故读入file1时执行前一个命令块{&#8230;}  
\# 读入file2的时候，已读入的总记录数NR一定>读入file2的记录数FNR，故读入file2时执行后一个命令块{&#8230;}

awk &#8216;NR==FNR{&#8230;;next}{&#8230;}&#8217; file1 file2  
\# 读入file1时，满足NR==FNR，先执行前一个命令块，但因为其中有next命令，故后一个命令块{&#8230;}是不会执行的  
\# 读入file2时，不满足NR==FNR，前一个命令块{..}不会执行，只执行后一个命令块{&#8230;}

########################  
#     处理 多个 文件  
########################

当awk处理的文件超过两个时，显然上面那种方法就不适用了。因为读第3个文件或以上时，也满足NR>FNR (NR!=FNR)，显然无法区分开来，所以就要用到更通用的方法了：

1. ARGIND        # 当前被处理参数标志

awk &#8216;ARGIND==1{&#8230;}ARGIND==2{&#8230;}ARGIND==3{&#8230;}&#8230; &#8216; file1 file2 file3 &#8230;*复制代码*

2. ARGV            # 命令行参数数组

awk &#8216;FILENAME==ARGV[1]{&#8230;}FILENAME==ARGV[2]{&#8230;}FILENAME==ARGV[3]{&#8230;}&#8230;&#8217; file1 file2 file3 &#8230;*复制代码*

3. 把文件名直接加入判断

awk &#8216;FILENAME==&#8221;file1&#8243;{&#8230;}FILENAME==&#8221;file2&#8243;{&#8230;}FILENAME==&#8221;file3&#8243;{&#8230;}&#8230;&#8217; file1 file2 file3 &#8230;*复制代码*

&nbsp;

http://hi.baidu.com/beibeiboo/item/c0cb1856ba4344474eff20ab

&nbsp;

&nbsp;

> <span style="color: #0000ff;">awk -F, &#8216;BEGIN {<br /> while ((getline < &#8220;file2&#8243;) > 0)<br /> f2array[$2] = $1<br /> OFS=&#8221;,&#8221;}</span>
> 
> <span style="color: #0000ff;">{if (f2array[$1])<br /> print f2array[$1],$2,$3,$4,$5<br /> #else<br /> #  print $1 &#8221; not listed in file2&#8243; > &#8220;unmatched&#8221;<br /> }&#8217; file1</span>
