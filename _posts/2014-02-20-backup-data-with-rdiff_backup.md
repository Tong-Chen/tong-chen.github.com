---
title: Backup data using rdiff-backup
author: Chen Tong
layout: post
categories:
  - letter
tags:
  - bash
  - rsync
---

Here summarizes the usages of rdiff-backup to backup files with old version kept also.


#### Mirror backup and incremental backup

`rsync` is a great tool and also a great algorithm to mirror your data to different disks for backup usage. However, with a mirror, any changes made to the source directory are immediately sent to the backup directory, and old changes are lost. Therefor backup tools which can save both original files and changes are required. There are at least three tools can do this, `rdiff-backup`, `duplicity`, and `rsnapshot`. 

`rdiff-backup` creates an exact mirror of the **latest** copy of the data, and stores old versions of files - in fact, diffs between new and old - in a special subdirectory. To recover a file from 4 revisions ago, you start with the latest version and apply the 4 diffs in reverse order. One major disadvantage of `rdiff-backup` besides from the lack of encryption is that it demands that the server also has installed the **exact same version** of `rdiff-backup`.

`duplicity`, on the other hand, starts with a full copy of the **oldest** version of the data, and stores new versions of files as diffs between old and new. So to recreate the latest version of a file, you start with the original, and apply all the diffs required to bring it up to date.

`Rsnapshot` creates a "virtual look" where it appears that **each backup is a full backup**. Rsnapshot uses hard links to achieve the "virtual look" of full backups. The disk space required is just a little more than the space of one full backup, plus incrementals. This is an important feature if disk space is an issue.

Detailed comparison of these tools are referred in following references.


#### Install `rdiff-backup` at both local and remote computers

* Install requirements
  {% highlight bash %}
  #install for ubuntu, debian
  sudo apt-get install python-dev librsync-dev
  #self compile
  #downlaod rsync-dev from https://sourceforge.net/project/showfiles.php?group_id=56125
  tar xvzf librsync-0.9.7.tar.gz
  export CFLAGS="$CFLAGS -fPIC"
  ./configure --prefix=/home/user/rsync --with-pic
  make
  make install
  {% endhighlight %}

* Install rdiff-backup
  {% highlight bash %}
  #See Reference part for download link
  python setup.py install --prefix=/home/user/rdiff-backup
  #If you complied rsync-dev yourself, please specify the location of rsync-dev
  python setup.py --librsync-dir=/home/user/rsync install --prefix=/home/user/rdiff-backup
  {% endhighlight %}

* Add exeutable files and python modules to environmental variables
  {% highlight bash %}
  #Add the following words into .bashrc or .bash_profile or any other config files
  export PATH=${PATH}:/home/user/rdiff-backup/bin
  export PYTHONPATH=${PYTHONPATH}:/home/user/rdiff-backup/lib/python2.x/site-packages
  #pay attention to the x in python2.x of above line which can be 6 or 7 depending on 
  #the Python version used.
  {% endhighlight %}

* Test environmental variable when executing commands through ssh
  {% highlight bash %}
  ssh user@host 'echo ${PATH}' #When I run this command in my local computer, 
						       #I found only system environmetal variable is used 
							   #and none of my self-defined environmetal variable is used.
  #Then, I modified the following lines in file 'SetConnections.py' in 
  #/home/user/rdiff-backup/lib/python2.x/site-packages/rdiff_backup
  #to set environmental explicitly when login.
  #pay attention to the single quote used inside double quote
  __cmd_schema = "ssh -C %s 'source ~/.bash_profile; rdiff-backup --server'"
  __cmd_schema_no_compress = "ssh %s 'source ~/.bash_profile; rdiff-backup --server'"
  #choose the one contains environmental variable for rdiff-backup from .bash_profile and .bashrc.
  {% endhighlight %}


#### Use `rdiff-backup`

* Start backup
  
  * `rdiff-backup --no-compression --print-statistics user@host::/home/user/source_dir destination_dir` 

  * If the `destination_dir` exists, please add `--force` like `rdiff-backup --no-compression --force --print-statistics user@host::/home/user/source_dir destination_dir`. All things in original `destination_dir` will be depleted.

  * If you want to exclude or include special files or dirs please specify like `--exclude '**trash'` or `--include /home/user/source_dir/important`.

