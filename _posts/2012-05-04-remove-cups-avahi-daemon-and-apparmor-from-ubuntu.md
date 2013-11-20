---
title: Remove CUPS, Avahi-daemon, and Apparmor from Ubuntu
author: 悟道
layout: post
permalink: /?p=2064
categories:
  - linux
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

CUPS is the standards-based, open source printing system developed by Apple Inc. used not only on Linux system but MacOSX as well.

AppArmor (“Application Armor”) is a security module for the Linux kernel, released under the GNU General Public License. AppArmor allows the system administrator to associate with each program a security profile that restricts the capabilities of that program.

Avahi is a system which facilitates service discovery on a local network via the mDNS/DNS-SD protocol suite. This enables you to plug your laptop or computer into a network and instantly be able to view other people who you can chat with, find printers to print to or find files being shared.

To remove these applications they must be disabled and removed by managing the services through ‘update-rc.d’. To do this first issue the following commands:

<pre># sudo update-rc.d avahi-daemon disable
# sudo update-rc.d apparmor disable
# sudo update-rc.d cups disable</pre>

Now the services can be stopped using the scripts in the /etc/init.d/ directory.

<pre># sudo /etc/init.d/cups stop
# sudo /etc/init.d/avahi-daemon stop
# sudo /etc/init.d/apparmor stop</pre>

Now that the services are stopped we can go ahead and remove them.

<pre># sudo update-rc.d -f apparmor remove
# sudo update-rc.d -f avahi-daemon remove
# sudo update-rc.d -f cups remove</pre>

Now we can uninstall through Aptitude Package Manager.

<pre># sudo apt-get remove avahi-daemon avahi-utils cups apparmor</pre>

That’s it! Reboot and run the below commands to verify all services have stopped and are not running on any ports.

<pre># psaux |  more
# netstat -an | more

http://bullyvard.wordpress.com/2012/02/05/remove-cups-avahi-daemon-and-apparmor-from-ubuntu/</pre>