---
title: Upload high-throughput data to GEO
author: ct
layout: post
categories:
  - bioinformatics
tags:
  - geo
---

在我们发表高通量测序文章之前通常要上传测序数据到GEO数据库，现总结流程
如下。

* 在[NCBI GEO](https://www.ncbi.nlm.nih.gov/geo/submitter/)官网注册一
  个账号，然后登陆。

* 点击[Submission 
  Guidelines](https://www.ncbi.nlm.nih.gov/geo/info/seq.html) .
  从中查找`GEOarchive spreadsheet format`，并下载Metadata spreadsheet
  ，官方推荐下载最新版，这儿就提供链接了。

* 下载完之后填写表格。表格中有2个样例表，可以参考着填写。

	* 表格里面需要的MD5值在Linux下可以使用命令`md5sum filename`来获取
	* ；Windows下可以在网上搜索一个MD5值计算工具。

* 数据上传，原始测序的fastq一般采用gzip压缩后上传。
	
	* 在Linux系统，使用的是`lftp`上传；
	  Windows可以使用[FileZilla](https://www.filezilla.cn).

* `lftp`上传

  为了方便lftp上传，我写了一个bash脚本, 命名为`GEO_upload.sh`，只需提
  供FTP服务器的地址、用户名、密码、上传文件所在目录和上传到FTP服务器的
  目录即可。

  `GEO_upload.sh -f ftp-private.ncbi.nlm.nih.gov -u geo -p password -t
  fasp/detination_dir/ -s localdir/`

  为了简单方便，`localdir`里面只包含需要上传的文件，包括原始测序文件，
  处理后文件和Metadata spreadsheet。

```bash

#!/bin/bash

#set -x
set -e
set -u

usage()
{
cat <<EOF >&2
${txtcyn}
Usage:

$0 options${txtrst}

${bldblu}Function${txtrst}:

This script is used to upload files to an FTP server using lftp.

${txtbld}OPTIONS${txtrst}:
	-f	FTP address ${bldred}[NECESSARY]${txtrst}
	-u	User name ${bldred}[NECESSARY]${txtrst}
	-p	Password ${bldred}[NECESSARY]${txtrst}
	-t	Target dir ${bldred}[NECESSARY]${txtrst}
	-s	Source dir ${bldred}[NECESSARY]${txtrst}	
EOF
}

ftp=
user=
passwd=
target=
source_dir=

while getopts "hf:u:p:t:s:" OPTION
do
	case $OPTION in
		h)
			usage
			exit 1
			;;
		f)
			ftp=$OPTARG
			;;
		u)
			user=$OPTARG
			;;
		p)
			passwd=$OPTARG
			;;
		t)
			target=$OPTARG
			;;
		s)
			source_dir=$OPTARG
			;;
		?)
			usage
			exit 1
			;;
	esac
done

if [ -z $ftp ]; then
	usage
	exit 1
fi

cat <<END >lftp.script
open -u ${user},${passwd} ${ftp}
mkdir -p ${target}
cd ${target}
cache size 33554432
set cmd:parallel 10
mput -c ${source_dir}/*
END

lftp -f lftp.script

```

* `Filezilla`上传

	* 如图所示，填写好登录所需的信息，
      ![Filezilla login](/images/Filezilla_1.png)

	* 在右侧窗口，点击右键，选择`创建目录并进入`。

	* 将左侧窗口要上传的文件拖动到右侧窗口，开始上传。

	* 在菜单栏的`传输`--`对已存在文件的默认操作`
	  --选择`上传-继续文件传输`即可实现断点续传。

* 上传完成后，需要给GEO的管理人员写一封邮件，大体内容如下：

```
Receiver: geo@ncbi.nlm.nih.gov

Subject: ftp upload

Context:

Dear Sir/Madam, 

Thanks for you kindly host such great public data resource.

I have successfully transferred my data to NCBI-GEO ftp sever. 

Here is the information you may be needed for further processing

1. GEO account username: 我的GEO用户名
2. Names of the directory and files deposited: 文件上传的路径, 对应上
面的fasp/detination_dir/
3. Public release date: 2018-12-31 文件释放时间，一般可以设置的比较远

If there is any format or content problem,  please do not hesitate to
contact me.

Best, 

Name
```

* 待GEO的工作人员审核处理后，你可以在GEO的账户下查看已上次的数据的GEO
  号和供Reviewer访问的私人链接用于文章审阅。
