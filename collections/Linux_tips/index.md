---
title: Linux tips
author: ct
layout: page
---


### 记录无法归类的小问题及解决方法

1. Windows下转换的UTF-8文件通常为UTF-8 BOM, 文件的行首存在字符G，怎么查看和去除？

   在vim中执行`:set nobomb` and `:wq` 或在终端执行 `perl -pi~ -CSD -e 's/^\x{fffe}//' file`
   
   执行`less -a file`可以看有无特殊字符。

2. vim配置文件位置？

   `/etc/vimrc or ~/.vimrc`

3. 查看端口对应的进程
  
   `lsof -Pnl +M -i4`

4. 网站不能访问或没有权限 （关闭防火墙）

   ```
   #启动： 
   systemctl start firewalld
   #关闭： 
   systemctl stop firewalld
   #查看状态： 
   systemctl status firewalld 
   #开机禁用  ： 
   systemctl disable firewalld
   #开机启用  ： 
   systemctl enable firewalld
   firewall-cmd --zone=public --add-port=80/tcp --permanent    （--permanent永久生效，没有此参数重启后失效）
   #重新载入
   firewall-cmd --reload
   #查看
   firewall-cmd --zone= public --query-port=80/tcp
   #删除
   firewall-cmd --zone= public --remove-port=80/tcp --permanent
   ```

5. 关闭SELINUX

   ```
   setenforce 0  # 临时

   # 永久
   vim /etc/sysconfig/selinux

   SELINUX=enforcing 改为 SELINUX=disabled

   重启服务reboot
   ```
