---
title: gImageReader：从PDF和图像文件中导出文字
author: 悟道
layout: post
permalink: /?p=634
categories:
  - 转载
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

gImageReader是tesseract-ocr的一个GTK图形前端。如图：

[<img title="gimagereader" src="http://www.ubuntusoft.com/wp-content/uploads/2011/01/gimagereader.png" alt="" width="400" height="262" />][1]

Tesseract是一个OCR引擎，它可以识别图形中的文字。但不带文档输出分析，没有输出格式和图形用户界面。

gImageReader可以从图像或PDF文件中导出文字。它支持列选择和部分文档的功能，也可以打开多页面的PDF或图像文件，支持所有的图形格式，能只转化选定区域的文字。

**可选项：在UBUNTU 10.04和10.10中安装Tesseract OCR 3.0 SVN**

尽管Tesseract OCR 3.0仍在开发中，但比现在的稳定版要好很多。而且这个PPA中还包括很多语言包，所以，尽管这是一个可选项，仍然强力推荐。

**警告：安装完最新版Tesseract之后要马上禁用这个PPA源，因为它还包含一些很有风险的程序包。**

添加PPA源并安装Tesseract OCR 3.0 SVN:

sudo add-apt-repository ppa:alex-p/notesalexp

sudo apt-get update

sudo apt-get install tesseract-ocr

这个源中还包含了一些其他的语言包，比如德文，法文之类的（可惜没有中文）。在新立得中搜索tesseract-ocr，找到你需要的语言包，安装即可。

现在，需要禁用这个PPA，按ALT + F2，输入：

gksu software-properties-gtk

然后，在“其它软件”选项卡中找到”http://ppa.launchpad.net/alex-p/notesalexp”这一行，去掉前面的勾或者直接删除它。

**gImageReader**

gImageReader既可以在LINUX中使用也可以在WINDOWS中使用。可以在[这里][2]下载（.deb, .rpm 或 .exe 文件都有）

安装之后，选择你想要转化成文本的PDF或图像，如果转化整个文件就点击”Recognize all”，如果不是，用鼠标选中你想转化的那一部分点击”Recognize selection”

如果PDF文件或图像文件对应的语言包尚未安装，gImageReader会自动探测语言。

原文链接：[webupd8][3]

转自：[ubuntuhome][4]

转载本站文章请注明，转载自：**UbuntuSoft**[[http://www.ubuntusoft.com][5]]  
本文链接: [http://www.ubuntusoft.com/gimagereader-pdf-and-image-files-from-the-exported-text][6]

 [1]: http://www.ubuntusoft.com/wp-content/uploads/2011/01/gimagereader.png
 [2]: http://sourceforge.net/projects/gimagereader/
 [3]: http://www.ubuntuhome.com/www.webupd8.org/2011/01/extract-text-from-pdfs-and-images-with.html
 [4]: http://www.ubuntuhome.com/gimagereader-extract-text-from-pdf-or-image.html
 [5]: http://www.ubuntusoft.com/
 [6]: http://www.ubuntusoft.com/gimagereader-pdf-and-image-files-from-the-exported-text "gImageReader：从PDF和图像文件中导出文字"