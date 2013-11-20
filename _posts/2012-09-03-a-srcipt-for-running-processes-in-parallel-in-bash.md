---
title: A srcipt for running processes in parallel in Bash
author: 悟道
layout: post
permalink: /?p=2466
categories:
  - bash
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

## A srcipt for running processes in parallel in Bash

May 22, 2008 — kawakamasu

<div>
  <p>
    In Bash you can start new processes (theads) on the background simply by running a command with ampersand &. The <code>wait</code> command can be used to wait until all background processes have finished (to wait for a certain process do <code>wait PID</code> where <code>PID</code> is a process ID). So here’s a simple pseudocode for parallel processing:
  </p>
  
  <p>
    &nbsp;
  </p>
  
  <div id="highlighter_862015">
    <div>
      <div>
        <table>
          <tr>
            <td>
              <code>1</code>
            </td>
            
            <td>
              <code>for</code> <code>ARG</code> <code>in</code>  <code>$*; </code><code>do</code>
            </td>
          </tr>
        </table>
      </div>
      
      <div>
        <table>
          <tr>
            <td>
              <code>2</code>
            </td>
            
            <td>
              <code>    </code><code>command </code><code>$ARG</code> <code>&</code>
            </td>
          </tr>
        </table>
      </div>
      
      <div>
        <table>
          <tr>
            <td>
              <code>3</code>
            </td>
            
            <td>
              <code>    </code><code>NPROC</code><code>=$((</code><code>$NPROC</code><code>+</code><code>1</code><code>))</code>
            </td>
          </tr>
        </table>
      </div>
      
      <div>
        <table>
          <tr>
            <td>
              <code>4</code>
            </td>
            
            <td>
              <code>    </code><code>if</code> <code>[ </code><code>"$NPROC"</code> <code>-ge </code><code>4</code> <code>]; </code><code>then</code>
            </td>
          </tr>
        </table>
      </div>
      
      <div>
        <table>
          <tr>
            <td>
              <code>5</code>
            </td>
            
            <td>
              <code>        </code><code>wait</code>
            </td>
          </tr>
        </table>
      </div>
      
      <div>
        <table>
          <tr>
            <td>
              <code>6</code>
            </td>
            
            <td>
              <code>        </code><code>NPROC</code><code>=</code><code></code>
            </td>
          </tr>
        </table>
      </div>
      
      <div>
        <table>
          <tr>
            <td>
              <code>7</code>
            </td>
            
            <td>
              <code>    </code><code>fi</code>
            </td>
          </tr>
        </table>
      </div>
      
      <div>
        <table>
          <tr>
            <td>
              <code>8</code>
            </td>
            
            <td>
              <code>done</code>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
  
  <p>
    &nbsp;
  </p>
  
  <p>
    I.e. you run 4 processes at a time and wait until all of them have finished before executing the next four. This is a sufficient solution if all of the processes take equally long to finish. However this is suboptimal if running time of the processes vary a lot.
  </p>
  
  <p>
    A better solution is to track the process IDs and poll if all of them are still running. In Bash <code>$!</code> returns the ID of last initiated background process. If a process is running, the corresponding PID is found in directory <code>/proc/</code>.
  </p>
  
  <p>
    Based on the ideas given in a Ubuntu forum <a href="http://ubuntuforums.org/showthread.php?t=31339">thread</a> and a <a href="http://unmaintainable.wordpress.com/2007/08/05/cmdline-options-in-shell-scripts/">template</a> on command line parsing, I wrote a simple script “<code>parallel</code>” that allows you to run virtually any simple command concurrently.
  </p>
  
  <p>
    Assume that you have a program <code>proc</code> and you want to run something like <code>proc *.jpg</code> using three concurrent processes. Then simply do<br /> <code>&lt;br />
parallel -j 3 proc *.jpg&lt;br />
</code><br /> The script takes care of dividing the task. Obviously <code>-j 3</code> stands for three simultaneous jobs.<br /> If you need command line options, use quotes to separate the command from the variable arguments, e.g.<br /> <code>&lt;br />
parallel -j 3 "proc -r -A=40" *.jpg&lt;br />
</code><br /> Furthermore, <code>-r</code> allows even more sophisticated commands by replacing asterisks in the command string by the argument:<br /> <code>&lt;br />
parallel -j 6 -r "convert -scale 50% * small/small_*" *.jpg&lt;br />
</code><br /> I.e. this executes <code>convert -scale 50% file1.jpg small/small_file1.jpg</code> for all the jpg files. This is a real-life example for scaling down images by 50% (requires imagemagick).
  </p>
  
  <p>
    Finally, here’s the script. It can be easily manipulated to handle different jobs, too. Just write your command between <code>#DEFINE COMMAND</code> and <code>#DEFINE COMMAND END</code>.
  </p>
  
  <p>
    &nbsp;
  </p>
