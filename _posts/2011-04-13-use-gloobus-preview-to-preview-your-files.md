---
title: Use Gloobus Preview to preview your files
author: 悟道
layout: post
permalink: /?p=825
categories:
  - 默认
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

There are many ways to preview your files in Linux. Most often there is a single application used to preview a different file type. You have the Eye of GNOME for images, the Document Viewer for PDFs, and more. But what about a single application that will preview all types? Is there such a thing? Why yes there is. That “thing” is Gloobus Preview. This application is an amazingly flexible tool that can preview a large amount of file types.

Let’s take a look at installing, using, and creating a Nautilus action for Gloobus Preview.

Installation

I am going to illustrate the installation of Gloobus Preview on Ubuntu (10.04 to be exact). Since the PPA has been updated, installing on Ubuntu is quite simple. Just follow these steps:

Open up a terminal window.

Issue the command  
`sudo add-apt-repository ppa:gloobus-dev/gloobus-preview`

Now issue the command  
`sudo apt-get update`

Finally issue the command `sudo apt-get install gloobus-preview`

Once the software is installed you can close the terminal window.

Usage

Using Gloobus Preview is a bit tricky – which is why I want to show you how to add a Nautilus Action for this command. You can see just how Gloobus Preview will work by issuing the gloobus-preview command from within a directory that contains a file you want to preview. Say you want to preview the file image.jpg. To open this in Gloobus Preview you would issue the command gloobus-preview image.jpg. When you do this Gloobus Preview will open with the image inside.

As you can see there are two arrow buttons and a square icon. The up arrow changes Gloobus Preview to full screen, the down arrow switches back to normal view, and the square opens the file in the standard, default file type viewer (such as Eye Of GNOME for images).

Nautilus Action

Now, let’s create a Nautilus Action so you can simply right click a file within Nautilus and open that file in Gloobus Preview. To do this open up the Nautilus Actions Configuration tool (click System > Preferences > Nautilus Actions Configuration. From within this tool set up the following configurations:

Under the Action tab:</p> 
Check Display item in selection context menu.

Check Display item in location context menu.

Context label: Gloobus Preview.

Check Display item in the toolbar.

Leave all else default.

Under the Command tab:

Change the command path to /usr/bin/gloobus-preview.

Change the Parameters to %M</ul> 
That’s it. Now click the Save button and you’re almost ready to test it out. Before you test it, however, you need to restart Nautilus. To do this click** ALT-F2** and, in the run dialog, enter **nautilus -q**. Now open up Nautilus to a directory containing any of the following file types:

Images: jpeg, png, icns, bmp, svg, gif, psd, xcf  
Documents: pdf, cbr, cbz, doc, xls, odf, ods, odp, ppt  
Source: c++, c#, java, javascript, php, xml, log, sh, python  
Audio: mp3, ogg, midi, 3gp, wav  
Video: mpg, avi, ogg, 3gp, mkv, flv  
Other: folders, ttf, srt, plain-text

If you right-click any of those files you will see a Gloobus Preview entry in the context menu. Select Gloobus Preview and the file will open up in your newly created Gloobus Preview Action.

From:<a href=http://www.ghacks.net/2010/11/25/use-gloobus-preview-to-preview-your-files/>http://www.ghacks.net/2010/11/25/use-gloobus-preview-to-preview-your-files/</a>