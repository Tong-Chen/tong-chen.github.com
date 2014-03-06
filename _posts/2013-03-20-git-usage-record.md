---
title: Tutorial for git usage
author: 悟道
layout: post
categories:
  - git
  - letter
tags:
  - git
---

#### Git initialize a repository locally

{% highlight bash %}
#!/bin/bash

#set -x
set -e
set -u

if test $# -lt 1; then
        echo 1>&2 "Usage $0 dir_name_in_github"
        exit 1
fi

git init
git add *
git commit -m " Organized ones" 
git remote add origin git@github.com:NAME/$1.git
git push -u origin master
{% endhighlight %}

After you run this script, you can get a directory `.git`, check the `config` file within.
{% highlight bash %}
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
[remote "origin"]
		#ssh verification 
        url = git@github.com:NAME/Pot.git
		#or user-name password verification
		#url = https://github.com/NAME/NS.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master
{% endhighlight %}

#### Git update files (use `gitUpdate.sh "*"` for multiple files)

{% highlight bash %}
#!/bin/bash

#set -x
set -e
set -u

if test $# -lt 2; then
        echo 1>&2 "Usage $0 file commit"
        exit 1
fi

git add $1
git commit -m "$2 FOR <$1>" 
git push -u origin master

{% endhighlight %}

#### git中查看文件的差异

{% highlight bash %}
#显示在当前的工作目录里的，没有staged(添加到索引中)，且在下次提交时不会被提交的修改。
# + 或绿色标记的行为所要内同
git diff  

#如果你要看在下次提交时要提交的内容(staged,添加到索引中)
git diff --cached
{% endhighlight %}

#### git删除版本库中的一个提交。

{% highlight bash %}
如果没有git push的话，可以先通过git log查询出上一个版本的SHA码，然后git reset XXXXX退回到上一个版本.
{% endhighlight %}

#### git中合并几次提交

{% highlight bash %}
通过git log找到最想要的版本的SHA码，然后git reset SHA码，这样中间状态被消除，但是程序却没有变，再执行add-commit，提交就可以了。
{% endhighlight %}


Ref：http://gitbook.liuhui998.com/3_5.html