</div>

<div class="wp_codebox">
  <table>
    <tr id="p2466167">
      <td class="code" id="p2466code167">
        <pre class="bash" style="font-family:monospace;">&nbsp;
<span style="color: #666666; font-style: italic;">#!/bin/bash</span>
<span style="color: #007800;">NUM</span>=<span style="color: #000000;"></span>
<span style="color: #007800;">QUEUE</span>=<span style="color: #ff0000;">""</span>
<span style="color: #007800;">MAX_NPROC</span>=<span style="color: #000000;">2</span> <span style="color: #666666; font-style: italic;"># default</span>
<span style="color: #007800;">REPLACE_CMD</span>=<span style="color: #000000;"></span> <span style="color: #666666; font-style: italic;"># no replacement by default</span>
<span style="color: #007800;">USAGE</span>=<span style="color: #ff0000;">"A simple wrapper for running processes in parallel.
Usage: <span style="color: #780078;">`basename $0`</span> [-h] [-r] [-j nb_jobs] command arg_list
 	-h		Shows this help
	-r		Replace asterix * in the command string with argument
	-j nb_jobs 	Set number of simultanious jobs [2]
 Examples:
 	<span style="color: #780078;">`basename $0`</span> somecommand arg1 arg2 arg3
 	<span style="color: #780078;">`basename $0`</span> -j 3 <span style="color: #000099; font-weight: bold;">\"</span>somecommand -r -p<span style="color: #000099; font-weight: bold;">\"</span> arg1 arg2 arg3
 	<span style="color: #780078;">`basename $0`</span> -j 6 -r <span style="color: #000099; font-weight: bold;">\"</span>convert -scale 50% * small/small_*<span style="color: #000099; font-weight: bold;">\"</span> *.jpg"</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">function</span> queue <span style="color: #7a0874; font-weight: bold;">&#123;</span>
	<span style="color: #007800;">QUEUE</span>=<span style="color: #ff0000;">"<span style="color: #007800;">$QUEUE</span> $1"</span>
	<span style="color: #007800;">NUM</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">$NUM</span>+<span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">function</span> regeneratequeue <span style="color: #7a0874; font-weight: bold;">&#123;</span>
	<span style="color: #007800;">OLDREQUEUE</span>=<span style="color: #007800;">$QUEUE</span>
	<span style="color: #007800;">QUEUE</span>=<span style="color: #ff0000;">""</span>
	<span style="color: #007800;">NUM</span>=<span style="color: #000000;"></span>
	<span style="color: #000000; font-weight: bold;">for</span> PID <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #007800;">$OLDREQUEUE</span>
	<span style="color: #000000; font-weight: bold;">do</span>
		<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #660033;">-d</span> <span style="color: #000000; font-weight: bold;">/</span>proc<span style="color: #000000; font-weight: bold;">/</span><span style="color: #007800;">$PID</span>  <span style="color: #7a0874; font-weight: bold;">&#93;</span> ; <span style="color: #000000; font-weight: bold;">then</span>
			<span style="color: #007800;">QUEUE</span>=<span style="color: #ff0000;">"<span style="color: #007800;">$QUEUE</span> <span style="color: #007800;">$PID</span>"</span>
			<span style="color: #007800;">NUM</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #007800;">$NUM</span>+<span style="color: #000000;">1</span><span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
		<span style="color: #000000; font-weight: bold;">fi</span>
	<span style="color: #000000; font-weight: bold;">done</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">function</span> checkqueue <span style="color: #7a0874; font-weight: bold;">&#123;</span>
	<span style="color: #007800;">OLDCHQUEUE</span>=<span style="color: #007800;">$QUEUE</span>
	<span style="color: #000000; font-weight: bold;">for</span> PID <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #007800;">$OLDCHQUEUE</span>
	<span style="color: #000000; font-weight: bold;">do</span>
		<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #000000; font-weight: bold;">!</span> <span style="color: #660033;">-d</span> <span style="color: #000000; font-weight: bold;">/</span>proc<span style="color: #000000; font-weight: bold;">/</span><span style="color: #007800;">$PID</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span> ; <span style="color: #000000; font-weight: bold;">then</span>
			regeneratequeue <span style="color: #666666; font-style: italic;"># at least one PID has finished</span>
			<span style="color: #7a0874; font-weight: bold;">break</span>
		<span style="color: #000000; font-weight: bold;">fi</span>
	<span style="color: #000000; font-weight: bold;">done</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #666666; font-style: italic;"># parse command line</span>
<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #007800;">$#</span> <span style="color: #660033;">-eq</span> <span style="color: #000000;"></span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span> <span style="color: #666666; font-style: italic;">#  must be at least one arg</span>
	<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"<span style="color: #007800;">$USAGE</span>"</span> <span style="color: #000000; font-weight: bold;">&gt;&</span><span style="color: #000000;">2</span>
	<span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span>
