---
title: All scripts used for bak
author: 悟道
layout: post
permalink: /?p=3165
categories:
  - bash
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<pre class="brush: bash; title: server_project.bak; notranslate" title="server_project.bak">#!/bin/bash
#rsync -vazuL --delete \

echo "Bak to ~/sdcct/gold_bak/server-project/"

rsync -vazu --delete \
	--exclude-from ~/sdcct/gold_bak/server-project-exclude \
	  chentong@gold:/data7T/home-backup/chentong/server-project/ \
	  ~/sdcct/gold_bak/server-project/
ret=$?
if test $ret -ne 0; then
	echo "Wrong in server-project.bak" | mutt -s "Wrong in server-project.bak" chentong_biology@163.com
else
	echo "Right in server-project.bak" | mutt -s "Right in server-project.bak" chentong_biology@163.com
fi

echo "Finish rsync server-project ---`date`---"  &gt;&gt;~/server-project_rsync.log 2&gt;&1
</pre>

<pre class="brush: bash; title: m6a.bak; notranslate" title="m6a.bak">#!/bin/bash
#rsync -vazuL --delete \
rsync -vazu --delete --exclude 'nature' --exclude 'cell' --exclude 'trash' \
	  chentong@gold:/data10T/projects-10T/chentong/server-project/m6a/ \
	  ~/sdcct/gold_bak/m6a/
ret=$?
if test $ret -ne 0; then
	echo "Wrong in m6a.bak" | mutt -s "Wrong in m6a.bak" chentong_biology@163.com
else
	echo "Right in m6a.bak" | mutt -s "Right in m6a.bak" chentong_biology@163.com
fi

echo "Finish rsync $0 ---`date`---"  &gt;&gt;~/m6a_rsync.log 2&gt;&1

</pre>

<pre class="brush: bash; title: 5hmc.bak; notranslate" title="5hmc.bak">#!/bin/bash
#rsync -vazuL --delete \
rsync -vazu --delete \
	  chentong@gold:/data10T/projects-10T/chentong/server-project/5hmc/ \
	  ~/sdcct/gold_bak/5hmc/ 
ret=$?
if test $ret -ne 0; then
	echo "Wrong in 5hmC.bak" | mutt -s "Wrong in 5hmC.bak" chentong_biology@163.com
else
	echo "Right in 5hmC.bak" | mutt -s "Right in 5hmC.bak" chentong_biology@163.com
fi

echo "Finish rsync 5hmC ---`date`---"  &gt;&gt;~/5hmc_rsync.log 2&gt;&1


</pre>

<pre class="brush: bash; title: project.bak; notranslate" title="project.bak">#!/bin/bash
#rsync -vazuL --delete \
rsync -vazu --delete \
	chentong@diamond:/data7T/home-backup/chentong/project/ \
	  ~/sdcct/gold_bak/project/
ret=$?
if test $ret -ne 0; then
	echo "Wrong in project.bak" | \
		mutt -s "Wrong in project.bak" chentong_biology@163.com
else
	echo "Right in project.bak" | \
		mutt -s "Right in project.bak" chentong_biology@163.com
fi

echo "Finish rsync $0 ---`date`---"  &gt;&gt;~/project_rsync.log 2&gt;&1

</pre>

<pre class="brush: bash; title: wordpressBak.sh; notranslate" title="wordpressBak.sh">#!/bin/bash
if [ -e ~/sent ]; then
	/bin/rm -f ~/sent
fi

if [ -e ~/sent.lock ]; then
	/bin/rm -f ~/sent.lock
fi

path=~/

cur=$(date +%F)
file='wordpressSQLdroptable.'${cur}'.gz'
mysqldump --add-drop-table -uct586 -p524208572 own | gzip &gt;${path}$file
echo 'wordpress databse bak' | mutt -s $file chentong_biology@163.com \
	-a ${path}$file
file2='wordpressSRC.'${cur}'.tar.gz'
tar -czf ${path}$file2 /var/www/wordpress
echo 'wordpress src bak' | mutt -s $file2 chentong_biology@163.com \
    -a ${path}$file2

