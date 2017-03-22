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
  从中查找`GEOarchive spreadsheet format`，并下载`Metadata
  spreadsheet`, 通常是
  [Download metadata spreadsheet (template and examples) UPDATED!](https://www.ncbi.nlm.nih.gov/geo/info/examples/seq_template_v2.1.xls)
  ，官方推荐下载最新版，这儿就提供链接了。

* 下载完之后填写表格。表格中有2个样例表，可以参考着填写。

	* 表格里面需要的MD5值在Linux下可以使用命令`md5sum filename`来获取；
	  Windows下可以在网上搜索一个MD5值计算工具。

* 数据上传，原始测序的fastq一般采用gzip压缩后上传。
	
	* 在Linux系统，使用的是`lftp`上传；
	  Windows可以使用[FileZilla](https://www.filezilla.cn).

* `lftp`上传

  为了方便lftp上传，我写了一个bash脚本, 
  命名为[`GEO_upload.sh`](https://raw.githubusercontent.com/Tong-Chen/NGS/master/GEO_upload.sh)，只需提供FTP服务器的地址、用户名、密码、上传文件所在目录和上传到FTP服务器的目录即可。

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

	* 如图所示，填写好登录所需的信息，然后双击进入`fasp`目录。
      ![Filezilla login](/images/Filezilla_1.png)

	* 在右侧窗口，点击右键，选择`创建目录并进入`。

	* 将左侧窗口要上传的文件拖动到右侧窗口，开始上传。

	* 在菜单栏的`传输`--`对已存在文件的默认操作`
	  --选择`上传-继续文件传输`即可实现断点续传。
	
	* 设置`重连次数`: `编辑`-`设置`-`最大重试次数 99; 登陆重试延时 200; 超时秒数 20`

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

* 另外还可以借助airflow，使得上传更加自动化，具体程序如下：
  
  ```python
  #!/usr/bin/env python
  # -*- coding: utf-8 -*-
  from __future__ import unicode_literals
  from __future__ import division, with_statement
  '''
  Copyright 2015, 陈同 (chentong_biology@163.com).  
  ===========================================================
  '''
  __author__ = 'chentong & ct586[9]'
  __author_email__ = 'chentong_biology@163.com'
  #=========================================================
  desc = '''
  Program description:
      This will generate a dag file for uploading data to GEO.
      
      Suppose we have data for uploading in directory `/home/name/project1/upload`, 
      the generated dag file would be saved at the directory `/home/name/project1/`.
  '''
  
  import sys
  import os
  from json import dumps as json_dumps
  from datetime import datetime, timedelta 
  from optparse import OptionParser as OP
  
  debug = 0
  
  
  def cmdparameter(argv):
      if len(argv) == 1:
          global desc
          print >>sys.stderr, desc
          cmd = 'python ' + argv[0] + ' -h'
          os.system(cmd)
          sys.exit(1)
      usages = "%prog -i ftp"
      parser = OP(usage=usages)
      parser.add_option("-f", "--ftp-link", dest="ftp",
          metavar="FTP", default="ftp-private.ncbi.nlm.nih.gov", 
          help="The url of FTP server. Default <ftp-private.ncbi.nlm.nih.gov>.")
      parser.add_option("-u", "--username-ftp", dest="userFTP",
          metavar="USERNAME", default='geo', 
          help="Username of FTP server. Default <geo>.")
      parser.add_option("-p", "--passwd", dest="passwd",
          metavar="PASSWORD", default='33%9uyj_fCh?M16H', 
          help="Password for FTP server. Default <33%9uyj_fCh?M16H>.")
      parser.add_option("-U", "--user-name-NCBI", dest="userNCBI",
          help="Username for NCBI login.")
      parser.add_option("-d", "--absolute-path-for-directory-containing-all-data", 
          dest="dir",  
          help="The absolute path for directory containing \
  all and only data for uploading. \n\
  Please make sure you have another copy of all data in this folder, \
  since all these data will be deleted after uploading.")
      parser.add_option("-v", "--verbose", dest="verbose",
          action="store_true", help="Show process information")
      (options, args) = parser.parse_args(argv[1:])
      assert options.ftp != None, "A ftp link needed for -i"
      return (options, args)
  #--------------------------------------------------------------------
  
  
  def main():
      options, args = cmdparameter(sys.argv)
      #-----------------------------------
      ftp = options.ftp
      userFTP = options.userFTP
      passwd  = options.passwd
      userNCBI = options.userNCBI
      verbose = options.verbose
      dir = options.dir
      parentdir = dir.rstrip('/').rsplit('/', 1)[0]
      output_dag = open(parentdir+'/'+userNCBI + '.dag.py', 'w')
      lftp_script1 = parentdir+'/'+userNCBI + '_lftp.script1'
      lftp_script2 = parentdir+'/'+userNCBI + '_lftp.script2'
      output_lftp1 = open(lftp_script1, 'w')
      output_lftp2 = open(lftp_script2, 'w')
      
      global debug
      #-----------------------------------
      print >>output_lftp1, '''
  open -u %s,%s %s
  mkdir -p fasp/GEO_metadata_%s/
      ''' % (userFTP, passwd, ftp, userNCBI)
  
      print >>output_lftp2, '''
  open -u %s,%s %s
  cd fasp/GEO_metadata_%s/
  cache size 33554432
  set cmd:parallel 20
  mput -E %s/*
      ''' % (userFTP, passwd, ftp, userNCBI, dir)
  
      output_lftp1.close()
      output_lftp2.close()
  
      print >>output_dag, '''
  from airflow import DAG
  from airflow.operators import BashOperator, EmailOperator
  
  from datetime import datetime, timedelta
  
  
  one_min_ago = datetime.combine(datetime.today() - timedelta(minutes=20),
                                    datetime.min.time())
  
  default_args = {
      'owner': 'ct',         
      'depends_on_past': True, 
      'start_date': one_min_ago,
      'email': ['chentong_biology@163.com'],
      'email_on_failure': True, 
      'email_on_retry': True, 
      'retries': 500, 
      'retry_delay': timedelta(seconds=30)
  }
  '''
  
      print >>output_dag, '''
  
  dag_id = "%s_GEO_upload"
  
  mkdir = "lftp -f %s"
  lftp = "lftp -f %s"
  
  
  dag = DAG(dag_id, default_args=default_args,
      schedule_interval="@once")
  
  geo_lftp_mkdir = BashOperator(
      task_id='geo_lftp_mkdir', 
      bash_command=mkdir, 
      dag=dag, retries=3)
  
  #In case the directory exists, but still supplying 3 minutes for `geo_lftp_mkdir` to run before strating `geo_lftp_upload`
  geo_lftp_sleep = BashOperator(
      task_id='geo_lftp_sleep', 
      bash_command="sleep 3m",
      dag=dag, retries=1, trigger_rule="dummy")
  
  geo_lftp_sleep.set_upstream(geo_lftp_mkdir)
  
  geo_lftp_upload = BashOperator(
      task_id='geo_lftp_upload', 
      bash_command=lftp, 
      dag=dag)
  
  geo_lftp_upload.set_upstream(geo_lftp_sleep)
  
  ''' % (userNCBI, lftp_script1, lftp_script2)
  
      twoyearafter = datetime.now()+timedelta(days=750)
      
      print >>output_dag, """
  html_content = '''
  Dear Sir/Madam,  
    
    Thanks for you kindly host such great public data resource.
      
    I have successfully transferred my data to NCBI-GEO ftp sever. 
        
    Here is the information you may be needed for further processing
          
      1. GEO account username: <strong>%s</strong>
      2. Names of the directory and files deposited: <strong>fasp/GEO_metadata_%s/</strong>
      3. Public release date: <strong>%s</strong>
        
    If there is any format or content problem, please do not hesitate to contact me.
              
    Best,  
                
    %s
  
  ''' 
  """ % (userNCBI, userNCBI, twoyearafter.strftime('%Y-%m-%d'), userNCBI)
      print >>output_dag, '''
  
  Success_mail = EmailOperator(
      task_id="Success_mail", 
      to="chentong_biology@163.com",  
      subject="GEO upload Finished",  
      html_content=html_content,  
      dag=dag)
  
  Success_mail.set_upstream(geo_lftp_upload)
  
  '''
  
      output_dag.close()
  
  if __name__ == '__main__':
      main()


  ```