<span style="color: #000000; font-weight: bold;">fi</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #7a0874; font-weight: bold;">getopts</span> j:rh OPT; <span style="color: #000000; font-weight: bold;">do</span> <span style="color: #666666; font-style: italic;"># "j:" waits for an argument "h" doesnt</span>
    <span style="color: #000000; font-weight: bold;">case</span> <span style="color: #007800;">$OPT</span> <span style="color: #000000; font-weight: bold;">in</span>
	h<span style="color: #7a0874; font-weight: bold;">&#41;</span>	<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"<span style="color: #007800;">$USAGE</span>"</span>
		<span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;"></span> <span style="color: #000000; font-weight: bold;">;;</span>
	j<span style="color: #7a0874; font-weight: bold;">&#41;</span>	<span style="color: #007800;">MAX_NPROC</span>=<span style="color: #007800;">$OPTARG</span> <span style="color: #000000; font-weight: bold;">;;</span>
	r<span style="color: #7a0874; font-weight: bold;">&#41;</span>	<span style="color: #007800;">REPLACE_CMD</span>=<span style="color: #000000;">1</span> <span style="color: #000000; font-weight: bold;">;;</span>
	\?<span style="color: #7a0874; font-weight: bold;">&#41;</span>	<span style="color: #666666; font-style: italic;"># getopts issues an error message</span>
		<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"<span style="color: #007800;">$USAGE</span>"</span> <span style="color: #000000; font-weight: bold;">&gt;&</span><span style="color: #000000;">2</span>
		<span style="color: #7a0874; font-weight: bold;">exit</span> <span style="color: #000000;">1</span> <span style="color: #000000; font-weight: bold;">;;</span>
    <span style="color: #000000; font-weight: bold;">esac</span>
<span style="color: #000000; font-weight: bold;">done</span>
&nbsp;
<span style="color: #666666; font-style: italic;"># Main program</span>
<span style="color: #7a0874; font-weight: bold;">echo</span> Using <span style="color: #007800;">$MAX_NPROC</span> parallel threads
<span style="color: #7a0874; font-weight: bold;">shift</span> <span style="color: #000000; font-weight: bold;">`</span><span style="color: #c20cb9; font-weight: bold;">expr</span> <span style="color: #007800;">$OPTIND</span> - <span style="color: #000000;">1</span><span style="color: #000000; font-weight: bold;">`</span> <span style="color: #666666; font-style: italic;"># shift input args, ignore processed args</span>
<span style="color: #007800;">COMMAND</span>=<span style="color: #007800;">$1</span>
<span style="color: #7a0874; font-weight: bold;">shift</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">for</span> INS <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #007800;">$*</span> <span style="color: #666666; font-style: italic;"># for the rest of the arguments</span>
<span style="color: #000000; font-weight: bold;">do</span>
	<span style="color: #666666; font-style: italic;"># DEFINE COMMAND</span>
	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #007800;">$REPLACE_CMD</span> <span style="color: #660033;">-eq</span> <span style="color: #000000;">1</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">then</span>
		<span style="color: #007800;">CMD</span>=<span style="color: #800000;">${COMMAND//"*"/$INS}</span>
	<span style="color: #000000; font-weight: bold;">else</span>
		<span style="color: #007800;">CMD</span>=<span style="color: #ff0000;">"<span style="color: #007800;">$COMMAND</span> <span style="color: #007800;">$INS</span>"</span> <span style="color: #666666; font-style: italic;">#append args</span>
	<span style="color: #000000; font-weight: bold;">fi</span>
	<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"Running <span style="color: #007800;">$CMD</span>"</span> 
&nbsp;
	<span style="color: #007800;">$CMD</span> <span style="color: #000000; font-weight: bold;">&</span>
	<span style="color: #666666; font-style: italic;"># DEFINE COMMAND END</span>
&nbsp;
	<span style="color: #007800;">PID</span>=<span style="color: #007800;">$!</span>
	queue <span style="color: #007800;">$PID</span>
&nbsp;
	<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #007800;">$NUM</span> <span style="color: #660033;">-ge</span> <span style="color: #007800;">$MAX_NPROC</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>; <span style="color: #000000; font-weight: bold;">do</span>
		checkqueue
		<span style="color: #c20cb9; font-weight: bold;">sleep</span> <span style="color: #000000;">0.4</span>
	<span style="color: #000000; font-weight: bold;">done</span>
<span style="color: #000000; font-weight: bold;">done</span>
<span style="color: #7a0874; font-weight: bold;">wait</span> <span style="color: #666666; font-style: italic;"># wait for all processes to finish before exit</span></pre>
      </td>
    </tr>
  </table>
</div>