</pre>

<pre class="brush: bash; title: makefile.bak.sh; notranslate" title="makefile.bak.sh">#!/bin/bash

cur=$(date +%F)
make="Makefile."${cur}'.tar.gz'
tar -czf /home/chentong/$make `find /home/chentong -name Makefile`\
	`find /home/chentong -name makefile.tm` \
    `find /data7T/home-backup/chentong/ -name Makefile`\
    `find /data7T/home-backup/chentong/ -name makefile.tm` \
    `find /data10T/projects-10T/chentong/ -name Makefile`\
    `find /data10T/projects-10T/chentong/ -name makefile.tm`


#echo 'Server Makefile bak' | mutt -s $make chentong_biology@163.com \
#	-a /home/chentong/$make''
python /home/chentong/bin/pythonmail2.py $make "Server Makefile bak /data7T/home-backup/chentong /home/chentong /data10T/projects-10T/chentong/" /home/chentong/$make

echo "Finish raync makefile `date`" &gt;&gt;/home/chentong/makefile.bak.log

</pre>

<pre class="brush: bash; title: programBak.sh; notranslate" title="programBak.sh">#!/bin/bash
if [ -e ~/sent ]; then
	/bin/rm -f ~/sent
fi

if [ -e ~/sent.lock ]; then
	/bin/rm -f ~/sent.lock
fi


cur=$(date +%F)
file='program.'${cur}'.tar.gz'
tar -czf $file /home/chentong/home/server/pybin/*.py /home/chentong/home/server/r /home/chentong/home/server/calendar\
	/home/chentong/home/server/bin/*.sh /home/chentong/home/server/bin/*.py /home/chentong/home/server/clib /home/chentong/home/server/python\
	/home/chentong/.bash_aliases /home/chentong/home/server/makefile.tm /home/chentong/home/server/bashrc.mk \
	/home/chentong/home/project/project5/pybin/
#/oldhome/CT/server/cbin ---stop 20120829 /oldhome/CT/bin --stop 20120829
#/oldhome/CT/server/project/project1/README --- stop 20120829

size=`ls -l $file | cut -d ' ' -f 5`

if [ $size -gt 40000000 ]; then
	#echo "Super size; emergency" | mutt -s $file chentong_biology@163.com
	pythonmail2.py "Super size; emergency" "Super size; emergency" 
else
	#echo 'program bak' | mutt -s $file chentong_biology@163.com \
	#-a $file
	pythonmail2.py "Program bak" "Program bak" $file 
fi
#if test $? -ne 0; then
#	echo "No mutt"
#fi
/bin/rm -f $file

#make="Makefile."${cur}'.tar.gz'
#tar -czf $make `find /oldhome/CT/server -name Makefile` `find /oldhome/CT/server/ -name makefile.tm` `find ~/sdcct/project5/ -name Makefile` `find ~/sdcct/project5/ -name makefile.tm` `find ~/sdcct/server-project5/ -name Makefile` `find ~/sdcct/server-project5/ -name makefile.tm`
##tar -czfr $make `find /oldhome/CT/server/ -name makefile.tm`
#
#echo 'Makefile bak' | mutt -s $make chentong_biology@163.com \
#	-a $make 
#
#/bin/rm -f $make

#docbak=" Doc."${cur}'.tar.gz'
#tar -czf $docbak /oldhome/CT/server/doc/weekly/ \
#	`find /oldhome/CT/server/doc/report/ -name *.tex` \
#	`find /oldhome/CT/server/project/project5/doc/ -name *.tex` 
#
#
#size=`ls -l ${docbak} | cut -d ' ' -f 5`
#
#if [ $size -gt 40000000 ]; then
#	echo "Super size; emergency" | mutt -s $docbak chentong_biology@163.com
#else
#	echo 'Doc bak' | mutt -s $docbak chentong_biology@163.com \
#	-a $docbak
#fi
#
#/bin/rm -f $docbak

</pre>