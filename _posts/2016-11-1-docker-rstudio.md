---
title: Docker rstudio
author: ct
layout: post
description:
modified:
categories: [Bioinformatics, docker, R]
tags: [R, docker]
---

### 安装运行Docker-rstudio

* 下载并运行: `docker run -d --name rstuido -p 8787:8787 rocker/hadleyverse`
* 在浏览器中打开<http://127.0.0.1:8787>，输入`rstudio`作为用户名和密码登录，进行操作
* 若要停止则关掉并删除运行的容器`rstudio`: `docker stop rstudio && docker rm rstudio`

### 共享宿主机的安装包

* 设置`R_LIBS`环境变量`.Renviron`
  
  ```
  # .Renviron content

  # ~/R/hostlibrary为宿主机R library的挂载目录
  R_LIBS="/usr/local/lib/R/site-library:/usr/lib/R/site-library:/usr/lib/R/library:~/R/hostlibrary"
  ```

* 挂载`.Renviron`到默认用户`rstudio`的家目录，以便在启动R时读入环境变量；挂载`/usr/lib64/R/library`到默认用户的`/home/rstudio/R/hostlibrary`目录（只读形式）

  ```
  docker run -d -p 8787:8787 --name rstudio -v /MPATHB/soft/R/.Renviron:/home/rstudio/.Renviron -v /usr/lib64/R/library:/home/rstudio/R/hostlibrary:ro rocker/hadleyverse
  ```

### 安装R包到宿主机目录

* 设置`R_LIBS`环境变量`.Renviron`
  
  ```
  # .Renviron content

  # ~/R/hostlibrary为宿主机R library的挂载目录
  # ~/R/library为container内安装R包的路径
  R_LIBS_USER="~/R/library"
  R_LIBS="~/R/library:/usr/local/lib/R/site-library:/usr/lib/R/site-library:/usr/lib/R/library:~/R/hostlibrary"
  ```

* 在宿主机新建目录`mkdir -p /R_lib`, 保证任何用户有可读写权限。

* 挂载`.Renviron`到默认用户`rstudio`的家目录，以便在启动R时读入环境变量；挂载`/usr/lib64/R/library`到默认用户的`/home/rstudio/R/hostlibrary`目录（只读形式）

  ```
  docker run -d -p 8787:8787 --name rstudio -e USERID=$UID -v /MPATHB/soft/R/.Renviron:/home/rstudio/.Renviron -v /R_lib:/home/rstudio/R/library -v /usr/lib64/R/library:/home/rstudio/R/hostlibrary:ro rocker/hadleyverse
  ```

* 挂载数据目录`/home/ct5/data`；为了获得数据目录的使用权限，需设置`docker container`的用户ID为宿主机的用户ID `-e USERID=$UID`。`$UID`为当前宿主机用户的ID。

  ```
  docker run -d -p 8787:8787 --name rstudio -e USERID=$UID -v /MPATHB/soft/R/.Renviron:/home/rstudio/.Renviron -v /R_lib:/home/rstudio/R/library -v /home/ct5/data:/home/rstudio/data rocker/hadleyverse
  ```

* 进入运行的容器，执行测试命令 `docker exec -it container_id bash` (会以根用户权限)

### Dockerfile

在Dockerfile所在目录运行 `docker build -t "username/r-bio:v1" .`。

```
FROM rocker/ropensci
MAINTAINER Tong Chen chentong_biology@163.com
## Py-dev

## Install additional dependencies
RUN install2.r --error \ 
    -r 'http://cran.rstudio.com' \
	-r 'http://datacube.wu.ac.at' \
	-r 'http://packages.ropensci.org' \
	-r 'http://www.bioconductor.org/packages/release/bioc' \
	-r 'http://nceas.github.io/drat' \
	gplots \
	Formula \
	ggfortify \
	vipor \
	viridis \
	VGAM \
	useful \
	tximport \
	test \
	tiff \
	trimcluster \
	tsne \
	supraHex \
	statmod \
	SummarizedExperiment \
	snow \
	sn \
	ShortRead \
	shape \
	segmented \
	scran \
	Rsamtools \
	rtracklayer \
	Rtsne \
	ROCR \
	robustbase \
	affy \
	DESeq2 \
	edgeR \
	genefilter \
	DESeq \
	EBImage \
	clusterProfiler \
	corrplot \
	bookdown \
	DOSE \
	modeltools \
	mclust \
	limma \
	BiocParallel \
	destiny \
	BiocGenerics \
	GenomeInfoDb \
	GenomicFeatures \
	GenomicFeatures \
	GOSemSim \
	ggbeeswarm \
	geneplotter \
	VennDiagram \
	qvalue \
	org.Hs.eg.db \
	org.Mm.eg.db \
	MAST \
	GO.db \
	fgsea \
	acepack \
	scater \
	scran \
	statmod \
	&& Rscript -e "devtools::install_github(c('satijalab/seurat'))" 
```

### Other files

Work for me

```
alias docker_rstudio="docker run -d -p 8787:8787 -e USERID=501 --name rbio -v /MPATHB/soft/R/.Renviron:/home/rstudio/.Renviron -v /MPATHB/r_lib:/data/r_library -v /MPATHC/ct:/data/data ct5869/r-bio:v1"
alias docker_rstudio_rm="docker stop rbio && docker rm rbio"

.Renviron

R_LIBS_USER="/data/r_library"
R_LIBS="/data/r_library:/usr/local/lib/R/site-library:/usr/lib/R/site-library:/usr/lib/R/library:~/R/hostlibrary"
```

### 直接安装运行Rstudio-server

* 安装参考 <https://www.rstudio.com/products/rstudio/download-server/>
  * wget https://download2.rstudio.org/rstudio-server-rhel-1.0.136-x86_64.rpm
  * sudo yum install --nogpgcheck rstudio-server-rhel-1.0.136-x86_64.rpm

* 具体操作
  * sudo rstudio-server verify-installation #查看是否安装正确
  * sudo rstudio-server start ## 启动
  * sudo rstudio-server status ## 查看状态
  * sudo rstudio-server stop ## 停止
  * ifconfig | grep 'inet addr' ## 查看服务端ip地址
  * sudo rstudio-server start ## 修改配置文件后重启
  * sudo rstudio-server active-sessions ## 列出活跃的sessions:
  * sudo rstudio-server suspend-session <pid> ## 暂停session
  * sudo rstudio-server suspend-all
  * <https://support.rstudio.com/hc/en-us/articles/200532327-Configuring-the-Server>
  

* 日志目录：/var/log/rstudio-server/
* 配置文件：
  * /etc/rstudio/rserver.conf 
  	* www-port=8787 (default)
	* www-address=0.0.0.0 (default)
    * rsession-ld-library-path=/opt/local/lib:/opt/local/someapp/lib
	* rsession-which-r=/usr/local/bin/R
  * /etc/rstudio/rsession.conf
    * Timeout
	  ```
	  [user]
	  session-timeout-minutes=30
	  [@powerusers]
	  session-timeout-minutes=0
      ```

### References
* DOcker Rstudio DOC <https://github.com/rocker-org/rocker/wiki/Using-the-RStudio-image>
* <https://ropensci.org/blog/blog/2014/10/23/introducing-rocker>
* 共享宿主机安装包和数据 <https://sbamin.com/blog/2016/02/13/running_rstudio_in_docker_environment/#running-rstudio-with-shared-folder>
