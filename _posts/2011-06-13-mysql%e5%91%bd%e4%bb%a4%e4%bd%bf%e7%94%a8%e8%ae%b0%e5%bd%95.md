---
title: mysql命令使用记录
author: 悟道
layout: post
permalink: /?p=1019
categories:
  - sql
tags:
  - sql
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.查看表的结构

> describe tablename;

2.从表中取出数行以查看表的内容

> select * from tablename limit 1,20;

3.限定读取条件

> select * from tablename where Key=&#8221;sth&#8221; OR Key2 LIKE %sth%;

4.mysql输出结果重定向到文件

> select * INTO OUTFILE &#8220;filename&#8221; from tablename;
> 
> mysql -uuser -ppasswd <file.sql >file.result（命令写在文件中）

5.备份和恢复数据库(详见[here][1])

> mysqldump -uuser -ppasswd DATABASENAME >FILE

> MYSQLDUMP -Uuser -Ppasswd DATABASENAME | gzip >file

> mysql -u user -p passed <FILE

6.新建用户

> grant all privileges on databasename.* to &#8216;usr&#8217;@'localhost&#8217; identified by &#8216;passwd&#8217;
> 
> grant select on ncbi_taxonomy.* to &#8216;pc&#8217;@&#8217;210.75.224.6&#8242; identified by &#8216;pc&#8217;； #access from other IP can cause &#8220;ERROR 1130 (00000): Host &#8216;gold&#8217; is not allowed to connect to this MySQL server&#8221;
> 
> #grant select on ncbi_taxonomy.\* to &#8216;pc&#8217;@&#8217;210.75.224.\*&#8217; identified by &#8216;pc&#8217;;  #wrong
> 
> &#8216;ncbi_taxonomy&#8217; indicates the name of database, \*.\* means all databases and tables
> 
> &#8216;pc&#8217;@&#8217;210.75.224.6&#8242;  means user can use username &#8216;pc&#8217; at client with ip 210.75.224.6 to access the database
> 
> &#8216;pc&#8217;@'%&#8217; means user can access to the database at any ip address.
> 
> flush privileges; #update user table
> 
> #browse user status
> 
> use mysql;
> 
> select host, user from user;

7.查看用户权限

> show grants for &#8216;user&#8217;@'localhost&#8217;

8.解决ERROR 2003 (HY000): Can&#8217;t connect to MySQL server on &#8221;host&#8221; (111)

默认情况下Mysql只允许本地登录，所以需要修改配置文件将地址绑定给注释掉：

> vim /etc/mysql/my.cnf
> 
> \# Instead of skip-networking the default is now to listen only on  
> \# localhost which is more compatible and is not less secure.  
> #bind-address <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> <wbr /> = 127.0.0.1 <wbr /> <&#8212;注释掉这一行就可以远程登录了

重启mysql服务：

> **sudo /etc/init.d/mysql restart**

<http://blog.sina.com.cn/s/blog_60fcb5a10100qkyb.html>

<http://hepeng1688.iteye.com/blog/50716>

9.重启mysql服务

> **sudo /etc/init.d/mysql restart**

10.当我们不管是利用mysqlimport 还是load data infile导入数据时，碰到错误：

> ERROR 13 (HY000): Can&#8217;t get stat of &#8216;/home/marry/users.txt&#8217; (Errcode: 13)

是目录权限问了。当然我们：

> chown -R u+rx /home/marry

可以解决这个问题。

11.ERROR 29 (HY000): File &#8216;/var/www/gi\_taxid\_prot.dmp&#8217; not found (Errcode: 13) [<http://ubuntuforums.org/showthread.php?t=822084>]

> sudo chown mysql:mysql /home/marry/users.txt

12.mysql导入数据 [http://stackoverflow.com/questions/4541983/why-is-this-mysql-statement-giving-me-an-error]

> use ncbi_taxonomy;
> 
> drop table if exists gi\_taxid\_prot;
> 
> create table gi\_taxid\_prot (gi INT , taxid INT，PRIMARY KEY (gi));
> 
> load data infile &#8220;/var/www/gi\_taxid\_prot.dmp&#8221; into table gi\_taxid\_prot;
> 
> load data local infile &#8220;/var/www/gi\_taxid\_prot.dmp&#8221; into table gi\_taxid\_prot; 【when ERROR 1045 (28000) appeared】
> 
> #if Error 1148 ERROR 1148 (42000): The used command is not allowed with this MySQL version happend [<http://ubuntuforums.org/showthread.php?t=1990780>]
> 
> <pre>use : mysql -h localhost -u monte -p monte --local-infile
or mysql -u user -p --local-infile menagerie</pre>
> 
> load data infile &#8216;/var/www/gi\_taxid\_prot.dm&#8217; into table test fields terminated by &#8216;,&#8217; lines terminated by &#8216;\n&#8217;;

13.创建主键和索引【http://codereflex.net/primary-key-index-mysql/】，主键会默认被索引。

> CREATE TABLE Employee (  
> Emp\_id INT NOT NULL AUTO\_INCREMENT,first\_name VARCHAR(19) NOT NULL,last\_name VARCHAR(19) NOT NULL,age SMALLINT NOT NULL,  
> Designation VARCHAR(19) NOT NULL,Address VARCHAR(19),PRIMARY KEY (Emp_id));
> 
> **ALTER TABLE Employee ADD PRIMARY KEY (Emp_id);**
> 
> CREATE TABLE Employee (  
> Emp\_id INT NOT NULL ,first\_name VARCHAR(19) NOT NULL,  
> last\_name VARCHAR(19) NOT NULL,age SMALLINT NOT NULL,Designation VARCHAR(19) NOT NULL,Address VARCHAR(19),PRIMARY KEY (Emp\_id, first_name));
> 
> **ALTER TABLE Employee ADD PRIMARY KEY (Emp\_id,first\_name);**

14.简单的多表查询例子

> mysql -h 198.162.3.1 -u username -p password ncbi_taxonomy \  
> < opt.sql >out.result
> 
> cat opt.sql:
> 
> drop table if exists tmp;  
> create table tmp (gi INT, PRIMARY KEY (gi));  
> load data local infile &#8220;\`pwd\`/${file1}.gi&#8221; into table tmp;  
> select gi\_taxid\_prot.gi,gi\_taxid\_prot.taxid from gi\_taxid\_prot,tmp where tmp.gi = gi\_taxid\_prot.gi;

15.mysql日志和配置文件目录

<pre class="brush: bash; title: ; notranslate" title="">/var/log/mysql/error.log
/etc/mysql/my.cnf
</pre>

16.

17.

18.

19.

20.

 [1]: http://210.75.224.29/wordpress/?p=397