* Timely backup your data
  
  * Add the above command into `crontab (hit 'crontab -e' in terminal to open crontab)` in the format like `5   22  */1    *   *   command` which means executing the `command` at 22:05 everyday.

* Restore data 

  * Restore the latest data by running `rdiff-backup -r now destination_dir user@host::/home/user/source_dir.restore`. Add `--force` if you want to restore to `source_dir`.
  * Restore files 10 days ago by running `rdiff-backup -r 10D destination_dir user@host::/home/user/source_dir.restore`. Other acceptable time formats include 5m4s (5 minutes 4 seconds) and 2014-01-01 (January 1st, 2014).
  * Restore files from an increment file by running `rdiff-backup destination_dir/rdiff-backup-data/increments/server_add.2014-02-21T09:22:45+08:00.missing user@host::/home/user/source_dir.restore/server_add`. Increment files are stored in `destination_dir/rdiff-backup-data/increments/server_add.2014-02-21T09:22:45+08:00.missing`.

* Remove older records to save space

  * Deletes all information concerning file versions which have not been current for 2 weeks by running `rdiff-backup --remove-older-than 2W --force destination_dir`. Note that an existing file which has not changed for a year will still be preserved. But a file which was deleted 15 days ago can not be restored after this command. Normally one should use `--force` since it is used to delete multiple increments at the same time which `--remove-older-than` refuses to do by default.
  * Only keeps the last n rdiff-backup sessions by running `rdiff-backup --remove-older-than 20B --force destination_dir`.

* Statistics
  
  * Lists increments in given golder by `rdiff-backup --list-increments destination_dir/`.
  * Lists of files changed in last 5 days by `rdiff-backup --list-changed-since 5D destination_dir/`.
  * Compare the difference between source and bak by `rdiff-backup --compare user@host::source-dir destination_dir`
  * Compare the sifference between source and bak (as it was two weeks ago) by `rdiff-backup --compare-at-time 2W user@host::source-dir destination_dir`.

#### A complete script (automatically sync using `crontab`)

{% highlight bash %}

#!/bin/bash

export PYTHONPATH=${PYTHONPATH}:/soft/rdiff_backup/lib/python2.7/site-packages/

rdiff-backup --no-compression -v5 --exclude '**trash' user@server::source/ bak_dir/

ret=$?
if test $ret -ne 0; then
	echo "Wrong in bak" | mutt -s "Wrong in bak" bak@mail.com
else
	echo "Right in bak" | mutt -s "Right in bak" bak@mail.com
fi

echo "Finish rdiff-backup $0 ---`date`---"  >>bak.log 2>&1


echo "`rdiff-backup --exclude '**trash' --compare-at-time 1D user@server::source/ bak_dir/`" | mutt -s "Lists of baked files" bak@mail.com


{% endhighlight %}

#### References
* [rdiff-backup](http://www.nongnu.org/rdiff-backup/index.html)
* [duplicity](http://www.nongnu.org/duplicity/)
* [rsnapshot](http://www.rsnapshot.org/howto/)
* [http://www.saltycrane.com/blog/2008/02/backup-on-linux-rsnapshot-vs-rdiff/](http://www.saltycrane.com/blog/2008/02/backup-on-linux-rsnapshot-vs-rdiff/)
* [http://james.lab6.com/2008/07/09/rdiff-backup-and-duplicity/](http://james.lab6.com/2008/07/09/rdiff-backup-and-duplicity/)
* [http://bitflop.com/document/75](http://bitflop.com/document/75)
* [http://askubuntu.com/questions/2596/comparison-of-backup-tools](http://askubuntu.com/questions/2596/comparison-of-backup-tools)
* [http://www.reddit.com/r/linux/comments/fgmbb/rdiffbackup_duplicity_or_rsnapshot_which_is/](http://www.reddit.com/r/linux/comments/fgmbb/rdiffbackup_duplicity_or_rsnapshot_which_is/)
* [http://serverfault.com/questions/491341/optimize-space-rdiff-backup](http://serverfault.com/questions/491341/optimize-space-rdiff-backup)
* [Another great post on usage of rdiff-backup](http://bencane.com/2013/05/20/securely-backing-up-your-files-with-rdiff-backup-and-sudo/)
