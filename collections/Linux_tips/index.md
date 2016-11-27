---
title: Linux tips
author: ct
layout: page
---


### 记录无法归类的小问题及解决方法

1. Windows下转换的UTF-8文件通常为UTF-8 BOM, 文件的行首存在字符`<U+FEFF>`，怎么查看和去除？

   在vim中执行`:set nobomb` and `:wq` 或在终端执行 `perl -pi~ -CSD -e 's/^\x{fffe}//' file`
   
   执行`less -a file`可以看有无特殊字符。

2. vim配置文件位置？

   /etc/vimrc or ~/.vimrc

3. 查看端口对应的进程
  
   lsof -Pnl +M -i4

4. fork: retry: Resource temporarily unavailable

   修改最大允许的进程数和打开文件数

   在文件`/etc/security/limits.conf`中增加或修改如下文字

   ```
   # <*> 可替换为用户名
   * soft nofile 65535
   * hard nofile 65535
   * soft nproc 65535
   * hard nproc 65535
   ```
   
   如果是centos6，还需修改文件`/etc/security/limits.d/90-nproc.conf`
   
   ```
   * soft nproc 102400
   * hard nproc 102400
   ```

	修改完成后，重新登录服务器，运行`ulimit -a`查看。

