---
title: Linux下文件夹时间戳和权限问题
author: ysx
layout: post
categories:
  - R
tags:
  - R
  - Bioinfo
---

在日常多人协作时，最开始习惯看文件夹更新时间来查看是否有更新。

比如，起始状态：

```
ysx@localhost:~/trash/ehbio$ ls -ltr
total 0
drwxr-xr-x. 2 ysx ehbio 6 Jan  7 10:48 webserver
drwxr-xr-x. 2 ysx ehbio 6 Jan  7 10:48 train
drwxr-xr-x. 2 ysx ehbio 6 Jan  7 10:48 bioinfoservice
```

在`webserver`文件夹下，增加一个文件，`record.md`

```
ysx@localhost:~/trash/ehbio$ cat <<END >webserver/record.md
1. 完成9个生物在线数据存储、查询和分析网站的建设。
END
```

再查看下文件夹日期有没有变化, 发生变化了，为我们新增文件的日期。

```
ysx@localhost:~/trash/ehbio$ ls -ltr webserver/record.md
-rw-r--r--. 1 ysx ehbio 74 Jan  7 10:49 webserver/record.md
ysx@localhost:~/trash/ehbio$ ls -ltr
total 0
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 train
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 bioinfoservice
drwxr-xr-x. 2 ysx ehbio 22 Jan  7 10:49 webserver
```

那么再继续追加内容，还是使用`cat` (不同写入方式也有影响，后面会提到)。

```
ysx@localhost:~/trash/ehbio$ cat <<END >>webserver/record.md 
2. 一个网站发表于NAR数据库专刊，3个网站正在投稿中。
END
```

这时再看文件夹日期，发现与文件不同步了。文件日期`更新`了，文件夹日期却`没变`。

```
ysx@localhost:~/trash/ehbio$ ls -ltr webserver/record.md
-rw-r--r--. 1 ysx ehbio 148 Jan  7 10:52 webserver/record.md
ysx@localhost:~/trash/ehbio$ ls -ltr
total 0
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 train
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 bioinfoservice
drwxr-xr-x. 2 ysx ehbio 22 Jan  7 10:49 webserver
```

我们有每天必须做工作记录的习惯，查看工作记录有无更新时，根据文件夹日期来判断文件夹内的文件内容有没有更新就不合适了。

那么文件夹的更新日期是什么决定的呢？

我们在使用`less`操作时，有时会不小心对一个文件夹进行`less`操作。看上去就像文件夹里的内容变成了一个文本文件。


```
ysx@localhost:~/trash/ehbio$ less webserver/
total 4
drwxr-xr-x. 2 ysx ehbio  22 Jan  7 10:49 ./
drwxr-xr-x. 5 ysx ehbio  70 Jan  7 10:48 ../
-rw-r--r--. 1 ysx ehbio 148 Jan  7 10:52 record.md
```

而实际上确实是类似文本文件的方式存储的，文件夹可以看做`文件inode:文件名`组成的文本文件。只要文件夹内未发生文件的新增、删除、软链或文件夹内文件的`inode` (也称为索引节点)未改变，文件夹的时间戳就不会发生变化。

而我们每次追加文件内容都未改变文件名字和文件的`inode`，所以文件夹的日期未发生变化。

```
# -i可查看文件的inode
ysx@localhost:~/trash/ehbio$ ls -ai webserver/
2763934 .  2764125 ..   104480 record.md
ysx@localhost:~/trash/ehbio$ cat <<END >>webserver/record.md 
> 3. 继续为大数据的再次利用和更方便利用而努力
> END
ysx@localhost:~/trash/ehbio$ ls -ai webserver/
2763934 .  2764125 ..   104480 record.md
```

关于文件夹日期更新的问题算是解决了。

另一个问题是，我每次更新完文件内容，文件夹的日期却都会变化，看上去与前面的认知矛盾。我想问题可能出在`vim`上，我每次都使用它来更新文件，下面看一下。


大家注意这里面`webserver`日期与`webserver/record.md`日期的变化和`ls -i`的输出结果的变化。
```
ysx@localhost:~/trash/ehbio$ ls -ltr 
total 0
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 train
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 bioinfoservice
drwxr-xr-x. 2 ysx ehbio 22 Jan  7 10:49 webserver
ysx@localhost:~/trash/ehbio$ ls -ltr webserver/record.md 
-rw-r--r--. 1 ysx ehbio 212 Jan  7 11:03 webserver/record.md

# -i可查看文件的inode
ysx@localhost:~/trash/ehbio$ ls -i webserver/record.md
104480 webserver/record.md
ysx@localhost:~/trash/ehbio$ vim webserver/record.md
ysx@localhost:~/trash/ehbio$ ls -ltr webserver/record.md 
-rw-r--r--. 1 ysx ehbio 215 Jan  7 11:06 webserver/record.md
ysx@localhost:~/trash/ehbio$ ls -ltr
total 0
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 train
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 bioinfoservice
drwxr-xr-x. 2 ysx ehbio 22 Jan  7 11:06 webserver

# -i可查看文件的inode
ysx@localhost:~/trash/ehbio$ ls -i webserver/record.md
2465326 webserver/record.md
```

确实是`vim`改变了文件的`inode`，也就是说在我们使用`vim`修改文件时，`vim`为了避免中间出现意外，先从命名了修改前的文件，修改后的文件以之前文件的名字存储，看上去我们做的是**原位修改**, 实际上是有了新的文件，所以`inode`发生了变化。当然这个操作可以自己配置修改。

在另外一个情况下，如果我们对文件夹**无**可写权限，但对该文件夹内的文件**有可写权限**时，`vim`自动调用另外一个方式修改文件，先把文件做个备份，然后原位修改。

```
ysx@localhost:~/trash/ehbio$ chmod a-w webserver/
ysx@localhost:~/trash/ehbio$ ls -ltr
total 0
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 train
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 bioinfoservice
dr-xr-xr-x. 2 ysx ehbio 22 Jan  7 11:06 webserver
# 写不进去
ysx@localhost:~/trash/ehbio$ vim webserver/a

# 可以修改
ysx@localhost:~/trash/ehbio$ vim webserver/record.md 
ysx@localhost:~/trash/ehbio$ ls -ltr webserver/record.md
-rw-r--r--. 1 ysx ehbio 249 Jan  7 11:15 webserver/record.md
# 文件夹时间戳未变
ysx@localhost:~/trash/ehbio$ ls -ltr
total 0
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 train
drwxr-xr-x. 2 ysx ehbio  6 Jan  7 10:48 bioinfoservice
dr-xr-xr-x. 2 ysx ehbio 22 Jan  7 11:06 webserver

# 文件inode也未变
ysx@localhost:~/trash/ehbio$ ls -i webserver/record.md
2465326 webserver/record.md
```

设计软件时，需要考虑的问题还是挺多的。看上去挺简单的事情，里面说不准有多少点需要注意，作分析也是这样。

## 如果有需求，欢迎联系我们。

* 数据库和网站建设：把测序过的数据盘活，以更好的组织方式来展示、查询、使用和共享
* 生信培训：与老司机一起快速入门和分享经验绕出大坑
* 生信数据分析：一起定制分析，更快更好地解析数据


