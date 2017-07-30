---
title: Docker for LAMP with multiple virtual hosts
author: ct
layout: post
categories:
  - Docker
tags:
  - Docker
---

### Docker-gen + Nginx reverse proxy

```
docker run -d -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock
jwilder/nginx-proxy
```

### Run one domain

```
docker run -d -v /var/www/html:/app -v
/data/ct/ehb_result/:/app/result -e VIRTUAL_HOST=www.ehbio.com
tutum/lam
```

### Run the other domain 

```
docker run -d --volumes-from=wicd_db -v /root/docker_test/web/:/app -e
VIRTUAL_HOST=wicdb.ehbio.com -e MYSQL_PASS="wicd_ali"  tutum/lamp
```
