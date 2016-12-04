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

5. Centos6安装Mysql5.7 

   ```bash
   # 官网下载源码包
   wget http://dev.mysql.com/get/mysql57-community-release-el6-7.noarch.rpm
   # rpm安装yum源
   rpm -Uvh mysql57-community-release-el6-7.noarch.rpm
   # Mysql安装 
   yum install -y mysql-community-client mysql-community-server
   # Start mysql service
   service mysqld start 

   # 在日子/var/log/mysqld.log中会有root的密码信息
   #  temporary password is generated for root@localhost: gaB1wd

   # 查看并设置mysqld自启动
   chkconfig --list | grep mysqld
   chkconfig mysqld on

   # 配置mysql
   mysql_secure_installation 
   ```

   * [install ref](https://segmentfault.com/a/1190000005820034)

   * 启动错误InnoDB: The Auto-extending innodb_system data file './ibdata1' is of a different size 640 pages (rounded down to MB) than specified in the .cnf file: initial 768 pages,  max 0 (relevant if non-zero) pages!))''
     
     Add `innodb_data_file_path = ibdata1:10M:autoextend` to `/etc/my.cnf` `mysqld` block
	 OR 

	 Remove `id*` files in mysql datadir


   * Mysql datadir

     Defined in file `/etc/my.conf` with `datadir=/mysql`.
   
   * Your password does not satisfy the current policy requirements
     
     PASSWORD needs containing uppercase leters, lowercase letters, numbers and special characters. 
     
     Please refer [here](http://bbs.bestsdk.com/detail/762.html) to `SET GLOBAL validate_password_policy='LOW';`。

6. centos安装pandoc，pandoc-citeproc

   ```r
   #make sure libgmp.so.10 in LD_LIBRARY_PATH
   #locate libgmp.so.10
   #Add path of libgmp.so.10 to file /etc/ld.so.conf
   #ldconfig -v

   # Install stack
   curl -sSL https://get.haskellstack.org/ | sh
   stack setup
   # cable install cpphs
   cabal install cpphs
   
   #Clone and install
   mkdir pandoc-build
   cd pandoc-build
   git clone https://github.com/jgm/pandoc-types
   git clone https://github.com/jgm/texmath
   git clone https://github.com/jgm/pandoc-citeproc
   git clone https://github.com/jgm/pandoc
   git clone https://github.com/jgm/cmark-hs
   git clone https://github.com/jgm/zip-archive
   cd pandoc
   git submodule update --init
   stack install --test --install-ghc --stack-yaml stack.full.yaml
   
   # pandoc and pandoc-citeproc will be installed to /root/.local/bin
   # add this directory to PATH 
   ```

   To pull in the latest changes,  after you’ve done this and there have been changes in the repositories: Visit `each repository` in `pandoc-build` (pandoc-types, texmath, pandoc-citeproc, pandoc, zip-archive, cmark-hs) and do `git pull`. In the pandoc repo,  also do `git submodule update` and `stack install --test --stack-yaml stack.full.yaml`.)
