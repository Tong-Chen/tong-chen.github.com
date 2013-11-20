---
title: 记录SHELL终端命令及其输出
author: 悟道
layout: post
permalink: /?p=520
categories:
  - bash
  - 转载
tags:
  - bash
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

对终端输出进行复制粘贴可能非常乏味，我们使用一个叫做*script*的鲜为人知的程序来解决这个问题，它是大多数Linux产品util-linux软件包的一部分。

*script*记录会话的一切内容：你输入的内容和你看到的内容。它甚至记录颜色；因此如果你的命令提示符或程序输出中包含颜色，*script*将记录它。

要使用*script*，简单执行以下命令：

*$ script*

*<span style="color: #ff0000;">（$script -a -f通常这么使用， 可以打开man查看参数意义）</span>  
*

默认情况下，它向当前目录的*typescript*文件中写入内容。然后，你输入的一切内容都被记录到那个文件中。要往另一个文件中记录日志，只需使用*script/path/to/file*命令。

完成记录后，输入*exit*退出。这个命令将关闭*script*会话并保存文件。现在你可以使用*cat*或其它任何程序来检查日志文件。

使用*script*的缺点在于，它记录所有特殊的字符；因此你输入的文件中将充满控制字符和ANSI转义序列。你可以在*script*中使用一个非常简单的shell来解决这个问题：

$ <span style="color: #ff0000;">SHELL=/bin/sh PS1=&#8221;$ &#8221; script</span>

**使用*script*时，不要使用交互式程序或处理窗口的程序，如*vior top*，它们会破坏会话的输出结果。****（经测试，可以记录终端中启动的R、python、mysql命令）。**

另外，日志文件会记录你使用的任何命令行程序和你完成一项任务所采取的步骤。如果你需要在脚本中编辑一个文件，考虑退出*script*会话，然后用*script –a*（它在旧会话后添加新会话）对文件进行编辑后再重新启动会话。

尝试在.bashrc中写入命令以便打开终端即可执行script，但是总是卡死，尚未解决。

参考：http://www.builder.com.cn/2007/0313/381363.shtml