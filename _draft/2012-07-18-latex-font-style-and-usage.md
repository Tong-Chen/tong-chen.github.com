---
title: latex font style and usage
author: 悟道
layout: post
permalink: /?p=2226
categories:
  - tex
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.XeTeX relies on OS-specific libraries to load fonts. In case of Linux it is the fontconfig library. It&#8217;s quite easy for basic use.

If the font is already installed in the system (and many will be), it can be selected simply by its name. You can find out the precise name to use by issuing **fc-list** and examining the output (perhaps with the help of grep).  
If the font is not listed, it can be installed manually. Fonts can be installed system-wise or user-wise. I recommend the second way, because it does not require additional privileges and won&#8217;t pollute the system directories. To install a font, simply place it in the **.fonts** directory in your home directory. You may need to create the directory if it doesn&#8217;t exist, and you may need to enable display of hidden files to see this directory in your file manager. Once the font has been placed in the directory, run fc-cache to regenerate the font cache, then try the first step again.

http://tex.stackexchange.com/questions/43591/how-to-change-default-font-to-rockwell

Install the fonts in `/usr/local/share/fonts` if you want them system-wide or in `~/.fonts` if you want them only for the current user.

You can then check for the font in `fc-list`:

>     fc-list : family file | grep -i fontin /usr/local/share/fonts/Fontin-SmallCaps.otf: Fontin SmallCaps,Fontin /usr/local/share/fonts/Fontin-Italic.otf: Fontin /usr/local/share/fonts/Fontin-Bold.otf: Fontin /usr/local/share/fonts/Fontin-Regular.otf: Fontin

which gives you the name to use in XeTeX (using `fontspec`). For example:

>     \setmainfont{Fontin} 

    http://tex.stackexchange.com/questions/27659/how-to-use-downloaded-fonts-with-xetex-on-ubuntu 

2.