4. 查看端口是否通

   `telnet server_ip 25` (25为端口号)

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
   /etc/init.d/mysqld start

   # 在日子/var/log/mysqld.log中会有root的密码信息
   #  temporary password is generated for root@localhost: gaB1wd

   # 查看并设置mysqld自启动
   chkconfig --list | grep mysqld
   chkconfig mysqld on

   # 配置mysql
   mysql_secure_installation 

  # /tmp/mysql.sock
  # 获取 mysql.sock的位置
  netstat -ln | grep mysql   
   ```

   * [install ref](https://segmentfault.com/a/1190000005820034)

   * 启动错误InnoDB: The Auto-extending innodb_system data file './ibdata1' is of a different size 640 pages (rounded down to MB) than specified in the .cnf file: initial 768 pages,  max 0 (relevant if non-zero) pages!))''
     
     Add `innodb_data_file_path = ibdata1:10M:autoextend` to `/etc/my.cnf` `mysqld` block
     OR 

     Remove `ib*` files in mysql datadir

   * 启动错误 Fatal error: mysql.user table is damaged. Please run mysql_upgrade.

     First,  start your mysql without reading the user table: `/etc/init.d/mysqld start --skip-grant-tables`; Then run `mysql_upgrade` which should now run smoothly; Next stop mysqld: `killall mysqld`. Now you should be able to start up your mysql service normally again. [ref](https://stackoverflow.com/questions/36156475/mysqld-doesnt-start-after-brew-upgrade-from-5-6-to-5-7)

   * Mysql datadir

     Defined in file `/etc/my.conf` with `datadir=/mysql`.

     ```
     # stop mysqld service
     service mysqld stop

     # change mysql datadir

     ## mkdir
     mkdir -p /test2/mysql
	 chown mysql:mysql /test2/mysql
     /bin/cp /var/lib/mysql/* /test2/mysql/
     
     ## change /etc/my.cnf
     # datadir=/var/lib/mysql
     datadir=/test2/mysql
     #socket=/var/lib/mysql/mysql.sock
     socket=/test2/mysql/mysql.sock
     
     .
     .
     .
     
     [client]
     port=3306
     socket=/test2/mysql/mysql.sock


     ## Change /etc/init.d/mysql
	 #get_mysql_option datadir "/var/lib/mysql"  mysqld
	 get_mysql_option datadir "/test2/mysql"  mysqld 
     
     # start mysqld service
     service mysqld start
     ```
   
   * Your password does not satisfy the current policy requirements
     
     PASSWORD needs containing uppercase leters, lowercase letters, numbers and special characters. 
     
     Please refer [here](http://bbs.bestsdk.com/detail/762.html) to `SET GLOBAL validate_password_policy='LOW';`。
	
   * DBD::mysql::st execute failed: The total number of locks exceeds the lock table size

     Add "innodb_buffer_pool_size = 10G" to /etc/my.conf (default innodb buffer size is 128 M,  change to some number larger).

	 Then restart mysqld service `/etc/init.d/mysqld restart`.

	 Check the value of `innodb_buffer_pool_size` using `show  variables like 'innodb_buffer_pool_size';`.

6. centos安装pandoc，pandoc-citeproc

   ```bash
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


7. 添加用户并root权限

   ```bash
   adduser username
   passwd username

   赋予权限
   # /etc/sudoers
   username   All=(ALL)   ALL
   # /etc/passwd
   ```

8. Apache配置权限

   ```bash

   # Modify config file to allow .htaccess
   # /etc/httpd/conf/httpd.conf
   <Directory "/var/www/html">
   ------
   #Add following line
   AllowOverride AuthConfig
   </Directory>
   ```

   Restart server `apachectl restart`

   ```bash
   # In the folder which access wanted to be controlled
   # create .htaccess with following content
   # make sure .htpasswd_label not in same dir as .htaccess 
   # require: can specify username; valid-user meaning all users in .htpasswd can have access

   AuthType Basic
   AuthName "Please contact administrator for more information!!!"  
   AuthUserFile /dir/.htpasswd_label  
   require valid-user #
   ```

   Generate `.htpasswd_label` with command `htpasswd -cmb /dir/.htpasswd_label username userpasswd`. Apache下以`.ht`开头的文件不会被外部读取，安全性比较高。

   若出现500 EROOR，请查阅`/etc/httpd/logs/error_log`根据具体信息解决。

9. 权限问题

   ```bash
   chgrp -R user_grp dir
   ```

10. awk输出到文件
 
    ```bash
    awk 'BEGIN{OFS=FS="\t";file="output"}{print $1 >file; print $2;}' input >output2
    ```

11. 去除文件最后2行

    ```bash
    head -n -2 file #notice -2
    ```

12. Perl程序内设置环境变量

    ```perl
    $ENV{PATH} = "/MPATHB/soft/java8/jdk1.8.0_121/bin:$ENV{PATH}";
    ```

13. awk循环输出

    ```bash
    awk '{for (i=1; i<=NF; i++) printf "%.3f %s", $$i, (i==NF?RS:FS)}' file
    ```

14. Mariadb status and stop

    ```
    systemctl status mariadb
    systemctl stop mariadb
    ```

15. 查看端口使用情况

    ```
    netstat -a | grep '8080'
    lsof -i:8080
    ```

16. 给文件夹而非文件增加可执行属性

	The important thing to note here is that uppercase `X` acts differently to lowercase `x`. In manual we can read:

	The execute/search bits if the file is a directory or any of the execute/search bits are set in the original (unmodified) mode.
	In other words, `chmod u+X` on a file won't set the execute bit; and `g+X` will only set it if it's already set for the user.

    ```
    chmod -R u+rwX,g+rwX,go-rwx path

    or 

    find /path/to/base/dir -type d -exec chmod 755 {} +
    find /path/to/base/dir -type f -exec chmod 644 {} +
    chmod 755 $(find /path/to/base/dir -type d)
    chmod 644 $(find /path/to/base/dir -type f)
    find /path/to/base/dir -type d -print0 | xargs -0 chmod 755 
    find /path/to/base/dir -type f -print0 | xargs -0 chmod 644
    ```

17. awk中执行系统命令 (注意引号的使用)

    ```bash
    awk 'BEGIN{OFS=FS="\t"}{system("mv "$1".fq "$2".fq");}' 1
    ```

18. 定义全局函数

    ```bash
    # write in ~/.bash_profile
    abcdefg() {
		echo 'CT'
	}

	export -f abcdefg
	
    # source ~/.bash_profile
    # use in another program
	#!/bin/bash

	#set -x
	set -e
	set -u

	abcdefg
    ```

19. 输出到标准错误

   ```
   (>&2 echo "I willbe output to STDERR")
   ```

20. scp 和 rsync 非默认端口

   ```
   scp -P remote_port_number local remote
   rsync -av -e 'ssh -p remote_port_number' local remote
   ```

21. find 使用

    ```
	find . -name *.log -newer pca/2018-02-10.txt -size +0
	```

22. zip -j file.zip file # 不包含路径

23. 用户操作

```
# 批量修改密码
cat <<END >user_pass
user1:pass1
user2:pass2
END
chpasswd <user_pass

# 用户增加组
usermod -a -G ehbio ct

# 新建用户
cat <<END >/tmp/${user}.create
${user}:${password}::${group}::/disk/${user}:/bin/bash
END

newusers </tmp/${user}.create

# 删除用户
userdel -r ${user}
```

24. csplit

```
csplit --elide-empty-files --prefix=test  test.fa '/^>/' "{*}"
```

25. 取出文件倒数第二行

```
rev file | cut -f 2 | rev 
# 扔掉倒数第二行
rev file | cut -f 2 --complement | rev 
awk '{a=NF-1; print $a}' file
```

26. 合并pdf

```
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/default -dNOPAUSE -dQUIET -dBATCH -dDetectDuplicateImages -dCompressFonts=true -r150 -sOutputFile=output.pdf input.pdf
```
