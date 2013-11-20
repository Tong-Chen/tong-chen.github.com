---
title: 'dpkg: dependency problems prevent configuration of linux-generic-pae'
author: 悟道
layout: post
permalink: /?p=3226
categories:
  - linux
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<pre></pre>

chentong@chentong-Lenovo-Product:~/Desktop/dai$** sudo apt-get remove &#8211;purge linux-image-3.2.0-53-generic-pae**  
Reading package lists&#8230; Done  
Building dependency tree  
Reading state information&#8230; Done  
You might want to run &#8216;apt-get -f install&#8217; to correct these:  
The following packages have unmet dependencies:  
linux-generic-pae : Depends: linux-image-generic-pae (= 3.2.0.41.49) but 3.2.0.53.63 is to be installed  
Depends: linux-headers-generic-pae (= 3.2.0.41.49) but 3.2.0.53.63 is to be installed  
linux-image-generic-pae : Depends: linux-image-3.2.0-53-generic-pae but it is not going to be installed  
E: Unmet dependencies. Try &#8216;apt-get -f install&#8217; with no packages (or specify a solution).  
chentong@chentong-Lenovo-Product:~/Desktop/dai$ sudo apt-get -f install  
Reading package lists&#8230; Done  
Building dependency tree  
Reading state information&#8230; Done  
Correcting dependencies&#8230; Done  
The following packages were automatically installed and are no longer required:  
libopencv-highgui2.3 libdc1394-22 libopencv-imgproc2.3 libopencv-core2.3  
Use &#8216;apt-get autoremove&#8217; to remove them.  
The following extra packages will be installed:  
linux-generic-pae  
The following packages will be upgraded:  
linux-generic-pae  
1 upgraded, 0 newly installed, 0 to remove and 322 not upgraded.  
1 not fully installed or removed.  
Need to get 0 B/1,726 B of archives.  
After this operation, 0 B of additional disk space will be used.  
Do you want to continue [Y/n]? y  
**dpkg: dependency problems prevent configuration of linux-generic-pae:**  
** linux-generic-pae depends on linux-image-generic-pae (= 3.2.0.41.49); however:**  
** Version of linux-image-generic-pae on system is 3.2.0.53.63.**  
** linux-generic-pae depends on linux-headers-generic-pae (= 3.2.0.41.49); however:**  
** Version of linux-headers-generic-pae on system is 3.2.0.53.63.**  
**dpkg: error processing linux-generic-pae (&#8211;configure):**  
dependency problems &#8211; leaving unconfigured  
No apport report written because the error message indicates its a followup error from a previous failure.  
Errors were encountered while processing:  
linux-generic-pae  
E: Sub-process /usr/bin/dpkg returned an error code (1)  
chentong@chentong-Lenovo-Product:~/Desktop/dai$ **sudo dpkg &#8211;remove linux-generic-pae**  
(Reading database &#8230; 367914 files and directories currently installed.)  
Removing linux-generic-pae &#8230;  
chentong@chentong-Lenovo-Product:~/Desktop/dai$ **sudo apt-get install linux-generic-pae**  
Reading package lists&#8230; Done  
Building dependency tree  
Reading state information&#8230; Done  
The following packages were automatically installed and are no longer required:  
libopencv-highgui2.3 libdc1394-22 libopencv-imgproc2.3 libopencv-core2.3  
Use &#8216;apt-get autoremove&#8217; to remove them.  
The following NEW packages will be installed:  
linux-generic-pae  
0 upgraded, 1 newly installed, 0 to remove and 322 not upgraded.  
Need to get 0 B/1,726 B of archives.  
After this operation, 32.8 kB of additional disk space will be used.  
Selecting previously unselected package linux-generic-pae.  
(Reading database &#8230; 367912 files and directories currently installed.)  
Unpacking linux-generic-pae (from &#8230;/linux-generic-pae\_3.2.0.53.63\_i386.deb) &#8230;  
Setting up linux-generic-pae (3.2.0.53.63) &#8230;

&nbsp;

<http://askubuntu.com/questions/251862/broken-count-error-linux-generic-pae-depends-linux-image-generic-pae-3-2>