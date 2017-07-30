---
title: Learn the Usage of I-TASSER for protein structure prediction
author: ct
layout: post
description: Learn the Usage of I-TASSER for protein structure prediction
modified:
categories: [Bioinformatics]
tags: [Protein structure]
---

### I-TASSER 安装

1. 下载I-TASSER, <http://zhanglab.ccmb.med.umich.edu/I-TASSER/download/>，解压即完成安装。

2. 下载、编译、安装`parallel`便于使用简单并行，<http://ftp.gnu.org/gnu/parallel/parallel-20160522.tar.bz2>

3. 安装依赖的数据文件
   * 新建本地目录存储数据文件 `mkdir ITLIB`
   * 运行脚本`./I-TASSER5.0/download_lib.pl -N false -libdir ITLIB/`下载数据文件，如果本地有`nr`数据库，则设置`-N false`, 跳过下载，直接软链过来就好。

4. 修改主程序文件`./I-TASSER5.0/I-TASSERmod/runI-TASSER.pl`
   
   * 修改nr数据库的判断
   
     ```perl
     $db       = "$libdir/nr/"; #remove last nr
  
     if(!-s "$db") # original
     {
       print "Your library files are not complete, please download library with the script download_lib.pl\n";
  	   exit;
     } #original
  
     $db       = "$libdir/nr/nr"; #add this line
     ``` 

   * 修饰FASTA文件的读取，屏蔽非字母字符

     ```
	 #if($line=~/(\S+)/) # Original
	 if($line=~/([A-Za-z]+)/) # Change to this
	 ```

   * 修改`PSSpred`运行顺序以便输入序列中含有末尾的`*`也可以运行

     ```perl
     `cp $datadir/seq.fasta .`; #original
     `cp $datadir/seq.txt .`; # add this line
     if(-s "seq.txt"){ # change fasta to txt
  	   `perl $pkgdir/PSSpred/mPSSpred.pl seq.txt $pkgdir $libdir`;
     }elsif(-s "seq.fasta"){  #change txt to fasta
  	   `perl $pkgdir/PSSpred/mPSSpred.pl seq.fasta $pkgdir $libdir`;
     }
     ```

   * 在2.2步骤结束后，2.3步骤开始前增加一个判断，如果未获得`seq.data`则退出程序。

     ```perl
     #add the following 3 line  
     if(!-s "$datadir/seq.dat"){
  	   exit(1);
     }
	 printf "2.3 Predict solvent accessibility...\n"; #original
     ```

5. 更正部分数据文件权限使得所有用户可读
   
   * 只发现这个目录下文件存在权限问题，执行`chmod a+rx ITLIB/summary/*`
   * 粗暴的做法可以给所有文件加可读，`chmod a+rx -R ITLIB/`，最后发现用这个方法省心


### I-TASSER运行

为了简化运行，把I-TASSER脚本做一个包装, 命名为`I_TASSER.sh`, 运行时只需要指定数据文件就好`I_TASSER.sh -n cyp -d cyp_dir`。

```
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

This script is used to facilitate I-TASSER usage.
Output will be directory given to <-d>.

${txtbld}OPTIONS${txtrst}:
	-f	Directory for I-TASSER${bldred}[NECESSARY]${txtrst}
		Default: /soft/I_TASSER/I-TASSER5.0/
	-l	Directory for template libraries${bldred}[NECESSARY]${txtrst}
		Default: /soft/I_TASSER/ITLIB/
	-j	Directory containing "bin/java"${bldred}[NECESSARY]${txtrst}
		Default: /usr/
	-n	Name of your query sequence.${bldred}[NECESSARY]${txtrst}
	-d	Directory containing file <seq.fasta> which saves query sequence 
		(without terminating * at the end of amino acid sequences)
	-o	Specify one or all other analyses like
		<-LBS>: predict ligand-binding site
		<-EC>:	predict EC number
		<-GO>:	predict GO terms
		Default: <-LBS>
EOF
}

pkgdir=/soft/I_TASSER/I-TASSER5.0
libdir=/soft/I_TASSER/ITLIB/
javadir=/usr/
seq_name=
seq_dir=
other_par="-LBS"


while getopts "hf:l:j:n:d:o:" OPTION
do
	case $OPTION in
		h)
			usage
			exit 1
			;;
		f)
			pkgdir=$OPTARG
			;;
		l)
			libdir=$OPTARG
			;;
		j)
			javadir=$OPTARG
			;;
		n)
			seq_name=$OPTARG
			;;
		d)
			seq_dir=$OPTARG
			;;
		o)
			other_par=$OPTARG
			;;
		?)
			usage
			exit 1
			;;
	esac
done

if [ -z ${seq_name} ]; then
	usage
	exit 1
fi

cat <<EOF
perl ${pkgdir}/I-TASSERmod/runI-TASSER.pl -pkgdir ${pkgdir} -libdir ${libdir} \
	-java ${javadir} -runstyle gnuparallel \
	-seqname ${seq_name} -datadir ${seq_dir} \
	${other_par}
EOF


perl ${pkgdir}/I-TASSERmod/runI-TASSER.pl -pkgdir ${pkgdir} -libdir ${libdir} \
	-java ${javadir} -runstyle gnuparallel \
	-seqname ${seq_name} -datadir ${seq_dir} \
	${other_par}

	#-homoflag benchmark 
```

