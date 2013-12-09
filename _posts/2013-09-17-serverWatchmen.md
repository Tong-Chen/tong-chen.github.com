---
title: A script to monitor the running programs in the server
layout: post
categories:
  - bash
  - letter
  - linux
tags:
  - bash
  - linuc
---

Recently, the server has been crashed frequently for programs costing most of the memories. To avoid this, two suggestions are prosed.

* One is more flexible by changing the maximum memory usage for one user locally or globally. Here I suggest users set this variable locally in case they want to run programs need lots of memories by adding `ulimit -v 30000000` to `.bash_profiles` (30,000,000 means maximum 30G is allowed). If one want to run programs cost larger than 30G RAM, just change this value and *re-login*.

* Another is running the following program `serverWatchman` to kill programs cost more than 90% memories.

{% highlight bash %}
#!/bin/bash

#84G is the maximally allowed total memory usage.
maxmem=84

while true
do
	mem=`free -g | grep -- '^-' | awk '{print $3}'`
	echo ${mem}
	echo ${maxmem}
	if [ ${mem} -gt ${maxmem} ]; then
		info=`ps aux | sort -k4nr | head -n 1`
		id=`echo ${info} | awk '{print $2}'`
		#echo $id
		echo ${info} | wall
		kill -9 $id
		# Be merciful, grieve the death of the process
		sleep 60s
		#exit 1
		#maxmem=10000
	fi
	sleep 5s
done
{% endhighlight %}
