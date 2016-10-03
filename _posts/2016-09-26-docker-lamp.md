---
title: Docker for LAMP
author: ct
layout: post
categories:
  - Docker
tags:
  - Docker
---

这部分介绍下，如何利用Docker搭建一个便携的LAMP网络服务器。
Docker的基本使用请参考 <{{ site.url }}/2016/07/docker/>。


### 基本使用

官方未提供LAMP的镜像，搜索了下, 发现推荐使用
[`tutum/lamp`](https://hub.docker.com/r/tutum/lamp/)的帖子最多，
且在Docker hub上评分较高，故这里也用这个做为示例。运行`docker search
lamp`获得其它LAMP相关镜像。

运行`docker pull tutum/lamp`获取LAMP镜像。

运行`docker run --rm -p 8080:80 -p 3306:3306 tutum/lamp`启动LAMP容器。
	
  * 若出现错误`bind: address already in use`, 
	则选择一个新的host_port (`-p host_port:container_port`)做为映射端口。

  * 因为作为测试用，所以加了`--rm`；若做daemon, 替换其为`-d`。

在宿主机上再打开一个新的终端，运行`curl http://127.0.0.1:8080`就可以探
测到LAMP镜像中运行的网页服务器了。如果有外网访问权限或设置了SSH tunnel，
则可在浏览器中测试。

### 挂载自己的网站到LAMP镜像
	
* 方法一：运用volume映射，运行`docker run --rm -v /local_html/:/app -p 8080:80 tutum/lamp`.

* 方法二：运用Dockerfile新构建一个lamp

  Dockerfile内容如下 (local_html与Dockerfile在同一目录)：

  ```
  FROM tutum/lamp:latest
  RUN rm -rf /app/*
  COPY local_html/* /app/
  EXPOSE 80 3306
  CMD ["/run.sh"]
  ```
  
  运行`docker build -t docker_hub_username/lamp-self .`创建新的映像。

  注：在我们得到一个镜像后，可以使用`docker history --no-trunc=true
  tutum/lamp`来查看这个镜像的生成历史，获得类似于Dockerfile的文件，
  然后增加或者覆盖想要的操作。

  ```
  IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
  3d4f934accdb        7 months ago        /bin/sh -c #(nop) CMD ["/run.sh"]               0 B                 
  aa321fa8d23f        7 months ago        /bin/sh -c #(nop) EXPOSE 3306/tcp 80/tcp        0 B                 
  6446fbfc507d        7 months ago        /bin/sh -c #(nop) VOLUME [/etc/mysql /var/lib   0 B                 
  44e98bdf2bbf        7 months ago        /bin/sh -c #(nop) ENV PHP_POST_MAX_SIZE=10M     0 B                 
  bedff16caee9        7 months ago        /bin/sh -c #(nop) ENV PHP_UPLOAD_MAX_FILESIZE   0 B                 
  72b723ccc97f        7 months ago        /bin/sh -c mkdir -p /app && rm -fr /var/www/h   0 B                 
  9bb67f3e1d7b        7 months ago        /bin/sh -c git clone https://github.com/ferma   66.45 kB            
  30aeae62f85c        7 months ago        /bin/sh -c a2enmod rewrite                      0 B                 
  18c7fa6ee534        7 months ago        /bin/sh -c #(nop) ADD file:4eacfc1aa3adff00b3   1.115 kB            
  0e6ae46b9d7a        7 months ago        /bin/sh -c chmod 755 /*.sh                      1.767 kB            
  41b57fec0232        7 months ago        /bin/sh -c #(nop) ADD file:846d81e0679354c2e3   1.122 kB            
  d1cbec592f63        7 months ago        /bin/sh -c rm -rf /var/lib/mysql/*              0 B                 
  520e2f6560c9        7 months ago        /bin/sh -c #(nop) ADD file:1b12f1071297cfbb02   84 B                
  17db5629ffc0        7 months ago        /bin/sh -c #(nop) ADD file:dadf942589f45f87e6   86 B                
  4fa78a22f055        7 months ago        /bin/sh -c #(nop) ADD file:3568f72d83e2d611e1   30 B                
  b57aa10ab85b        7 months ago        /bin/sh -c chmod 755 /*.sh                      645 B               
  438f80d6c1e7        7 months ago        /bin/sh -c #(nop) ADD file:a72b1b2b34a76805fc   549 B               
  4dfade5e9c4a        7 months ago        /bin/sh -c #(nop) ADD file:bbf77f727c38cb03a7   29 B                
  7601a98f8a03        7 months ago        /bin/sh -c #(nop) ADD file:62ecf7e0d59dfa5d60   67 B                
  0ebbbec8ac86        7 months ago        /bin/sh -c apt-get update &&   apt-get -y ins   238.9 MB            
  9fabaa35b190        7 months ago        /bin/sh -c #(nop) ENV DEBIAN_FRONTEND=noninte   0 B                 
  2c3431c1c481        7 months ago        /bin/sh -c #(nop) MAINTAINER Fernando Mayo <f   0 B                 
  8693db7e8a00        8 months ago        /bin/sh -c #(nop) CMD ["/bin/bash"]             0 B                 
  a4c5be5b6e59        8 months ago        /bin/sh -c sed -i 's/^#\s*\(deb.*universe\)$/   1.895 kB            
  c4fae638e7ce        8 months ago        /bin/sh -c echo '#!/bin/sh' > /usr/sbin/polic   194.5 kB            
  f15ce52fc004        8 months ago        /bin/sh -c #(nop) ADD file:7ce20ce3daa6af21db   187.7 MB            
  ```

  我们可以从运行的container中拷贝文件到宿主机，使用`docker ps`查看运行
  中container的名字，如`berserk_payne`, 运行`docker cp
  berserk_payne:run.sh .`就可以拷贝`run.sh`文件到本地，然后相应修改。

  ```
  CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                                            NAMES
  aeafa241a81c        tutum/lamp          "/run.sh"           About an hour ago   Up About an hour    0.0.0.0:10000->80/tcp, 0.0.0.0:10001->3306/tcp   berserk_payne       
  ```

  我们可以利用命令`docker run --rm -it -p 8080:80 tutum/lamp bash`来覆盖原来image中的CMD命令，进而进入交互式界面。

  ```
  root@a1716037e274:/# ls
  app   create_mysql_admin_user.sh  home   media  proc  run.sh
  start-apache2.sh   tmp            bin    dev    lib   mnt    
  root  sbin         start-mysqld.sh       usr    boot  etc                  lib64              opt            run    srv    sys   var
  root@a1716037e274:/# 
  ```

### 挂载外部数据库

1. 新建数据库容器存储数据

   ```
   # 如果是跟着流程走，想偷懒的话或者系统中有其它需要依赖ubuntu image
   # 的容器，则使用ubuntu image 构建数据容器。
   docker create -v /var/lib/mysql --name test_db ubuntu
   # 也可以用docker run创建新的容器
   docker run -d -v /var/lib/mysql --name test_db ubuntu
   # 推荐使用alpine image，占用空间小，只有5M
   docker create -v /var/lib/mysql --name test_db alpine sh
   ```
   
   Note: you can change the name of the volume container,  which will be
   used in the next step. The volume path (`/var/lib/mysql`) should not be
   changed if using `mysql`.
 
2. 在LAMP中向`test_db`写入数据

   启动LAMP容器，`docker run --rm --volumes-from=test_db -v
   /local_html/:/app -p 10000:80 -p 10001:3306 -e
   MYSQL_PASS="test_ali" tutum/lamp`。


   请注意：`An empty or uninitialized MySQL volume is detected`。

   ```
   => An empty or uninitialized MySQL volume is detected in
   /var/lib/mysql
   => Installing MySQL ...
   => Done!
   => Waiting for confirmation of MySQL service startup
   => Creating MySQL admin user with preset password
   => Done!
   ========================================================================
   You can now connect to this MySQL Server using:
   
       mysql -uadmin -ptest_ali -h<host> -P<port>
   
   Please remember to change the above password as soon as possible!
   MySQL user 'root' has no password but only allows local connections
   ========================================================================
   /usr/lib/python2.7/dist-packages/supervisor/options.py:295:
   UserWarning: Supervisord is running as root and it is searching
   for its configuration file in default locations (including its
   current working directory); you probably want to specify a " -c"
   argument specifying an absolute path to a configuration file for
   improved security.
   'Supervisord is running as root and it is searching '
   2016-09-25 11:33:39, 807 CRIT Supervisor running as root (no
   user in config file)
   2016-09-25 11:33:39, 807 WARN Included extra file "
   /etc/supervisor/conf.d/supervisord-apache2.conf"  during parsing
   2016-09-25 11:33:39, 807 WARN Included extra file "
   /etc/supervisor/conf.d/supervisord-mysqld.conf"  during parsing
   2016-09-25 11:33:39, 844 INFO RPC interface 'supervisor'
   initialized
   2016-09-25 11:33:39, 845 CRIT Server 'unix_http_server' running
   without any HTTP authentication checking
   2016-09-25 11:33:39, 845 INFO supervisord started with pid 1
   2016-09-25 11:33:40, 848 INFO spawned: 'mysqld' with pid 432
   2016-09-25 11:33:40, 850 INFO spawned: 'apache2' with pid 433
   2016-09-25 11:33:42, 267 INFO success: mysqld entered RUNNING
   state,  process has stayed up for > than 1 seconds (startsecs)
   2016-09-25 11:33:42, 268 INFO success: apache2 entered RUNNING
   state,  process has stayed up for > than 1 seconds (startsecs)
   ```

   连接mysql数据库 `mysql -uadmin -ptest_ali -h 127.0.0.1 -P 10001`。

   ```
   mysql> create database test;
   Query OK,  1 row affected (0.00 sec)
   ```
   
   加载备份的数据库 `mysql -uadmin -ptest_ali -h 127.0.0.1 -P 10001 test <test.dump`

3. 再次启动LAMP容器，查看写入的数据是否已经保存。
   `docker run --rm --volumes-from=test_db -v
   /root/docker/docker-test/web/:/app -p 10000:80 -p 10001:3306 -e
   MYSQL_PASS="test_ali" tutum/lamp`


   请注意：`Using an existing volume of MySQL`。

   ```
   => Using an existing volume of MySQL
   2016-09-25 12:24:19, 261 CRIT Supervisor running as root (no user
		   in config file)
   2016-09-25 12:24:19, 262 WARN Included extra file "
   /etc/supervisor/conf.d/supervisord-apache2.conf"  during parsing
   2016-09-25 12:24:19, 262 WARN Included extra file "
   /etc/supervisor/conf.d/supervisord-mysqld.conf"  during parsing
   2016-09-25 12:24:19, 312 INFO RPC interface 'supervisor'
   initialized
   2016-09-25 12:24:19, 312 CRIT Server 'unix_http_server' running
   without any HTTP authentication checking
   2016-09-25 12:24:19, 312 INFO supervisord started with pid 1
   2016-09-25 12:24:20, 316 INFO spawned: 'mysqld' with pid 9
   2016-09-25 12:24:20, 318 INFO spawned: 'apache2' with pid 10
   2016-09-25 12:24:21, 746 INFO success: mysqld entered RUNNING
   state,  process has stayed up for > than 1 seconds (startsecs)
	2016-09-25 12:24:21, 746 INFO success: apache2 entered RUNNING
	state,  process has stayed up for > than 1 seconds (startsecs)
   ```

4. 正式运行：
   `docker run -d --volumes-from=test_db -v
   /root/docker/docker-test/web/:/app -p 10000:80 -p 10001:3306 -e
   MYSQL_PASS="test_ali" tutum/lamp`

### 备份数据库容器
   
前面，我们运行`docker run -d -v /var/lib/mysql --name test_db
ubuntu`新建了一个数据容器，并且在mysql里面写入了数据。现在我们想把
这些数据保存起来，怎么操作？

打包提取：

```
docker run --rm --volumes-from=test_db \
 -v /root/docker/docker-test/:/backup ubuntu \
 tar czvf /backup/backup.tar.gz /var/lib/mysql/
# test_db: 为想要储存的数据容器名字, 必须有
# /root/docker/docker-test/: 为宿主机存储备份文件backup.tar的位置
# /backup/: 为容器ubuntu中存储backup.tar的位置
# /var/lib/mysql: 为需要打包的目录，来源于test_db
```

解压到新的容器：

```
#新建一个容器, 使用alphine，只有5M系统
docker run -v /var/lib/mysql --name test_db2 alpine sh
#解压到指定目录 /var/lib/mysql
docker run --rm --volumes-from=test_db2 \
 -v /root/docker/docker-test/:/backup ubuntu \
 bash -c "cd /var/ && tar zxvf /backup/backup.tar --strip 1"

#注意我们在打包时，tar会去除leading /, 因此解压时我们是在/var目录下
做的解压。
```

删除旧的数据容器：

```
docker rm -v test_db
```

### 多虚拟主机实现

为了实现多虚拟主机的挂载，我们使用[`jwilder/nginx-proxy`](https://github.com/jwilder/nginx-proxy)
设置好的反向代理。

```
docker run -d -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock jwilder/nginx-proxy
```

在我们运行其它虚拟主机时加上对应的域名 （域名需在DNS服务商处配置过指向
host机的IP）。

```
#virtual machine 1
docker run -d --volumes-from=test_db -v /root/docker_test/web/:/app -e
VIRTUAL_HOST=test.ehb.com -e MYSQL_PASS="test_ali" tutum/lamp
#virtual machine 2
docker run -d -v /var/www/html:/app -v /data/ct/ehb_result/:/app/result -e VIRTUAL_HOST=www.ehb.com httpd:2.4-alpine
```

### 参考

* 基本LAMP <http://www.tuicool.com/articles/UBNvMjq>
* Database volume <https://blog.tutum.co/2014/05/27/containerize-your-database-volume-with-tutum-mysql-images/>
* 官方Volume <https://docs.docker.com/engine/tutorials/dockervolumes/>
* 步步Docker apache <http://linoxide.com/linux-how-to/configure-apache-containers-docker-fedora-22/>
* Nginx proxy <http://tech.mybuilder.com/virtual-hosts-with-docker/>
* Apache virtual hosts (not work for me ) <https://medium.com/@jmarhee/running-multiple-web-applications-on-a-docker-host-with-apache-85f673f02803#.dbg3bbqyz>
