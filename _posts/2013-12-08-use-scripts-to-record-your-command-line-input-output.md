---
title: Use script and scriptreplay command 
layout: post
description: Introduce a tool to record the typescript of everything printed on your terminal.
categories:
 - bash
 - letter
tags:
 - bash
---

What would you do if you want to share your typescript to others or when you 
try to remember what you have typed to generate this file?

One would say that `history | grep 'things'` is a good choice. 

Of course, it is only a `good` choice until I find a great solution at 
[stackoverflow.](http://stackoverflow.com/questions/945288/saving-current-directory-to-bash-history/960684#960684)

However, today I will introduce another command `script` to record commands 
