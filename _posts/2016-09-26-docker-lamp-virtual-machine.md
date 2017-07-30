---
title: Docker for LAMP with multiple virtual hosts
author: ct
layout: post
categories:
  - Docker
tags:
  - Docker
---

### 搭建主LAMP服务器

* 下载alpine-httpd: `docker pull httpd:2.4-alpine`
* 交互式运行alpine-httpd: `docker run --rm -it -p 80:80 --name apache-main httpd:2.4-alpine bash`
  
  ```
  bash-4.3# ls
  bin      build    cgi-bin  conf     error    htdocs   icons
  include  logs     man      manual   modules
  bash-4.3# pwd
  /usr/local/apache2
  bash-4.3# ls conf/
  extra       httpd.conf  magic       mime.types  original
  bash-4.3# ls conf/extra/
  httpd-autoindex.conf           httpd-default.conf
  httpd-languages.conf           httpd-mpm.conf
  httpd-ssl.conf                 httpd-vhosts.conf
  httpd-dav.conf                 httpd-info.conf
  httpd-manual.conf              httpd-multilang-errordoc.conf
  httpd-userdir.conf             proxy-html.conf
  bash-4.3# 
  ```

* 拷贝出httpd.conf文件：`docker cp apache-main:/usr/local/apache2/conf/httpd.conf .`

* 对http文件做一些修改

  ```
  115c115
  < #LoadModule charset_lite_module modules/mod_charset_lite.so
  ---
  > LoadModule charset_lite_module modules/mod_charset_lite.so
  196, 197c196, 197
  < User daemon
  < Group daemon
  ---
  > User apache
  > Group apache
  218c218
  < ServerAdmin you@example.com
  ---
  > ServerAdmin user@domain.com
  227c227
  < #ServerName www.example.com:80
  ---
  > ServerName www.domain.com
  434, 435c434, 435
  <     #AddType text/html .shtml
  <     #AddOutputFilter INCLUDES .shtml
  ---
  >     AddType text/html .shtml
  >     AddOutputFilter INCLUDES .shtml
  501c501
  < #Include conf/extra/httpd-vhosts.conf
  ---
  > Include conf/extra/httpd-vhosts.conf
  528a529, 530
  > AddDefaultCharset UTF-8
  ```

* 拷贝出httpd-vhosts.conf文件：`docker cp
* apache-main:/usr/local/apache2/conf/extra/httpd-vhosts.conf .`

* `CTRL+c`中断apache-main的运行


### 指定Volume运行

* 从httpd.conf文件中可以看到`DocumentRoot`为`usr/local/apache2/htdocs/`, 挂载本地网站到相应目录。
* 运行本地主网站 `docker run --rm -dit --name apache-main -v /var/wwww/html/:/usr/local/apache2/htdocs/ httpd:2.4-alphine`


### 


### Reference

* Dockerfile RUN vs CMD vs ENTRY <http://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/#>
* Multiple virtual hosts <https://medium.com/@jmarhee/running-multiple-web-applications-on-a-docker-host-with-apache-85f673f02803#.dbg3bbqyz>

