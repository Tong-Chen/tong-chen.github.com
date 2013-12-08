---
title: Install UCSC genome browser locally
layout: post
categories:
  - seq
  - NGS
  - letter
tags:
  - NGS
---

前期配置安装mysql+apache略过

1.新建mysql用户

{% highlight bash %}
create user 'gw'@'localhost' identified by 'qazplm_gw';

{% endhighlight %}

2.同步UCSC所需html文件和运行程序

{% highlight bash %}
mkdir /var/www/gw
#rsync -avzP --exclude 'ENCODE' --exclude 'goldenPath' rsync://hgdownload.cse.ucsc.edu/htdocs/ /var/www/gw
rsync -avzP --exclude 'ENCODE' rsync://hgdownload.cse.ucsc.edu/htdocs/ /var/www/gw
mkdir /var/www/gw/cgi-bin
rsync -avzP rsync://hgdownload.cse.ucsc.edu/cgi-bin/ /var/www/gw/cgi-bin/  #64 bit
rsync -avzP rsync://hgdownload.cse.ucsc.edu/cgi-bin-i386/ /var/www/gw/cgi-bin/  #32bit
chown -R www-data.www-data /var/www/gw/cgi-bin/

{% endhighlight %}

3.把一下内容写入/etc/apahce2/httpd.conf。XBitHack on是必须的。

{% highlight bash %}
/etc/apache2$ cat httpd.conf
XBitHack on
&lt;Directory /var/www/gw&gt;
	AllowOverride AuthConfig
	Options +Includes
&lt;/Directory&gt;

 # the ScriptAlias directive is crucial

ScriptAlias /gw/cgi-bin /var/www/gw/cgi-bin

&lt;Directory "/var/www/gw/cgi-bin"&gt;

	AllowOverride None
	Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch

	Order allow,deny
	Allow from all
	AddHandler cgi-script cgi pl

&lt;/Directory&gt;

{% endhighlight %}

4.设置Apache解析有执行权限的文件中的SSI指令，然后重启apache

{% highlight bash %}
ln -s /etc/apache2/mods-available/include.load /etc/apache2/mods-enabled/
/etc/init.d/apache2 restart

{% endhighlight %}

5.配置数据库。

进入/var/www/gw/cgi-bin/ 目录，建立hg.conf并写入下列内容，同时sudo chown www-data /var/www/gw/cgi-bin/hg.conf。 更多功能的conf文件见http://genome-test.cse.ucsc.edu/~kent/src/unzipped/product/ex.hg.conf。

{% highlight bash %}
db.host=localhost
db.user=gw
db.password=qazplm_gw
db.trackDb=trackDb

central.db=hgcentral
central.host=localhost
central.user=gw
central.password=qazplm_gw
central.domain=

backupcentral.db=hgcentral
backupcentral.host=localhost
backupcentral.user=gw
backupcentral.password=qazplm_gw
backupcentral.domain=

{% endhighlight %}

6.建立缓存文件夹

{% highlight bash %}
rm /var/www/gw/trash
mkdir /var/www/gw/trash
chown www-data.www-data /var/www/gw/trash

{% endhighlight %}

7、提供Javascript文件

{% highlight bash %}
mkdir -p /usr/local/apache/htdocs/
ln -s /var/www/gw/js/ /usr/local/apache/htdocs/js
ln -s /var/www/gw/style/ /usr/local/apache/htdocs/style
每次重启服务器后，可能要重复上述操作。
{% endhighlight %}

8.这时就应该能够访问了，成功的标志就是访问http://localhost/gw 会看到UCSC常见的页面。

9.配置数据库

{% highlight bash %}
wget http://hgdownload.cse.ucsc.edu/admin/hgcentral.sql
mysql -u&lt;high-user&gt; -p&lt;passwd&gt; -e 'create database hgcentral'
mysql -u&lt;high-user&gt; -p&lt;passwd&gt; -e &quot;grant all privileges on hgcentral.* to 'gw'@'localhost'&quot;
mysql -ugw -p qazplm_gw hgcentral &lt;hgcentral.sql
mysql -u&lt;high-user&gt; -p&lt;passwd&gt; -e 'create database hgFixed'
mysql -u&lt;high-user&gt; -p&lt;passwd&gt; -e &quot;grant select on hgFixed.* to 'gw'@'localhost'

{% endhighlight %}

10.出现错误/var/www/gw/cgi-bin/hgGateway: error while loading shared libraries: libssl.so.6: cannot open shared object file: No such file or directory,&#8230;

