---
title: Tips for LaTex usages
layout: post
categories:
    - Tex
    - Latex
    - letter
tags:
    - Tex
    - Latex
---

* Linux安装[Texlive](http://tug.org/texlive/)
    * [下载安装包](http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz)，解压，进入解压后目录。
    * 运行 `./install-tl`
    * 根据提示，如果需要修改安装目录，输入大写的`D`，再输入`1`，输入目标目录`~/texlive/2014`，其它的路径也会相应改变。然后按`R`返回主菜单，输入`I`即可开始安装。安装过程会下载挺多文件，大约需要1-3小时。安装出错或中断后可再次运行，会继续之前的安装。
    * 安装完成之后，根据输出提示设置环境变量`PATH`,`MANPATH`,`INFOPATH`，一般可把屏幕上于此相关的三句话拷到`~/.bash_profile`里面(这个文件不存在，则可以新建)。写完之后，`source ~/.bash_profile`。
    * 现在可以在命令行输入`xelatex`开始执行。

* 中文字体解决
    * 拷贝Windows系统的字体(C:\WINDOWS\FONTS)到Linux的`~/.fonts`目录下(目录不存在可以新建)。
        * `cp /media/Win-mount/Windoes/Fonts/{SIM,sim}* ~/fonts` 
    * 在Linux下运行`fc-cache -fsv`(参数可不加)更新系统字体缓存
    * 在Linux下运行`fc-list :lang=zh`查看系统中的中文字体
    * 在Linux-TexLive安装目录下修改`texmf-dist/tex/latex/ctex/fontset/ctex-xecjk-winfonts.def`,尤其注意楷体和仿宋是否和`fc-list`列出的一致。([见附录1])
    * 修改TexLive安装目录下的`texmf.cnf`文件，向其中加入语句`OSFONTDIR = ~/.fonts//;/usr/share/fonts//;/usr/local/share/fonts//`。

* 测试
	* 新建文件`test.tex`包含如下内容，然后运行`xelatex test.tex`。

```
\documentclass{article}
\usepackage{ctex}
\begin{document}
中文测试
\end{document}
```

#### 附录1：

```
% ctex-xecjk-winfonts.def: Windows 的 xeCJK 字体设置，默认为六种中易字体
% vim:ft=tex

\setCJKmainfont[BoldFont={SimHei},ItalicFont={KaiTi}]
  {SimSun}
\setCJKsansfont{SimHei}
\setCJKmonofont{FangSong}

\setCJKfamilyfont{zhsong}{SimSun}
\setCJKfamilyfont{zhhei}{SimHei}
\setCJKfamilyfont{zhkai}{KaiTi}
\setCJKfamilyfont{zhfs}{FangSong}
% \setCJKfamilyfont{zhli}{LiSu}
% \setCJKfamilyfont{zhyou}{YouYuan}

\newcommand*{\songti}{\CJKfamily{zhsong}} % 宋体
\newcommand*{\heiti}{\CJKfamily{zhhei}}   % 黑体
\newcommand*{\kaishu}{\CJKfamily{zhkai}}  % 楷书
\newcommand*{\fangsong}{\CJKfamily{zhfs}} % 仿宋
% \newcommand*{\lishu}{\CJKfamily{zhli}}    % 隶书
% \newcommand*{\youyuan}{\CJKfamily{zhyou}} % 幼圆

\endinput
```
#### 参考

* [Linux-wiki-latex](http://linux-wiki.cn/wiki/LaTeX%E4%B8%AD%E6%96%87%E6%8E%92%E7%89%88%EF%BC%88%E4%BD%BF%E7%94%A8XeTeX%EF%BC%89#cite_note-2)
* [https://code.google.com/p/ctex-kit/wiki/UnixFonts](https://code.google.com/p/ctex-kit/wiki/UnixFonts)
* [http://www.tug.org/texlive/quickinstall.html](http://www.tug.org/texlive/quickinstall.html)