当有较多蛋白需要运行时，可以使用依赖于`airflow`的批量并行脚本`I_TASSER_bat.py -i multi_cyp.fa -m 8 -n cyp -w absolute_path_for_multi_cyp.fa`，

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
    Airflow based bat-running of I_TASSER.
'''

import sys
import os
from json import dumps as json_dumps
from time import localtime, strftime 
timeformat = "%Y-%m-%d %H:%M:%S"
from optparse import OptionParser as OP
from string import maketrans


debug = 0

def cmdparameter(argv):
    if len(argv) == 1:
        global desc
        print >>sys.stderr, desc
        cmd = 'python ' + argv[0] + ' -h'
        os.system(cmd)
        sys.exit(1)
    usages = "%prog -i file"
    parser = OP(usage=usages)
    parser.add_option("-i", "--input-file", dest="filein",
        metavar="FILEIN", help="Fasta file with multiple protein sequences. Sequence name should not contain symbols other than alphabets, numbers and underlines.")
    parser.add_option("-m", "--maximum-number-itasser", dest="max_num",        
            type="int", help="Maximum allowed number of proteins for running I_TASSER paraellely.")
    parser.add_option("-n", "--project-name", dest="project_name",
            help="A string containing only alphabets, numbers and underlines to specify the name of the project. Normally one should add his/her username to avoid name conflicts.")
    parser.add_option("-w", "--working-dir", dest="work_dir",
        help="The absolute path for FASTA file")
    parser.add_option("-v", "--verbose", dest="verbose",
        action="store_true", help="Show process information")
    parser.add_option("-d", "--debug", dest="debug",
        default=False, action="store_true", help="Debug the program")
    (options, args) = parser.parse_args(argv[1:])
    assert options.filein != None, "A filename needed for -i"
    return (options, args)
#--------------------------------------------------------------------

def generateCmd(key, tmpL, count, max_num, index, assignmentL, work_dir):
    os.system("mkdir -p %s" % key)
    fh_out = open("%s/seq.fasta" % key, 'w')
    print >>fh_out, ">%s\n%s" % (key, ''.join(tmpL).rstrip('*'))
    fh_out.close()
    command = "(cd %s; I_TASSER.sh -n %s -d %s/)" % (work_dir, key, key)
    comment = '' if count > max_num else '#'

    print '''
%s = BashOperator(
    task_id='%s', 
    bash_command="%s", 
    dag=dag)

%s_success_mail = EmailOperator(
    task_id="%s_success_mail", 
    to="chentong_biology@163.com",  
    subject="%s I_TASSER success",  
    html_content="%s I_TASSER success",  
    dag=dag)
                
%s_success_mail.set_upstream(%s)
%s%s.set_upstream(%s)
''' % (key, key, command, 
       key, key, key, key, 
       key, key, 
       comment, key, assignmentL[index])
    if debug:
        print >>sys.stderr, "\t%s-->%s" % (key, assignmentL[index])
    assignmentL[index] = key
#---------END of generateCmd----------------------

def main():
    options, args = cmdparameter(sys.argv)
    #-----------------------------------
    file = options.filein
    max_num = options.max_num
    name    = options.project_name
    work_dir = options.work_dir
    verbose = options.verbose
    global debug
    debug = options.debug
    #-----------------------------------
    if file == '-':
        fh = sys.stdin
    else:
        fh = open(file)
    #--------------------------------
    print '''
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
    'retry_delay': timedelta(hours=300)
}

dag = DAG('%s', default_args=default_args,
    schedule_interval="@once")

    ''' % (name)

    count = 1
    key = ''
    tmpL = ''
    assignmentL = ['_'] * max_num
    for line in fh:
        if line[0] == '>':
            if key:
                generateCmd(key, tmpL, count, max_num, index, assignmentL, work_dir)
                count += 1
                if debug:
                    print >>sys.stderr, assignmentL
            #---------------------------------------------------
            key = line[1:].strip().translate(maketrans(' .-/({[]})', '_'*10))
            key = '_'+key
            tmpL = []
            index = count % max_num - 1
            #print >>sys.stderr, index
        else:
            tmpL.append(line.strip())
    if key:
        generateCmd(key, tmpL, count, max_num, index, assignmentL, work_dir)
    #-------------END reading file----------
    #----close file handle for files-----
    if file != '-':
        fh.close()
    #-----------end close fh-----------
    if verbose:
        print >>sys.stderr,\
            "--Successful %s" % strftime(timeformat, localtime())

if __name__ == '__main__':
    main()

```


### 类似工具
* <https://salilab.org/modeller/>
* <http://www.gromacs.org/>