{% highlight bash %}
sudo apt-get install libssl0.9.8  #不能确定是否必须
#ln -s /usr/lib/libssl.so.0.9.8 /usr/lib/libssl.so.6
#ln -s /usr/lib/libcrypto.so.0.9.8 /usr/lib/libcrypto.so.6
sudo ln -s /lib/i386-linux-gnu/libssl.so.0.9.8 /usr/lib/libssl.so.6
sudo ln -s /lib/i386-linux-gnu/libcrypto.so.0.9.8 /usr/lib/libcrypto.so.6

{% endhighlight %}

11.建立本地mysql数据库

{% highlight bash %}
#change datadir to /home/mysql
/etc/init.d/mysql stop
vim /etc/mysql/my.cnf

#下载数据库
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chromInfo.MYD /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chromInfo.MYI /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chromInfo.frm /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/cytoBandIdeo.MYD /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/cytoBandIdeo.MYI /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/cytoBandIdeo.frm /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/grp.MYD /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/grp.MYI /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/grp.frm /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/hgFindSpec.MYD /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/hgFindSpec.MYI /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/hgFindSpec.frm /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/trackDb.MYD /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/trackDb.MYI /home/mysql/mm9
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/trackDb.frm /home/mysql/mm9

##赋予权限
chown -R mysql.mysql /home/mysql/mm9

{% endhighlight %}

12.出现错误  
a.Couldn&#8217;t connect to database (null) on localhost as gw. Client does not support authentication protocol requested by server; consider upgrading MySQL 的解决方法

{% highlight bash %}
set password for 'gw'@'localhost'=OLD_PASSWORD('qazplm_gw');
flush privileges;

{% endhighlight %}

b. Can’t connect to local MySQL server through socket ‘/var/lib/mysql/mysql.sock’

{% highlight bash %}
ln -s /var/run/mysqld/mysqld.sock /var/lib/mysql/mysql.sock
chmod 666 /var/lib/mysql/mysql.sock
chmod 755 /var/lib/mysql/

{% endhighlight %}

13.下载gbdb数据

{% highlight bash %}
#bbi 为encode数据
mkdir -p ~/gbdb/mm9
rsync -avzP --delete --max-delete=20 --exclude=bbi \
    rsync://hgdownload.cse.ucsc.edu/gbdb/mm9/ ~/gbdb/mm9/
#---mappability data---------------
rsync -avzp rsync://hgdownload.cse.ucsc.edu/gbdb/mm9/bbi/*.bw ~/gbdb/mm9/bbi
ln -s /home/genomebrowser/gbdb /gbdb

{% endhighlight %}

14.访问链接<http://localhost/gw/cgi-bin/hgGateway?db=mm9>

安装参考：http://blog.sciencenet.cn/blog-723745-569746.html

http://enotacoes.wordpress.com/2009/09/03/installing-a-minimal-ucsc-mirror-in-ubuntu-jaunty-64-bits/

15.构建UCSC hubtrack

{% highlight bash %}
#首先看目录结构
/var/www/hub$ tree
.
├── genomes.txt
├── hub.txt
└── mm9
    ├── ctcf1.bw
    ├── P3001.bw
    ├── ctcf2.bw
    ├── P3002.bw
    └── trackDb.txt

1 directory, 7 files

#再看每个文件的内容
$cat genomes.txt
genome	mm9
trackDb	mm9/trackDb.txt

$cat hub.txt
hub	myhub
shortLabel	Testhub
longLabel	Testhubsdsdsdsd
genomesFile	genomes.txt
email	my@my.com

$cat mm9/trackDb.txt
# access http://localhost/cgi-bin/hgTracks?db=mm9&amp;hubUrl=https://localhost/hub.txt
# help : http://genome.ucsc.edu/goldenPath/help/hgTrackHubHelp.html
# trackDb.txt syntaxhttp://genome.ucsc.edu/goldenPath/help/trackDb/trackDbHub.html#bigBed_-_Item_or_Region_Track_Settings
#http://davetang.org/muse/2012/03/15/ucsc-genome-browser-custom-overlap-tracks/
track One
container multiWig
shortLabel One
longLabel One
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks
windowingFunction mean+whiskers
maxHeightPixels 100:60:8

track One_ctcf
bigDataUrl ctcf1.bw
shortLabel ctcf1.bw
longLabel ctcf1.bw
parent one
type bigWig
color 0,102,255

track P300
bigDataUrl P3001.bw
shortLabel P3001.bw
longLabel P3001.bw
parent one
type bigWig
color 136,102,255

track Two
container multiWig
shortLabel Two
longLabel Two
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
windowingFunction maximum
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks

track ctcf2
bigDataUrl ctcf2.bw
shortLabel ctcf2.bw
longLabel ctcf2.bw
parent Two
type bigWig
color 0,102,255

track P3002
bigDataUrl P3002.bw
shortLabel P3002.bw
longLabel P3002.bw
parent Two
type bigWig
color 136,102,255

{% endhighlight %}

PS:其它需要添加的数据  
1.mm9相关数据表

{% highlight bash %}
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/all_bacends.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/all_bacends.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/all_bacends.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chromInfo.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chromInfo.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chromInfo.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/cytoBandIdeo.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/cytoBandIdeo.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/cytoBandIdeo.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/description.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/description.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/description.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/downloadlist.txt /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/extFile.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/extFile.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/extFile.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbCdnaInfo.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbCdnaInfo.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbCdnaInfo.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbExtFile.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbExtFile.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbExtFile.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbLoaded.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbLoaded.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbLoaded.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbMiscDiff.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbMiscDiff.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbMiscDiff.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbSeq.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbSeq.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbSeq.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbStatus.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbStatus.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbStatus.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbWarn.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbWarn.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/gbWarn.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/grp.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/grp.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/grp.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/hgFindSpec.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/hgFindSpec.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/hgFindSpec.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/history.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/history.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/history.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgAlias.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgAlias.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgAlias.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgColor.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgColor.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgColor.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgProtAlias.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgProtAlias.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgProtAlias.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgProtMap2.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgProtMap2.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgProtMap2.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgSpAlias.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgSpAlias.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgSpAlias.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgTargetAli.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgTargetAli.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgTargetAli.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgTxInfo.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgTxInfo.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgTxInfo.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgXref.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgXref.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/kgXref.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownAlt.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownAlt.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownAlt.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownBlastTab.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownBlastTab.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownBlastTab.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownCanonical.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownCanonical.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownCanonical.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGene.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGeneMrna.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGeneMrna.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGeneMrna.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGene.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGene.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGenePep.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGenePep.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownGenePep.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownIsoforms.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownIsoforms.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownIsoforms.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToAllenBrain.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToAllenBrain.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToAllenBrain.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToEnsembl.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToEnsembl.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToEnsembl.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToGnf1m.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToGnf1m.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToGnf1m.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToGnfAtlas2.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToGnfAtlas2.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToGnfAtlas2.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToLocusLink.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToLocusLink.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToLocusLink.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToMOE430A.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToMOE430A.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToMOE430A.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToMOE430.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToMOE430.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToMOE430.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToPfam.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToPfam.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToPfam.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToRefSeq.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToRefSeq.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToRefSeq.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToSuper.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToSuper.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToSuper.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToU74.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToU74.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToU74.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToVisiGene.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToVisiGene.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/knownToVisiGene.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/microsat.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/microsat.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/microsat.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30wayFrames.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30wayFrames.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30wayFrames.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30way.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30way.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30way.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30waySummary.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30waySummary.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/multiz30waySummary.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/pfamDesc.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/pfamDesc.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/pfamDesc.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30wayEuarch.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30wayEuarch.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30wayEuarch.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30way.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30way.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30way.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30wayPlacental.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30wayPlacental.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastCons30wayPlacental.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30wayEuarch.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30wayEuarch.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30wayEuarch.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30way.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30way.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30way.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30wayPlacental.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30wayPlacental.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/phastConsElements30wayPlacental.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refFlat.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refFlat.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refFlat.MYD.1 /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refFlat.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refGene.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refGene.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refGene.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refLink.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refLink.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refLink.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqAli.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqAli.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqAli.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqStatus.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqStatus.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqStatus.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqSummary.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqSummary.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/refSeqSummary.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/scopDesc.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/scopDesc.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/scopDesc.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/simpleRepeat.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/simpleRepeat.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/simpleRepeat.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/tableDescriptions.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/tableDescriptions.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/tableDescriptions.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/trackDb.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/trackDb.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/trackDb.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/ucscScop.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/ucscScop.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/ucscScop.MYI /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/organism* /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chr*_rmsk.frm /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chr*_rmsk.MYD /home/mysql/mm9/
rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/mm9/chr*_rmsk.MYI /home/mysql/mm9/

{% endhighlight %}

2.定时清理

{% highlight bash %}
#!/bin/bash
#10080 means 10080 minutes which is 14 days.
find /var/www/gw/trash/ \! \( -regex "/var/www/gw/trash/ct/.*" -or \
	-regex "/var/www/gw/trash/hgSs/.*" \) -type f -amin +10080 -exec rm -f {} \;
#find /var/www/gw/trash/ \( -regex "/var/www/gw/trash/ct/.*" -or -regex "/var/www/gw/trash/hgSs/.*" \) -type f -amin +10080 -exec rm -f {} \;


{% endhighlight %}

3.另一个不错的浏览器  
Trackster&#8212;http://www.nature.com/nbt/journal/v30/n11/full/nbt.2404.html?WT.ec_id=NBT-201211

TrackDB.bak

{% highlight bash %}
# help : http://genome.ucsc.edu/goldenPath/help/hgTrackHubHelp.html

track RNA_Seq
container multiWig
shortLabel RNASeq
longLabel NSC.Red.iPS.Green.tNSC.Blue.sertoli.Yellow.eiNSC.Pink.ESC.Cyan
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
windowingFunction mean+whiskers
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks
maxHeightPixels 100:80:8

track TP16_Pos
bigDataUrl TP16.rnaseq.pos.bw
shortLabel TP16.Pos
longLabel TP16.rnaseq.pos.bw
parent RNA_Seq
type bigWig
color 255,0,0

track TP22_Pos
bigDataUrl TP22.rnaseq.pos.bw
shortLabel TP22.Pos
longLabel TP22.rnaseq.pos.bw
parent RNA_Seq
type bigWig
color 0,255,0

track TP23_Pos
bigDataUrl TP23.rnaseq.pos.bw
shortLabel TP23.Pos
longLabel TP23.rnaseq.pos.bw
parent RNA_Seq
type bigWig
color 0,0,255

track sertoli_Pos
bigDataUrl sertoli.rnaseq.pos.bw
shortLabel sertoli.Pos
longLabel sertoli.rnaseq.pos.bw
parent RNA_Seq
type bigWig
color 255,255,0

track eiNSC_Pos
bigDataUrl eiNSC.rnaseq.pos.bw
shortLabel eiNSC.Pos
longLabel eiNSC.rnaseq.pos.bw
parent RNA_Seq
type bigWig
color 255,0,255

track TP16_Neg
bigDataUrl TP16.rnaseq.neg.bw
shortLabel TP16.Neg
longLabel TP16.rnaseq.neg.bw
parent RNA_Seq
type bigWig
color 255,0,0

track TP22_Neg
bigDataUrl TP22.rnaseq.neg.bw
shortLabel TP22.Neg
longLabel TP22.rnaseq.neg.bw
parent RNA_Seq
type bigWig
color 0,255,0

track TP23_Neg
bigDataUrl TP23.rnaseq.neg.bw
shortLabel TP23.Neg
longLabel TP23.rnaseq.neg.bw
parent RNA_Seq
type bigWig
color 0,0,255

track sertoli_Neg
bigDataUrl sertoli.rnaseq.neg.bw
shortLabel sertoli.Neg
longLabel sertoli.rnaseq.neg.bw
parent RNA_Seq
type bigWig
color 255,255,0

track eiNSC_Neg
bigDataUrl eiNSC.rnaseq.neg.bw
shortLabel eiNSC.Neg
longLabel eiNSC.rnaseq.neg.bw
parent RNA_Seq
type bigWig
color 255,0,255

{% endhighlight %}

{% highlight bash %}
# help : http://genome.ucsc.edu/goldenPath/help/hgTrackHubHelp.html

track NSC
container multiWig
shortLabel NSC
longLabel NSC
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
windowingFunction mean+whiskers
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks
maxHeightPixels 100:60:8

track NSC_Rip
bigDataUrl P16.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel NSC.Rip
longLabel NSC.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent NSC
type bigWig
color 0,102,255

track NSC_Ctl
bigDataUrl TP16.tophat.corrected.uniq.self.normalized_by_wigsum.bw
shortLabel TNSC.Ctl
longLabel TNSC.tophat.corrected.uniq.self.normalized_by_wigsum.bw
parent NSC
type bigWig
color 136,102,255

track eiNSC
container multiWig
shortLabel eiNSC
longLabel eiNSC
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
windowingFunction mean+whiskers
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks
maxHeightPixels 100:60:8

track eiNSC_Rip
bigDataUrl ES_iNSC.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel eiNSC.Rip
longLabel ES_iNSC.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent eiNSC
type bigWig
color 0,102,255

track eiNSC_Ctl
bigDataUrl ES_iNSC.input.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel eiNSC.Ctl
longLabel ES_iNSC.input.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent eiNSC
type bigWig
color 136,102,255

track tNSC
container multiWig
shortLabel tNSC
longLabel tNSC
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
windowingFunction mean+whiskers
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks
maxHeightPixels 100:60:8

track tNSC_Rip
bigDataUrl P23.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel tNSC.Rip
longLabel tNSC.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent tNSC
type bigWig
color 0,102,255

track tNSC_Ctl
bigDataUrl TP23.tophat.corrected.uniq.self.normalized_by_wigsum.bw
shortLabel TtNSC.Ctl
longLabel TtNSC.tophat.corrected.uniq.self.normalized_by_wigsum.bw
parent tNSC
type bigWig
color 136,102,255

track ESC
container multiWig
shortLabel ESC
longLabel ESC
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
windowingFunction mean+whiskers
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks
maxHeightPixels 100:60:8

track ESC_Rip
bigDataUrl ESC.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel ESC.Rip
longLabel ESC.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent ESC
type bigWig
color 0,102,255

track ESC_Ctl
bigDataUrl ESC.input.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel ESC.Ctl
longLabel ESC.input.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent ESC
type bigWig
color 136,102,255

track iPS
container multiWig
shortLabel iPS
longLabel iPS
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
windowingFunction mean+whiskers
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks
maxHeightPixels 100:60:8

track iPS_Rip
bigDataUrl P22.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel iPS.Rip
longLabel iPS.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent iPS
type bigWig
color 0,102,255

track iPS_Ctl
bigDataUrl TP22.tophat.corrected.uniq.self.normalized_by_wigsum.bw
shortLabel TiPS.Ctl
longLabel TiPS.tophat.corrected.uniq.self.normalized_by_wigsum.bw
parent iPS
type bigWig
color 136,102,255

track Sertoli
container multiWig
shortLabel Sertoli
longLabel Sertoli
type bigWig
#viewLimits 0:160
visibility full
aggregate transparentOverlay
showSubtrackColorOnUi on
windowingFunction mean+whiskers
priority 1.2
configurable on
autoScale on
dragAndDrop subtracks
maxHeightPixels 100:60:8

track Sertoli_Rip
bigDataUrl sertoli.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel Sertoli.Rip
longLabel Sertoli.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent Sertoli
type bigWig
color 0,102,255

track Sertoli_Ctl
bigDataUrl sertoli.input.accepted_hits.uniq_extend.normalized_by_wigsum.bw
shortLabel Sertoli.Ctl
longLabel Sertoli.input.accepted_hits.uniq_extend.normalized_by_wigsum.bw
parent Sertoli
type bigWig
color 136,102,255

{% endhighlight %}

3.UCSC输出eps或pdf  
a. To print or save the image to a file:

<table>
  <tr>
    <td valign="top" width="20">
      <b>1.</b>
    </td>
    
    <td>
      In the blue navigation bar at the top of the screen, from the "View" menu, click the "PDF/PS" link.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="20">
      <b>2.</b>
    </td>
    
    <td>
      Click one of the PDF or EPS links.
    </td>
  </tr>
</table>

<pre>b.We will work on fixing it, but in the
&gt; &gt; meantime, you can still get to the page where you can export .eps files
&gt; &gt; by altering your URL. If you add "hgGenome_doPsOutput=1" right after
&gt; &gt; the "?" and add an "&" right after it, you should get to the
&gt; &gt; "PostScript/PDF Output" screen. Your altered URL will look something
&gt; &gt; like this:
&gt; &gt;
&gt; &gt; 
&gt; <a href="http://genome.ucsc.edu/cgi-bin/hgGenome?hgGenome_doPsOutput=1&hgsid=301123643&clade=mammal&org=Human&db=hg19&hgGenome_threshold_hg19=3.5&hgGenome_graph_hg19_1_1=ct_UserTrack1_8429&hgGenome_graphColor_hg19_1_1=blue&hgGenome_graph_hg19_1_2=&hgGenome_graphColor_hg19_1_2=red" target="_blank">http://genome.ucsc.edu/cgi-bin/hgGenome?hgGenome_doPsOutput= 1&hgsid=301123643&clade=mammal&org=Human&db= hg19&hgGenome_threshold_hg19=3.5&hgGenome_graph_hg19 _1_1=ct_UserTrack1_8429&hgGenome_graphColor_hg19_1_1=blu e&hgGenome_graph_hg19_1_2=&hgGenome_graphColor_hg19_ 1_2=red</a>
<a href="http://redmine.soe.ucsc.edu/forum/index.php?t=msg&goto=11357&S=5c52b567667756e3c66db0714f1f779f">http://redmine.soe.ucsc.edu/forum/index.php?t=msg&goto=11357&S=5c52b567667756e3c66db0714f1f779f</a>
</pre>
