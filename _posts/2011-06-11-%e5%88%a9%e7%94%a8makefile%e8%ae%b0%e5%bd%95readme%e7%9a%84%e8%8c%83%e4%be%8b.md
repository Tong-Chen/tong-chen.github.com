---
title: 利用Makefile记录README的范例
author: 悟道
layout: post
permalink: /?p=998
categories:
  - C
  - make
tags:
  - C
  - makefile
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

在做课题的过程中，我们需要利用各种脚本处理许多数据。为了方便记录不同结果所使用的不同脚本和参数，数据改变时及时更新相应的结果，并且记录结果文件的描述，这里利用了Makefile来辅助完成这个工作。

Readme-file

> This is the README file.
> 
> In this folder, there are three kind of files,
> 
> Makefile: this is the real README. It contains description of  
> files and command to get that files.
> 
> ._filename: this is the command to get tha file end with &#8216;filename&#8217;.  
> Use &#8216;make ._filename&#8217; to run it.
> 
> filename: this is the result file. If you want to know what this  
> file is and how I get this file, use &#8216;make filename&#8217; to show it.
> 
> So no matter what file it is, just use &#8216;make filename&#8217; to know it.

Makefile文件格式如下：

<div class="wp_codebox">
  <table>
    <tr id="p998108">
      <td class="code" id="p998code108">
        <pre class="make" style="font-family:monospace;">cmd<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span>echo <span style="color: #004400;">**</span>this is the command to get this file<span style="color: #004400;">**;</span>echo
dsp<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span>echo <span style="color: #004400;">**</span>this is the description of this file<span style="color: #004400;">**;</span>echo
&nbsp;
showall<span style="color: #004400;">=</span>for i in `ls <span style="color: #004400;">|</span> grep <span style="color: #004400;">-</span>v <span style="color: #CC2200;">'^_'</span>`<span style="color: #004400;">;</span> do make <span style="color: #000088; font-weight: bold;">$$</span>i<span style="color: #004400;">;</span> done
&nbsp;
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span>
&nbsp;
all<span style="color: #004400;">:$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*.</span>CT<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Finish$${txtrst} all operation at $$(pwd)."</span>
&nbsp;
all_n<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> _n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#91;</span>^<span style="color: #004400;">.</span>CT<span style="color: #004400;">&#93;</span>?<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Ready$${txtrst} for operation at $$(pwd)."</span>
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#ct_test=bash command</span>
<span style="color: #339900; font-style: italic;">#._test:</span>
<span style="color: #339900; font-style: italic;">#	$(ct_test); touch ._test ._test.CT</span>
<span style="color: #339900; font-style: italic;">#._test_n:</span>
<span style="color: #339900; font-style: italic;">#	@-/bin/rm ._test</span>
<span style="color: #339900; font-style: italic;">#result:</span>
<span style="color: #339900; font-style: italic;">#     $(cmd)</span>
<span style="color: #339900; font-style: italic;">#     @echo "$(ct_test)"</span>
<span style="color: #339900; font-style: italic;">#     $(dsp)</span>
<span style="color: #339900; font-style: italic;">#     @echo description information</span>
<span style="color: #339900; font-style: italic;">#showsubdir:</span>
<span style="color: #339900; font-style: italic;">#   cd subdir; $(showall)</span>
<span style="color: #339900; font-style: italic;">#makesubsir:</span>
<span style="color: #339900; font-style: italic;">#   cd subdir; make all</span></pre>
      </td>
    </tr>
  </table>
</div>

第二版Makefile

<div class="wp_codebox">
  <table>
    <tr id="p998109">
      <td class="code" id="p998code109">
        <pre class="make" style="font-family:monospace;">bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
touch<span style="color: #004400;">=</span>touch <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">.</span>CT
nake<span style="color: #004400;">=/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
&nbsp;
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
	<span style="color: #339900; font-style: italic;">#echo `perl -e "print '-' x 60"`;</span>
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
	<span style="color: #339900; font-style: italic;">#echo `perl -e "print '-' x 60"`;</span>
&nbsp;
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span>echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addprefix</span> show_<span style="color: #004400;">,</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to \
	list the <span style="color: #666622; font-weight: bold;">info</span> of each file or <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make \
	<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addprefix</span> <span style="color: #004400;">.</span>_mk_<span style="color: #004400;">,</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> in folder <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">.;</span>\
	echo
&nbsp;
<span style="color: #339900; font-style: italic;">#showall=for i in `ls | grep -v '^_'`; do make -s $$i; done</span>
&nbsp;
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span>
&nbsp;
all<span style="color: #004400;">:$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*.</span>CT<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Finish$${txtrst} all operation at $$(pwd)."</span>
&nbsp;
all<span style="color: #004400;">.</span>n<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#91;</span>^<span style="color: #004400;">.</span>CT<span style="color: #004400;">&#93;</span>?<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Ready$${txtrst} for operation at $$(pwd)."</span>
&nbsp;
all_p<span style="color: #004400;">:$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span>
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#dir:</span>
<span style="color: #339900; font-style: italic;">#	@echo "Dir information"</span>
<span style="color: #339900; font-style: italic;">#	@$(sub)</span>
<span style="color: #339900; font-style: italic;">#show_subdir:</span>
<span style="color: #339900; font-style: italic;">#	@cd subdir; make all_p</span>
<span style="color: #339900; font-style: italic;">#._mk_subdir:</span>
<span style="color: #339900; font-style: italic;">#	@cd subdir; make all</span>
<span style="color: #339900; font-style: italic;">#	@touch ._mk_subdir ._mk_subdir.CT</span>
<span style="color: #339900; font-style: italic;">#Attention: There is no other '.' in the command except the first one or\</span>
	the <span style="color: #004400;">.</span>n nake one<span style="color: #004400;">.</span>
<span style="color: #339900; font-style: italic;">#._test:dependency #(dependency should not be files in current directory)</span>
<span style="color: #339900; font-style: italic;">#	@echo 'test 1'; touch $@ $@.CT</span>
<span style="color: #339900; font-style: italic;">#._test.n:</span>
<span style="color: #339900; font-style: italic;">#	@-/bin/rm $(basename $@)</span>
<span style="color: #339900; font-style: italic;">#file:</span>
<span style="color: #339900; font-style: italic;">#	@$(cmd)</span>
<span style="color: #339900; font-style: italic;">#	@echo "$(ct_test)"</span>
<span style="color: #339900; font-style: italic;">#	@$(dsp)</span>
<span style="color: #339900; font-style: italic;">#	@echo ******************</span></pre>
      </td>
    </tr>
  </table>
</div>

第三版

<div class="wp_codebox">
  <table>
    <tr id="p998110">
      <td class="code" id="p998code110">
        <pre class="make" style="font-family:monospace;">bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
touch<span style="color: #004400;">=</span>touch <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">.</span>CT
nake<span style="color: #004400;">=/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
&nbsp;
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
	<span style="color: #339900; font-style: italic;">#echo `perl -e "print '-' x 60"`;</span>
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
	<span style="color: #339900; font-style: italic;">#echo `perl -e "print '-' x 60"`;</span>
&nbsp;
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span>echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addprefix</span> show_<span style="color: #004400;">,</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to \
	list the <span style="color: #666622; font-weight: bold;">info</span> of each file or <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make \
	<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addprefix</span> <span style="color: #004400;">.</span>_mk_<span style="color: #004400;">,</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> in folder <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">.;</span>\
	echo
&nbsp;
<span style="color: #339900; font-style: italic;">#showall=for i in `ls | grep -v '^_'`; do make -s $$i; done</span>
&nbsp;
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span>
&nbsp;
all<span style="color: #004400;">:$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*.</span>CT<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Finish$${txtrst} all operation at $$(pwd)."</span>
&nbsp;
all<span style="color: #004400;">.</span>n<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#91;</span>^<span style="color: #004400;">.</span>CT<span style="color: #004400;">&#93;</span>?<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Ready$${txtrst} for operation at $$(pwd)."</span>
&nbsp;
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#91;</span>^<span style="color: #004400;">.</span>CT<span style="color: #004400;">&#93;</span>?<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@-$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">nake</span><span style="color: #004400;">&#41;</span>
&nbsp;
all_p<span style="color: #004400;">:$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span>
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span>
&nbsp;
dir<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"Dir information"</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
show_subdir<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cd subdir<span style="color: #004400;">;</span> make all_p
<span style="color: #004400;">.</span>_mk_subdir<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cd subdir<span style="color: #004400;">;</span> make all
	<span style="color: #004400;">@</span>touch <span style="color: #004400;">.</span>_mk_subdir <span style="color: #004400;">.</span>_mk_subdir<span style="color: #004400;">.</span>CT
<span style="color: #339900; font-style: italic;">#Attention: There is no other '.' in the command except the first one or\</span>
	the <span style="color: #004400;">.</span>n nake one<span style="color: #004400;">.</span>
<span style="color: #339900; font-style: italic;">#(dependency should not be files in current directory)</span>
<span style="color: #004400;">.</span>_test<span style="color: #004400;">:</span>dependency
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">'test 1'</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">touch</span><span style="color: #004400;">&#41;</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##._test.n:</span>
<span style="color: #339900; font-style: italic;">##	@-/bin/rm $(basename $@)</span>
file<span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">cmd</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$(ct_test)"</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #004400;">******************</span></pre>
      </td>
    </tr>
  </table>
</div>

第四版

<div class="wp_codebox">
  <table>
    <tr id="p998111">
      <td class="code" id="p998code111">
        <pre class="make" style="font-family:monospace;">bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
touch<span style="color: #004400;">=</span>touch <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">.</span>CT
nake<span style="color: #004400;">=/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #000088; font-weight: bold;">$@</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> 
&nbsp;
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
	<span style="color: #339900; font-style: italic;">#echo `perl -e "print '-' x 60"`;</span>
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
	<span style="color: #339900; font-style: italic;">#echo `perl -e "print '-' x 60"`;</span>
&nbsp;
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span>echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addprefix</span> show_<span style="color: #004400;">,</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to \
	list the <span style="color: #666622; font-weight: bold;">info</span> of each file or <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make \
	<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addprefix</span> <span style="color: #004400;">.</span>_mk_<span style="color: #004400;">,</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> in folder <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">.;</span>\
	echo
&nbsp;
showsubdir<span style="color: #004400;">=</span>cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">subst</span> show_<span style="color: #004400;">,,</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all_p
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">subst</span> show_<span style="color: #004400;">,,</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all
&nbsp;
<span style="color: #339900; font-style: italic;">#showall=for i in `ls | grep -v '^_'`; do make -s $$i; done</span>
&nbsp;
<span style="color: #004400;">.</span>_mkpic<span style="color: #004400;">:</span>
	<span style="color: #004400;">@-</span>mkdir pic<span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">touch</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span>
&nbsp;
all<span style="color: #004400;">:$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*.</span>CT<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Finish$${txtrst} all operation at $$(pwd)."</span>
&nbsp;
all<span style="color: #004400;">.</span>n<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#91;</span>^<span style="color: #004400;">.</span>CT<span style="color: #004400;">&#93;</span>?<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Ready$${txtrst} for operation at $$(pwd)."</span>
&nbsp;
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#91;</span>^<span style="color: #004400;">.</span>CT<span style="color: #004400;">&#93;</span>?<span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@-$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">nake</span><span style="color: #004400;">&#41;</span>
&nbsp;
all_p<span style="color: #004400;">:$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span>
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span>
&nbsp;
pic<span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"All the picturs are avsed here and has a soft link to $(project)/pic"</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
<span style="color: #339900; font-style: italic;">#show_subdir:</span>
<span style="color: #339900; font-style: italic;">#	@$(showsubdir)</span>
<span style="color: #339900; font-style: italic;">#._mk_subdir:</span>
<span style="color: #339900; font-style: italic;">#	@$(mksubdir)</span>
<span style="color: #339900; font-style: italic;">#	$(touch)</span>
<span style="color: #339900; font-style: italic;">##Attention: There is no other '.' in the command except the first one or\</span>
	the <span style="color: #004400;">.</span>n nake one<span style="color: #004400;">.</span>
<span style="color: #339900; font-style: italic;">##dependency should not be files in current directory, which are also after .PHONY</span>
<span style="color: #339900; font-style: italic;">#._test:dependency</span>
<span style="color: #339900; font-style: italic;">#	@echo 'test 1'; $(touch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##._test.n:</span>
<span style="color: #339900; font-style: italic;">##	@-/bin/rm $(basename $@)</span>
<span style="color: #339900; font-style: italic;">#file:</span>
<span style="color: #339900; font-style: italic;">#	@$(cmd)</span>
<span style="color: #339900; font-style: italic;">#	@echo "$(ct_test)"</span>
<span style="color: #339900; font-style: italic;">#	@$(dsp)</span>
<span style="color: #339900; font-style: italic;">#	@echo ******************</span></pre>
      </td>
    </tr>
  </table>
</div>

Readme-file

> This is the README file.
> 
> In this folder, there are three kind of files,
> 
> Makefile: this is the real README. It contains description of  
> files and command to get that files.
> 
> filename: this is the command to get the file &#8216;filename&#8217;.  
> Use &#8216;make filename&#8217; to run it, and use &#8216;show filename&#8217; to show what this  
> file is and how I get this file.

第五版

<div class="wp_codebox">
  <table>
    <tr id="p998112">
      <td class="code" id="p998code112">
        <pre class="make" style="font-family:monospace;"><span style="color: #339900; font-style: italic;">#----------Premeable-------------------</span>
<span style="color: #339900; font-style: italic;">#In .bash_aliasesi or .bash_rc:</span>
<span style="color: #339900; font-style: italic;">#show()</span>
<span style="color: #339900; font-style: italic;">#{</span>
	<span style="color: #339900; font-style: italic;">#for i in $@; do</span>
	<span style="color: #339900; font-style: italic;">#	i=${i/\//} #Used to deal with folder name</span>
	<span style="color: #339900; font-style: italic;">#	make $i.CT</span>
	<span style="color: #339900; font-style: italic;">#done</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
<span style="color: #339900; font-style: italic;">#make filename: run the program</span>
<span style="color: #339900; font-style: italic;">#show filename: display file information</span>
<span style="color: #339900; font-style: italic;">#._filename is the bak</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
&nbsp;
bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
<span style="color: #339900; font-style: italic;">#--------operation-------------------------</span>
<span style="color: #339900; font-style: italic;">#add touch a judgment----------</span>
bak<span style="color: #004400;">:=.</span>CTBAK<span style="color: #004400;">.</span>
touch<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then diff_a<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#40;</span>diff <span style="color: #004400;">-</span>q <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  if test <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>\<span style="color: #339900; font-style: italic;">#diff_a} -ne 0; then\</span>
	  echo <span style="color: #CC2200;">"$@------`date`"</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span>fi<span style="color: #004400;">;</span>\
	  touch <span style="color: #004400;">.</span>_<span style="color: #000088; font-weight: bold;">$@</span>
touchonly<span style="color: #004400;">=</span>touch <span style="color: #004400;">.</span>_<span style="color: #000088; font-weight: bold;">$@</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#nake=if ! test -f $@$(bak); then /bin/mv -f $(basename $@) $(basename $@)$(bak);fi</span>
nake<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#-------this used to descrribe file properities---------------</span>
<span style="color: #339900; font-style: italic;">#####Use @ befoe these two commands############</span>
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span>
&nbsp;
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
&nbsp;
<span style="color: #339900; font-style: italic;">#--------Some usual commands---------------------</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##There maybe some bug about this two all commands for you do not know the sort of executation####</span>
all<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">subst</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">,,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Finish$${txtrst} all operation at $$(pwd)."</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
all<span style="color: #004400;">.</span>n<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Ready$${txtrst} for operation at $$(pwd) and its subdirectory."</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all<span style="color: #004400;">.</span>n<span style="color: #004400;">;</span>\
		<span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">nake</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-----dir related---each sub Makefile should have the following two lines</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##subdir=dir1 dir2 dir3 dir4</span>
<span style="color: #339900; font-style: italic;">##dir1.CT=file description</span>
<span style="color: #339900; font-style: italic;">##dir2.CT=file description</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">MAKE</span><span style="color: #004400;">&#41;</span> all
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span> echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> will rerun the subfolders<span style="color: #004400;">.;</span>echo
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">mksubdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>CT<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#If this command have more than one output, rewrite $(nake) and $(touch)</span>
<span style="color: #339900; font-style: italic;">#file:dependency</span>
<span style="color: #339900; font-style: italic;">#	$(nake)</span>
<span style="color: #339900; font-style: italic;">#	@echo 'test 1';</span>
<span style="color: #339900; font-style: italic;">#	$(touch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##file.n:</span>
<span style="color: #339900; font-style: italic;">##	$(nake)</span>
<span style="color: #339900; font-style: italic;">#file.CT:</span>
<span style="color: #339900; font-style: italic;">#	@$(cmd)</span>
<span style="color: #339900; font-style: italic;">#	@echo "$(ct_test)"</span>
<span style="color: #339900; font-style: italic;">#	@$(dsp)</span>
<span style="color: #339900; font-style: italic;">#	@echo ******************</span></pre>
      </td>
    </tr>
  </table>
</div>

第六版

<div class="wp_codebox">
  <table>
    <tr id="p998113">
      <td class="code" id="p998code113">
        <pre class="make" style="font-family:monospace;"><span style="color: #339900; font-style: italic;">#----------Premeable-------------------</span>
<span style="color: #339900; font-style: italic;">#In .bash_aliasesi or .bash_rc:</span>
<span style="color: #339900; font-style: italic;">#show()</span>
<span style="color: #339900; font-style: italic;">#{</span>
	<span style="color: #339900; font-style: italic;">#for i in $@; do</span>
	<span style="color: #339900; font-style: italic;">#	i=${i/\//} #Used to deal with folder name</span>
	<span style="color: #339900; font-style: italic;">#	make $i.CT</span>
	<span style="color: #339900; font-style: italic;">#done</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
<span style="color: #339900; font-style: italic;">#make filename: run the program</span>
<span style="color: #339900; font-style: italic;">#show filename: display file information</span>
<span style="color: #339900; font-style: italic;">#._filename is the bak</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
&nbsp;
bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
<span style="color: #339900; font-style: italic;">#--------operation-------------------------</span>
<span style="color: #339900; font-style: italic;">#add touch a judgment----------</span>
bak<span style="color: #004400;">:=.</span>CTBAK<span style="color: #004400;">.</span>
touch<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then diff_a<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#40;</span>diff <span style="color: #004400;">-</span>q <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  if test <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>\<span style="color: #339900; font-style: italic;">#diff_a} -ne 0; then\</span>
	  echo <span style="color: #CC2200;">"$@------`date`"</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span>fi<span style="color: #004400;">;</span>\
	  touch <span style="color: #004400;">.</span>_<span style="color: #000088; font-weight: bold;">$@</span>
<span style="color: #339900; font-style: italic;">###The test part is used for nake, when you rerun the program,</span>
<span style="color: #339900; font-style: italic;">##you mv object to object$(bak), it need deleted when</span>
<span style="color: #339900; font-style: italic;">##the second run finished.</span>
touchonly<span style="color: #004400;">=</span>touch <span style="color: #004400;">.</span>_<span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#nake=if ! test -f $@$(bak); then /bin/mv -f $(basename $@) $(basename $@)$(bak);fi</span>
nake<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#-------this used to descrribe file properities---------------</span>
<span style="color: #339900; font-style: italic;">#####Use @ befoe these two commands############</span>
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span>
&nbsp;
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
&nbsp;
<span style="color: #339900; font-style: italic;">#--------Some usual commands---------------------</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##There maybe some bug about this two all commands for you do not know the sort of executation####</span>
all<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">subst</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">,,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Finish$${txtrst} all operation at $$(pwd)."</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
all<span style="color: #004400;">.</span>n<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Ready$${txtrst} for operation at $$(pwd) and its subdirectory."</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all<span style="color: #004400;">.</span>n<span style="color: #004400;">;</span>\
		<span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">nake</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-----dir related---each sub Makefile should have the following two lines</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##subdir=dir1 dir2 dir3 dir4</span>
<span style="color: #339900; font-style: italic;">##dir1.CT=file description</span>
<span style="color: #339900; font-style: italic;">##dir2.CT=file description</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">MAKE</span><span style="color: #004400;">&#41;</span> all
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span> echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> will rerun the subfolders<span style="color: #004400;">.;</span>echo
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">mksubdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>CT<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#If this command have more than one output, rewrite $(nake) and $(touch)</span>
<span style="color: #339900; font-style: italic;">#file:dependency</span>
<span style="color: #339900; font-style: italic;">#	$(nake)</span>
<span style="color: #339900; font-style: italic;">#	@echo 'test 1';</span>
<span style="color: #339900; font-style: italic;">#	$(touch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##file.n:</span>
<span style="color: #339900; font-style: italic;">##	$(nake)</span>
<span style="color: #339900; font-style: italic;">#file.CT:</span>
<span style="color: #339900; font-style: italic;">#	@$(cmd)</span>
<span style="color: #339900; font-style: italic;">#	@echo "$(ct_test)"</span>
<span style="color: #339900; font-style: italic;">#	@$(dsp)</span>
<span style="color: #339900; font-style: italic;">#	@echo ******************</span></pre>
      </td>
    </tr>
  </table>
</div>

第七版

<div class="wp_codebox">
  <table>
    <tr id="p998114">
      <td class="code" id="p998code114">
        <pre class="make" style="font-family:monospace;"><span style="color: #339900; font-style: italic;">#----------Premeable-------------------</span>
<span style="color: #339900; font-style: italic;">#In .bash_aliasesi or .bash_rc:</span>
<span style="color: #339900; font-style: italic;">#show()</span>
<span style="color: #339900; font-style: italic;">#{</span>
	<span style="color: #339900; font-style: italic;">#for i in $@; do</span>
	<span style="color: #339900; font-style: italic;">#	i=${i/\//} #Used to deal with folder name</span>
	<span style="color: #339900; font-style: italic;">#	make $i.CT</span>
	<span style="color: #339900; font-style: italic;">#done</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
<span style="color: #339900; font-style: italic;">#make filename: run the program</span>
<span style="color: #339900; font-style: italic;">#show filename: display file information</span>
<span style="color: #339900; font-style: italic;">#._filename is the bak</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
&nbsp;
bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
<span style="color: #339900; font-style: italic;">#--------operation-------------------------</span>
<span style="color: #339900; font-style: italic;">#add touch a judgment----------</span>
bak<span style="color: #004400;">:=.</span>CTBAK<span style="color: #004400;">.</span>
touch<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then diff_a<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#40;</span>diff <span style="color: #004400;">-</span>q <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  if test <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>\<span style="color: #339900; font-style: italic;">#diff_a} -ne 0; then\</span>
	  echo <span style="color: #CC2200;">"$@------`date`"</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span>fi<span style="color: #004400;">;</span>\
	  touch <span style="color: #004400;">.</span>_<span style="color: #000088; font-weight: bold;">$@</span>
<span style="color: #339900; font-style: italic;">###The test part is used for nake, when you rerun the program, you mv object to object$(bak), it need deleted when the second run finished.</span>
touchonly<span style="color: #004400;">=</span>touch <span style="color: #004400;">.</span>_<span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#nake=if ! test -f $@$(bak); then /bin/mv -f $(basename $@) $(basename $@)$(bak);fi</span>
nake<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#-------this used to descrribe file properities---------------</span>
<span style="color: #339900; font-style: italic;">#####Use @ befoe these two commands############</span>
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span>
&nbsp;
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
&nbsp;
<span style="color: #339900; font-style: italic;">#--------Some usual commands---------------------</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##There maybe some bug about this two all commands for you do not know the sort of executation####</span>
all<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">subst</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">,,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">.</span>_<span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Finish$${txtrst} all operation at $$(pwd)."</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
all<span style="color: #004400;">.</span>n<span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #CC2200;">"$${mkalert}Ready$${txtrst} for operation at $$(pwd) and its subdirectory."</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
naked<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all<span style="color: #004400;">.</span>n<span style="color: #004400;">;</span>\
		<span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">naked</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-----dir related---each sub Makefile should have the following two lines</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##subdir=dir1 dir2 dir3 dir4</span>
<span style="color: #339900; font-style: italic;">##dir1.CT=file description</span>
<span style="color: #339900; font-style: italic;">##dir2.CT=file description</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">MAKE</span><span style="color: #004400;">&#41;</span> all
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span> echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> will rerun the subfolders<span style="color: #004400;">.;</span>echo
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">mksubdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>CT<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#If this command have more than one output, rewrite $(nake) and $(touch)</span>
<span style="color: #339900; font-style: italic;">#file:dependency</span>
<span style="color: #339900; font-style: italic;">#	$(nake)</span>
<span style="color: #339900; font-style: italic;">#	@echo 'test 1';</span>
<span style="color: #339900; font-style: italic;">#	$(touch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##file.n:</span>
<span style="color: #339900; font-style: italic;">##	$(nake)</span>
<span style="color: #339900; font-style: italic;">#file.CT:</span>
<span style="color: #339900; font-style: italic;">#	@$(cmd)</span>
<span style="color: #339900; font-style: italic;">#	@echo "$(ct_test)"</span>
<span style="color: #339900; font-style: italic;">#	@$(dsp)</span>
<span style="color: #339900; font-style: italic;">#	@echo ******************</span></pre>
      </td>
    </tr>
  </table>
</div>

第八版  
1.修正了all的问题，进一步简化，但是需要借助外部命令  
2.修正了readme，并且利用软连接来保持readme的一致性【find . -type d -exec ln -sf ~/server/CT.README {}/ \;】

Readme-file

> This is the README file.
> 
> In this folder, there are three kind of files,
> 
> Makefile: this is the real README. It contains description of  
> files and command to get that files.
> 
> filename: this is the command to get the file &#8216;filename&#8217;.  
> Use &#8216;make filename&#8217; to run it, and use &#8216;show filename&#8217; to show what this  
> file is and how I get this file.
> 
> Use command redoall to redo all.

<div class="wp_codebox">
  <table>
    <tr id="p998115">
      <td class="code" id="p998code115">
        <pre class="make" style="font-family:monospace;"><span style="color: #339900; font-style: italic;">#----------Premeable-------------------</span>
<span style="color: #339900; font-style: italic;">#In .bash_aliases or .bash_rc or anyfile which can be read by .bahsrc finally:</span>
<span style="color: #339900; font-style: italic;">#show()</span>
<span style="color: #339900; font-style: italic;">#{</span>
	<span style="color: #339900; font-style: italic;">#for i in $@; do</span>
	<span style="color: #339900; font-style: italic;">#	i=${i/\//} #Used to deal with folder name</span>
	<span style="color: #339900; font-style: italic;">#	make -s $i.CT</span>
	<span style="color: #339900; font-style: italic;">#done</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#	sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#	echo 'ALL:' `cut -s -d ':' -f 1 Makefile | grep -v '^#' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '\.CT\$' | grep -v '_'` &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#	echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#	make ALL | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
<span style="color: #339900; font-style: italic;">#make filename: run the program</span>
<span style="color: #339900; font-style: italic;">#show filename: display file information</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
&nbsp;
bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
<span style="color: #339900; font-style: italic;">#--------operation-------------------------</span>
<span style="color: #339900; font-style: italic;">#add touch a judgment----------</span>
bak<span style="color: #004400;">:=.</span>CTBAK<span style="color: #004400;">.</span>
<span style="color: #339900; font-style: italic;">##if # exists in a value of a variable, need a slash before.</span>
<span style="color: #339900; font-style: italic;">##If exists directly in command  line no need slash before</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#This command called 'touch' is the old style, I do not change it here to make sure the back compatibility.</span>
touch<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then diff_a<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#40;</span>diff <span style="color: #004400;">-</span>q <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  if test <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>\<span style="color: #339900; font-style: italic;">#diff_a} -ne 0; then\</span>
	  echo <span style="color: #CC2200;">"$@------`date`"</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">###The test part is used for nake, when you rerun the program, you mv object to object$(bak), it need deleted when the second run finished.</span>
touchonly<span style="color: #004400;">=</span>touch <span style="color: #000088; font-weight: bold;">$@</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#The parameter -n for mv means if the bak file exists, then no more bak.</span>
<span style="color: #339900; font-style: italic;">#this is different with command naked, it used directly</span>
nake<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#-------this used to descrribe file properities---------------</span>
<span style="color: #339900; font-style: italic;">#####Use @ befoe these two commands############</span>
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span>
&nbsp;
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
&nbsp;
<span style="color: #339900; font-style: italic;">#--------Some usual commands---------------------</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#naked used for .n command</span>
naked<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all<span style="color: #004400;">.</span>n<span style="color: #004400;">;</span>\
		<span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">naked</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">.</span>CT<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span> <span style="color: #004400;">|</span>\
		sed <span style="color: #CC2200;">"s/'<span style="color: #000099; font-weight: bold;">\(</span>show [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/"</span> <span style="color: #004400;">|</span>\
		sed <span style="color: #CC2200;">"s/redoall/$${mkcmd}redoall$${txtrst}/"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-----dir related---each sub Makefile should have the following two lines</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##subdir=dir1 dir2 dir3 dir4</span>
<span style="color: #339900; font-style: italic;">##dir1.CT=file description</span>
<span style="color: #339900; font-style: italic;">##dir2.CT=file description</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> redoall
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span> echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> will rerun the subfolders<span style="color: #004400;">.;</span>echo
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">mksubdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>CT<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#If this command have more than one output, rewrite $(nake) and $(touch)</span>
<span style="color: #339900; font-style: italic;">#.CT can not exist in any command only if used as the end.</span>
<span style="color: #339900; font-style: italic;">#file:dependency</span>
<span style="color: #339900; font-style: italic;">#	$(nake)</span>
<span style="color: #339900; font-style: italic;">#	@echo 'test 1';</span>
<span style="color: #339900; font-style: italic;">#	$(touch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##file.n:</span>
<span style="color: #339900; font-style: italic;">##	$(nake)</span>
<span style="color: #339900; font-style: italic;">#file.CT:</span>
<span style="color: #339900; font-style: italic;">#	@$(cmd)</span>
<span style="color: #339900; font-style: italic;">#	@echo "$(ct_test)"</span>
<span style="color: #339900; font-style: italic;">#	@$(dsp)</span>
<span style="color: #339900; font-style: italic;">#	@echo ******************</span></pre>
      </td>
    </tr>
  </table>
</div>

第九版  
1.更新redoall。  
2.修改makefile使其可以记录运行日志  
3.修正touchonly来应对make filename.n产生的备份

<div class="wp_codebox">
  <table>
    <tr id="p998116">
      <td class="code" id="p998code116">
        <pre class="make" style="font-family:monospace;"><span style="color: #339900; font-style: italic;">#----------Premeable-------------------</span>
<span style="color: #339900; font-style: italic;">#In .bash_aliases or .bash_rc or anyfile which can be read by .bahsrc finally:</span>
<span style="color: #339900; font-style: italic;">#show()</span>
<span style="color: #339900; font-style: italic;">#{</span>
	<span style="color: #339900; font-style: italic;">#for i in $@; do</span>
	<span style="color: #339900; font-style: italic;">#	i=${i/\//} #Used to deal with folder name</span>
	<span style="color: #339900; font-style: italic;">#	make -s $i.CT</span>
	<span style="color: #339900; font-style: italic;">#done</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#	sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#	echo 'ALL:' `cut -s -d ':' -f 1 Makefile | grep -v '^#' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '\.CT\$' | grep -v '_'` &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#	echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#	make ALL | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#}</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#	echo "The following shows the command that weill be executed and \</span>
<span style="color: #339900; font-style: italic;">#the  order. If it is that you wanted, press ${mkalert}y${txtrst}; \</span>
<span style="color: #339900; font-style: italic;">#else press others."</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#	sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#	cmd=`cut -s -d ':' -f 1 Makefile | grep -v '^#' | grep -v '\.CT' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '_'`</span>
<span style="color: #339900; font-style: italic;">#	echo ${cmd}</span>
<span style="color: #339900; font-style: italic;">#	read choose</span>
<span style="color: #339900; font-style: italic;">#	if test ${choose} == 'y'; then</span>
<span style="color: #339900; font-style: italic;">#		#sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#		echo 'ALL:' ${cmd} &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#		echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#		make ALL 2&gt;&amp;1 | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#	fi</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
<span style="color: #339900; font-style: italic;">#make filename: run the program</span>
<span style="color: #339900; font-style: italic;">#show filename: display file information</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
&nbsp;
bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
<span style="color: #339900; font-style: italic;">#--------operation-------------------------</span>
<span style="color: #339900; font-style: italic;">#add touch a judgment----------</span>
bak<span style="color: #004400;">:=.</span>CTBAK<span style="color: #004400;">.</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#record run log</span>
runlog<span style="color: #004400;">=</span>echo <span style="color: #CC2200;">"`pwd`<span style="color: #000099; font-weight: bold;">\n</span>    $@<span style="color: #000099; font-weight: bold;">\t</span>`date`"</span> <span style="color: #004400;">&</span>gt<span style="color: #004400;">;&</span>gt<span style="color: #004400;">;$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">logfile</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##if # exists in a value of a variable, need a slash before.</span>
<span style="color: #339900; font-style: italic;">##If exists directly in command  line no need slash before</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##This command called 'touch' is the old style, I do not change</span>
<span style="color: #339900; font-style: italic;">##it here to make sure the back compatibility.</span>
touch<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then diff_a<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#40;</span>diff <span style="color: #004400;">-</span>q <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  if test <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>\<span style="color: #339900; font-style: italic;">#diff_a} -ne 0; then\</span>
	  echo <span style="color: #CC2200;">"$@------`date`"</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span>fi<span style="color: #004400;">;$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">###The test part is used for nake, when you rerun the program,</span>
<span style="color: #339900; font-style: italic;">##you mv object to object$(bak), it need deleted when the second</span>
<span style="color: #339900; font-style: italic;">##run finished.</span>
<span style="color: #339900; font-style: italic;">#Modify touchonly to deal with the .n command</span>
touchonly<span style="color: #004400;">=</span>touch <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#The parameter -n for mv means if the bak file exists, then no more bak.</span>
<span style="color: #339900; font-style: italic;">#this is different with command naked, it used directly</span>
nake<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#-------this used to descrribe file properities---------------</span>
<span style="color: #339900; font-style: italic;">#####Use @ befoe these two commands############</span>
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span>
&nbsp;
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
&nbsp;
<span style="color: #339900; font-style: italic;">#--------Some usual commands---------------------</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#naked used for .n command</span>
naked<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all<span style="color: #004400;">.</span>n<span style="color: #004400;">;</span>\
		<span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">naked</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">.</span>CT<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span> <span style="color: #004400;">|</span>\
		sed <span style="color: #CC2200;">"s/'<span style="color: #000099; font-weight: bold;">\(</span>show [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/"</span> <span style="color: #004400;">|</span>\
		sed <span style="color: #CC2200;">"s/redoall/$${mkcmd}redoall$${txtrst}/"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-----dir related---each sub Makefile should have the following two lines</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##subdir=dir1 dir2 dir3 dir4</span>
<span style="color: #339900; font-style: italic;">##dir1.CT=file description</span>
<span style="color: #339900; font-style: italic;">##dir2.CT=file description</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> redoall
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span> echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> will rerun the subfolders<span style="color: #004400;">.;</span>echo
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">mksubdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>CT<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#If this command have more than one output, rewrite $(nake) and $(touch)</span>
<span style="color: #339900; font-style: italic;">#.CT can not exist in any command only if used as the end.</span>
<span style="color: #339900; font-style: italic;">#file:dependency</span>
<span style="color: #339900; font-style: italic;">#	$(nake)</span>
<span style="color: #339900; font-style: italic;">#	@echo 'test 1';</span>
<span style="color: #339900; font-style: italic;">#	$(touch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##file.n:</span>
<span style="color: #339900; font-style: italic;">##	$(nake)</span>
<span style="color: #339900; font-style: italic;">#file.CT:</span>
<span style="color: #339900; font-style: italic;">#	@$(cmd)</span>
<span style="color: #339900; font-style: italic;">#	@echo "$(ct_test)"</span>
<span style="color: #339900; font-style: italic;">#	@$(dsp)</span>
<span style="color: #339900; font-style: italic;">#	@echo ******************</span></pre>
      </td>
    </tr>
  </table>
</div>

第十版  
1.修正了前版命令只能记录什么时间运行得到哪个结果却不能记录参数的问题，为了配合这个记录，并且简化写作，我使用文件名即作为make的命令，又是对应的存储变量。同时将其并入nake命令。在描述时，把这个并入cmd命令。 这样nake和touch亦可并入同一命令，形成naketouch，并把$($@)取出nake。

<div class="wp_codebox">
  <table>
    <tr id="p998117">
      <td class="code" id="p998code117">
        <pre class="make" style="font-family:monospace;"><span style="color: #339900; font-style: italic;">#----------Premeable-------------------</span>
<span style="color: #339900; font-style: italic;">#In .bash_aliases or .bash_rc or anyfile which can be read by .bahsrc finally:</span>
<span style="color: #339900; font-style: italic;">#show()</span>
<span style="color: #339900; font-style: italic;">#{</span>
        <span style="color: #339900; font-style: italic;">#for i in $@; do</span>
        <span style="color: #339900; font-style: italic;">#       i=${i/\//} #Used to deal with folder name</span>
        <span style="color: #339900; font-style: italic;">#       make -s $i.CT</span>
        <span style="color: #339900; font-style: italic;">#done</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#       sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#       echo 'ALL:' `cut -s -d ':' -f 1 Makefile | grep -v '^#' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '\.CT\$' | grep -v '_'` &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#       echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#       make ALL | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#}</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#       echo "The following shows the command that weill be executed and \</span>
<span style="color: #339900; font-style: italic;">#the  order. If it is that you wanted, press ${mkalert}y${txtrst}; \</span>
<span style="color: #339900; font-style: italic;">#else press others."</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#       sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#       echo `cut -s -d ':' -f 1 Makefile`</span>
<span style="color: #339900; font-style: italic;">#       echo</span>
<span style="color: #339900; font-style: italic;">#       cmd=`cut -s -d ':' -f 1 Makefile | grep -v '^#' | grep -v '\.CT' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '_'`</span>
<span style="color: #339900; font-style: italic;">#       echo ${cmd}</span>
<span style="color: #339900; font-style: italic;">#       read choose</span>
<span style="color: #339900; font-style: italic;">#       if test ${choose} == 'y'; then</span>
<span style="color: #339900; font-style: italic;">#               #sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#               echo 'ALL:' ${cmd} &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#               echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#               make ALL 2&gt;&amp;1 | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#       fi</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
<span style="color: #339900; font-style: italic;">#make filename: run the program</span>
<span style="color: #339900; font-style: italic;">#show filename: display file information</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
&nbsp;
bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
<span style="color: #339900; font-style: italic;">#--------operation-------------------------</span>
<span style="color: #339900; font-style: italic;">#add touch a judgment----------</span>
bak<span style="color: #004400;">:=.</span>CTBAK<span style="color: #004400;">.</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#record run log</span>
<span style="color: #339900; font-style: italic;">#new attribute, record run command and parameter, it needs a variable</span>
<span style="color: #339900; font-style: italic;">#which called ALLCMD, and it turns out this strategy is wrong.</span>
<span style="color: #339900; font-style: italic;">#So I use the filename to save the command. Currently I only use it in</span>
<span style="color: #339900; font-style: italic;">#Sativa analysis for they are new, I will update At ASAP.</span>
runlog<span style="color: #004400;">=</span>echo <span style="color: #CC2200;">"`pwd`<span style="color: #000099; font-weight: bold;">\n</span>    $@<span style="color: #000099; font-weight: bold;">\t</span>`date`<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\t</span>$($@)"</span> <span style="color: #004400;">&</span>gt<span style="color: #004400;">;&</span>gt<span style="color: #004400;">;$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">logfile</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##if # exists in a value of a variable, need a slash before.</span>
<span style="color: #339900; font-style: italic;">##If exists directly in command  line no need slash before</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##This command called 'touch' is the old style, I do not change</span>
<span style="color: #339900; font-style: italic;">##it here to make sure the back compatibility.</span>
touch<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then diff_a<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#40;</span>diff <span style="color: #004400;">-</span>q <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
          if test <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>\<span style="color: #339900; font-style: italic;">#diff_a} -ne 0; then\</span>
          echo <span style="color: #CC2200;">"$@------`date`"</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
          <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span>fi<span style="color: #004400;">;$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">###The test part is used for nake, when you rerun the program,</span>
<span style="color: #339900; font-style: italic;">##you mv object to object$(bak), it need deleted when the second</span>
<span style="color: #339900; font-style: italic;">##run finished.</span>
<span style="color: #339900; font-style: italic;">#Modify touchonly to deal with the .n command</span>
touchonly<span style="color: #004400;">=</span>touch <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#The parameter -n for mv means if the bak file exists, then no more bak.</span>
<span style="color: #339900; font-style: italic;">#this is different with command naked, it used directly</span>
<span style="color: #339900; font-style: italic;">#also nake have another important mission which is tun the command.</span>
nake<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi<span style="color: #004400;">;</span> 
&nbsp;
naketouch<span style="color: #004400;">=$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">nake</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">touch</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-------this used to descrribe file properities---------------</span>
<span style="color: #339900; font-style: italic;">#####Use @ befoe these two commands############</span>
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
        echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
        <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span>\
        echo <span style="color: #CC2200;">"$($(basename $@))"</span>
&nbsp;
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
        echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
        <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
&nbsp;
<span style="color: #339900; font-style: italic;">#--------Some usual commands---------------------</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#naked used for .n command</span>
naked<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span>   bak<span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
        if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all<span style="color: #004400;">.</span>n<span style="color: #004400;">;</span>\
                <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">naked</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">.</span>CT<span style="color: #004400;">:</span>
        <span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span> <span style="color: #004400;">|</span>\
                sed <span style="color: #CC2200;">"s/'<span style="color: #000099; font-weight: bold;">\(</span>show [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/"</span> <span style="color: #004400;">|</span>\
                sed <span style="color: #CC2200;">"s/redoall/$${mkcmd}redoall$${txtrst}/"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-----dir related---each sub Makefile should have the following two lines</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##subdir=dir1 dir2 dir3 dir4</span>
<span style="color: #339900; font-style: italic;">##dir1.CT=file description</span>
<span style="color: #339900; font-style: italic;">##dir2.CT=file description</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> redoall
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span> echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> will rerun the subfold   ers<span style="color: #004400;">.;</span>echo
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
        <span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">mksubdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>CT<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
        <span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
        <span style="color: #004400;">@</span>echo <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
        <span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#If this command have more than one output, rewrite $(nake) and $(touch)</span>
<span style="color: #339900; font-style: italic;">#.CT can not exist in any command only if used as the end.</span>
<span style="color: #339900; font-style: italic;">#file=echo 'test $@'</span>
<span style="color: #339900; font-style: italic;">#file:dependency</span>
<span style="color: #339900; font-style: italic;">#       $(nake)</span>
<span style="color: #339900; font-style: italic;">#       $(touch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##file.n:</span>
<span style="color: #339900; font-style: italic;">##      $(naked)</span>
<span style="color: #339900; font-style: italic;">#file.CT:</span>
<span style="color: #339900; font-style: italic;">#       @$(cmd)</span>
<span style="color: #339900; font-style: italic;">#       @$(dsp)</span>
<span style="color: #339900; font-style: italic;">#       @echo ******************</span></pre>
      </td>
    </tr>
  </table>
</div>

第十一版  
1.第十版极其严重的问题是touchonly的$(bak) $(runlog)之间忘记了添加分号，可能会造成文件的误删。但鉴于runlog的开头文件不在当前目录下，故只会提示错误。不过这个失误可能会引起严重后果。

<div class="wp_codebox">
  <table>
    <tr id="p998118">
      <td class="code" id="p998code118">
        <pre class="make" style="font-family:monospace;"><span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#1.Patch nake and naked. When bak file exists, it will not rewrite it.</span>
<span style="color: #339900; font-style: italic;">#So original file still exists. It will affect rerunning. So I add a rm</span>
<span style="color: #339900; font-style: italic;">#to fix this.(2011-08-22)</span>
<span style="color: #339900; font-style: italic;">#2. touchonly leaks a ';' before $(runlog). It may cause serious erros.</span>
<span style="color: #339900; font-style: italic;">#(2011-08-22)</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#----------Premeable-------------------</span>
<span style="color: #339900; font-style: italic;">#In .bash_aliases or .bash_rc or anyfile which can be read by .bahsrc finally:</span>
<span style="color: #339900; font-style: italic;">#show()</span>
<span style="color: #339900; font-style: italic;">#{</span>
	<span style="color: #339900; font-style: italic;">#for i in $@; do</span>
	<span style="color: #339900; font-style: italic;">#	i=${i/\//} #Used to deal with folder name</span>
	<span style="color: #339900; font-style: italic;">#	make -s $i.CT</span>
	<span style="color: #339900; font-style: italic;">#done</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#	sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#	echo 'ALL:' `cut -s -d ':' -f 1 Makefile | grep -v '^#' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '\.CT\$' | grep -v '_'` &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#	echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#	make ALL | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#}</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#	echo "The following shows the command that weill be executed and \</span>
<span style="color: #339900; font-style: italic;">#the  order. If it is that you wanted, press ${mkalert}y${txtrst}; \</span>
<span style="color: #339900; font-style: italic;">#else press others."</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#	sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#	echo `cut -s -d ':' -f 1 Makefile`</span>
<span style="color: #339900; font-style: italic;">#	echo</span>
<span style="color: #339900; font-style: italic;">#	cmd=`cut -s -d ':' -f 1 Makefile | grep -v '^#' | grep -v '\.CT' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '_'`</span>
<span style="color: #339900; font-style: italic;">#	echo ${cmd}</span>
<span style="color: #339900; font-style: italic;">#	read choose</span>
<span style="color: #339900; font-style: italic;">#	if test ${choose} == 'y'; then</span>
<span style="color: #339900; font-style: italic;">#		#sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#		echo 'ALL:' ${cmd} &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#		echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#		make ALL 2&gt;&amp;1 | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#	fi</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
<span style="color: #339900; font-style: italic;">#make filename: run the program</span>
<span style="color: #339900; font-style: italic;">#show filename: display file information</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
&nbsp;
bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
<span style="color: #339900; font-style: italic;">#--------operation-------------------------</span>
<span style="color: #339900; font-style: italic;">#add touch a judgment----------</span>
bak<span style="color: #004400;">:=.</span>CTBAK<span style="color: #004400;">.</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#record run log</span>
<span style="color: #339900; font-style: italic;">#new attribute, record run command and parameter, it needs a variable</span>
<span style="color: #339900; font-style: italic;">#which called ALLCMD, and it turns out this strategy is wrong.</span>
<span style="color: #339900; font-style: italic;">#So I use the filename to save the command. Currently I only use it in</span>
<span style="color: #339900; font-style: italic;">#Sativa analysis for they are new, I will update At ASAP.</span>
runlog<span style="color: #004400;">=</span>echo <span style="color: #CC2200;">"`pwd`<span style="color: #000099; font-weight: bold;">\n</span>    $@<span style="color: #000099; font-weight: bold;">\t</span>`date`<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\t</span>$($@)"</span> <span style="color: #004400;">&</span>gt<span style="color: #004400;">;&</span>gt<span style="color: #004400;">;$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">logfile</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##if # exists in a value of a variable, need a slash before.</span>
<span style="color: #339900; font-style: italic;">##If exists directly in command  line no need slash before</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##This command called 'touch' is the old style, I do not change</span>
<span style="color: #339900; font-style: italic;">##it here to make sure the back compatibility.</span>
touch<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then diff_a<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#40;</span>diff <span style="color: #004400;">-</span>q <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  if test <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>\<span style="color: #339900; font-style: italic;">#diff_a} -ne 0; then\</span>
	  echo <span style="color: #CC2200;">"$@------`date`"</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">errorlog</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
	  <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span>fi<span style="color: #004400;">;$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">###The test part is used for nake, when you rerun the program,</span>
<span style="color: #339900; font-style: italic;">##you mv object to object$(bak), it need deleted when the second</span>
<span style="color: #339900; font-style: italic;">##run finished.</span>
<span style="color: #339900; font-style: italic;">#Modify touchonly to deal with the .n command</span>
touchonly<span style="color: #004400;">=</span>touch <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#The parameter -n for mv means if the bak file exists, then no more bak.</span>
<span style="color: #339900; font-style: italic;">#this is different with command naked, it used directly</span>
<span style="color: #339900; font-style: italic;">#also nake have another important mission which is tun the command.</span>
nake<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#combine nake and touch</span>
naketouch<span style="color: #004400;">=$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">nake</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">touch</span><span style="color: #004400;">&#41;</span>
<span style="color: #339900; font-style: italic;">#-------this used to descrribe file properities---------------</span>
<span style="color: #339900; font-style: italic;">#####Use @ befoe these two commands############</span>
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span>\
	echo <span style="color: #CC2200;">"$($(basename $@))"</span>
&nbsp;
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
	echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
	<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo
&nbsp;
<span style="color: #339900; font-style: italic;">#--------Some usual commands---------------------</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#naked used for .n command</span>
naked<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then cd <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> make all<span style="color: #004400;">.</span>n<span style="color: #004400;">;</span>\
		<span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">naked</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">.</span>CT<span style="color: #004400;">:</span>
	<span style="color: #004400;">@</span>cat <span style="color: #004400;">./</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span> <span style="color: #004400;">|</span>\
		sed <span style="color: #CC2200;">"s/'<span style="color: #000099; font-weight: bold;">\(</span>show [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/"</span> <span style="color: #004400;">|</span>\
		sed <span style="color: #CC2200;">"s/redoall/$${mkcmd}redoall$${txtrst}/"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-----dir related---each sub Makefile should have the following two lines</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##subdir=dir1 dir2 dir3 dir4</span>
<span style="color: #339900; font-style: italic;">##dir1.CT=file description</span>
<span style="color: #339900; font-style: italic;">##dir2.CT=file description</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> redoall
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span> echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> will rerun the subfolders<span style="color: #004400;">.;</span>echo
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">mksubdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>CT<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@</span>echo <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
	<span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#If this command have more than one output, rewrite $(nake) and $(touch)</span>
<span style="color: #339900; font-style: italic;">#.CT can not exist in any command only if used as the end.</span>
<span style="color: #339900; font-style: italic;">#file=echo 'test $@'</span>
<span style="color: #339900; font-style: italic;">#file:dependency</span>
<span style="color: #339900; font-style: italic;">#	$(naketouch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##file.n:</span>
<span style="color: #339900; font-style: italic;">##	$(naked)</span>
<span style="color: #339900; font-style: italic;">#file.CT:</span>
<span style="color: #339900; font-style: italic;">#	@$(cmd)</span>
<span style="color: #339900; font-style: italic;">#	@$(dsp)</span>
<span style="color: #339900; font-style: italic;">#	@echo ******************</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#Extra command</span>
uniqc<span style="color: #004400;">=</span>uniq <span style="color: #004400;">-</span>c <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">'s/^ *//g'</span> <span style="color: #004400;">|</span> awk <span style="color: #CC2200;">'{ss=$$1;$$1=$$2;$$2=ss; print $$0}'</span></pre>
      </td>
    </tr>
  </table>
</div>

最终版  
1.处理目录时依然有问题，但因为没用上，故没修改。  
2.增加了一键式备份makefile  
3.增加.DELETE\_ON\_ERROR，在运行make非正常退出时删掉靶文件，以便下次运行。  
4.在行首增加SHELL=/bin/bash -e -o pipefail， 捕获管道错误

<div class="wp_codebox">
  <table>
    <tr id="p998119">
      <td class="code" id="p998code119">
        <pre class="make" style="font-family:monospace;"><span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#1. Patch nake and naked. When bak file exists, it will not rewrite it.</span>
<span style="color: #339900; font-style: italic;">#So original file still exists. It will affect rerunning. So I add a rm</span>
<span style="color: #339900; font-style: italic;">#to fix this.(2011-08-22)</span>
<span style="color: #339900; font-style: italic;">#2. touchonly leaks a ';' before $(runlog). It may cause serious erros.</span>
<span style="color: #339900; font-style: italic;">#(2011-08-22)</span>
<span style="color: #339900; font-style: italic;">#3. cmd. Before I can not add $@ in its related command for it will impact</span>
<span style="color: #339900; font-style: italic;">#the output of 'show', now I add a filter mechanism to deal with it.</span>
<span style="color: #339900; font-style: italic;">#(2011-08-29)</span>
<span style="color: #339900; font-style: italic;">#4. set the variable SHELL with /bin/bash to change the default shell</span>
<span style="color: #339900; font-style: italic;">#environment.(2011-09-05)</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#----------Premeable-------------------</span>
<span style="color: #339900; font-style: italic;">#In .bash_aliases or .bash_rc or anyfile which can be read by .bahsrc finally:</span>
<span style="color: #339900; font-style: italic;">#show()</span>
<span style="color: #339900; font-style: italic;">#{</span>
        <span style="color: #339900; font-style: italic;">#for i in $@; do</span>
        <span style="color: #339900; font-style: italic;">#       i=${i/\//} #Used to deal with folder name</span>
        <span style="color: #339900; font-style: italic;">#       make -s $i.CT</span>
        <span style="color: #339900; font-style: italic;">#done</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#       sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#       echo 'ALL:' `cut -s -d ':' -f 1 Makefile | grep -v '^#' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '\.CT\$' | grep -v '_'` &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#       echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#       make ALL | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#}</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#redoall()</span>
<span style="color: #339900; font-style: italic;">#{</span>
<span style="color: #339900; font-style: italic;">#       echo "The following shows the command that weill be executed and \</span>
<span style="color: #339900; font-style: italic;">#the  order. If it is that you wanted, press ${mkalert}y${txtrst}; \</span>
<span style="color: #339900; font-style: italic;">#else press others."</span>
<span style="color: #339900; font-style: italic;">#</span>
<span style="color: #339900; font-style: italic;">#       sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#       echo `cut -s -d ':' -f 1 Makefile`</span>
<span style="color: #339900; font-style: italic;">#       echo</span>
<span style="color: #339900; font-style: italic;">#       cmd=`cut -s -d ':' -f 1 Makefile | grep -v '^#' | grep -v '\.CT' | \</span>
<span style="color: #339900; font-style: italic;">#grep -v '_'`</span>
<span style="color: #339900; font-style: italic;">#       echo ${cmd}</span>
<span style="color: #339900; font-style: italic;">#       read choose</span>
<span style="color: #339900; font-style: italic;">#       if test ${choose} == 'y'; then</span>
<span style="color: #339900; font-style: italic;">#               #sed -i '/^ALL/d' Makefile</span>
<span style="color: #339900; font-style: italic;">#               echo 'ALL:' ${cmd} &gt;&gt;Makefile</span>
<span style="color: #339900; font-style: italic;">#               echo "-----redoall-----`date`-------" &gt;&gt;all.log</span>
<span style="color: #339900; font-style: italic;">#               make ALL 2&gt;&amp;1 | tee -a all.log</span>
<span style="color: #339900; font-style: italic;">#       fi</span>
<span style="color: #339900; font-style: italic;">#}</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
<span style="color: #339900; font-style: italic;">#make filename: run the program</span>
<span style="color: #339900; font-style: italic;">#show filename: display file information</span>
<span style="color: #339900; font-style: italic;">#--------new rules-----2011-06-30------------------</span>
SHELL<span style="color: #004400;">=/</span>bin<span style="color: #004400;">/</span>bash <span style="color: #004400;">-</span>e <span style="color: #004400;">-</span>o pipefail
bin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>
cbin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>cbin<span style="color: #004400;">/</span>
pybin<span style="color: #004400;">=</span>~<span style="color: #004400;">/</span>server<span style="color: #004400;">/</span>pybin<span style="color: #004400;">/</span>
<span style="color: #339900; font-style: italic;">#--------operation-------------------------</span>
<span style="color: #339900; font-style: italic;">#add touch a judgment----------</span>
bak<span style="color: #004400;">:=.</span>CTBAK<span style="color: #004400;">.</span>
<span style="color: #339900; font-style: italic;">#add 2011-09-05-----------</span>
<span style="color: #339900; font-style: italic;">#record run log</span>
<span style="color: #339900; font-style: italic;">#new attribute, record run command and parameter, it needs a variable</span>
<span style="color: #339900; font-style: italic;">#which called ALLCMD, and it turns out this strategy is wrong.</span>
<span style="color: #339900; font-style: italic;">#So I use the filename to save the command. Currently I only use it in</span>
<span style="color: #339900; font-style: italic;">#Sativa analysis for they are new, I will update At ASAP.</span>
runlog<span style="color: #004400;">=</span>echo <span style="color: #CC2200;">"`pwd`<span style="color: #000099; font-weight: bold;">\n</span>    $@<span style="color: #000099; font-weight: bold;">\t</span>`date`<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\t</span>$($@)"</span> <span style="color: #004400;">&</span>gt<span style="color: #004400;">;&</span>gt<span style="color: #004400;">;</span>makerun<span style="color: #004400;">.</span>log
&nbsp;
<span style="color: #339900; font-style: italic;">##if # exists in a value of a variable, need a slash before.</span>
<span style="color: #339900; font-style: italic;">##If exists directly in command  line no need slash before</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##This command called 'touch' is the old style, I do not change</span>
<span style="color: #339900; font-style: italic;">##it here to make sure the back compatibility.</span>
touch<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>e <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then diff_a<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#40;</span>diff <span style="color: #004400;">-</span>q <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
          if test <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>\<span style="color: #339900; font-style: italic;">#diff_a} -ne 0; then\</span>
          echo <span style="color: #CC2200;">"$@------`date`"</span> <span style="color: #004400;">|</span> tee <span style="color: #004400;">-</span>a makeerror<span style="color: #004400;">.</span>log<span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>\
          <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span>fi<span style="color: #004400;">;$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">###The test part is used for nake, when you rerun the program,</span>
<span style="color: #339900; font-style: italic;">##you mv object to object$(bak), it need deleted when the second</span>
<span style="color: #339900; font-style: italic;">##run finished.</span>
<span style="color: #339900; font-style: italic;">#Modify touchonly to deal with the .n command</span>
touchonly<span style="color: #004400;">=</span>touch <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#The parameter -n for mv means if the bak file exists, then no more bak.</span>
<span style="color: #339900; font-style: italic;">#this is different with command naked, it used directly</span>
<span style="color: #339900; font-style: italic;">#also nake have another important mission which is tun the command.</span>
nake<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>e <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #000088; font-weight: bold;">$@</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span>fi
&nbsp;
<span style="color: #339900; font-style: italic;">#combine nake and touch</span>
naketouch<span style="color: #004400;">=$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">nake</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">touch</span><span style="color: #004400;">&#41;</span>
touchd<span style="color: #004400;">=$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">runlog</span><span style="color: #004400;">&#41;</span>
<span style="color: #339900; font-style: italic;">#-------this used to descrribe file properities---------------</span>
<span style="color: #339900; font-style: italic;">#####Use @ befoe these two commands############</span>
cmd<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
        echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>command<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> to get \
        <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span>\
        echo <span style="color: #CC2200;">"$($(basename $@))"</span> <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">'s/<span style="color: #000099; font-weight: bold;">\.</span>CT//g'</span>
&nbsp;
dsp<span style="color: #004400;">=</span>echo `perl <span style="color: #004400;">-</span>e <span style="color: #CC2200;">"print '-' x 60"</span>`<span style="color: #004400;">;</span>\
        echo This is the <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkemph<span style="color: #004400;">&#125;</span>description<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> of \
        <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkfile<span style="color: #004400;">&#125;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">---;</span>echo<span style="color: #004400;">;</span> \
        echo <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkalert<span style="color: #004400;">&#125;</span>Here lists parts of the files<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span><span style="color: #004400;">;</span> echo<span style="color: #004400;">;</span>\
        if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then ls <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #666622; font-weight: bold;">else</span> \
        head <span style="color: #004400;">-</span>n <span style="color: #CC2200;">10</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi<span style="color: #004400;">;</span> echo
&nbsp;
<span style="color: #339900; font-style: italic;">#--------Some usual commands---------------------</span>
lineno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`cat <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">|</span> wc <span style="color: #004400;">-</span>l`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
gtno<span style="color: #004400;">=</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mknum<span style="color: #004400;">&#125;</span>`grep <span style="color: #004400;">-</span>c <span style="color: #CC2200;">'&gt;'</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>`<span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#naked used for .n command</span>
naked<span style="color: #004400;">=</span>if test <span style="color: #004400;">-</span>e <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>mv <span style="color: #004400;">-</span>n <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">bak</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> <span style="color: #004400;">/</span>bin<span style="color: #004400;">/</span>rm <span style="color: #004400;">-</span>f <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span>fi
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>n<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">wildcard</span> <span style="color: #004400;">*</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
        if test <span style="color: #004400;">-</span>d <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> then echo <span style="color: #CC2200;">"Nothing to do with directory, danger"</span><span style="color: #004400;">;</span>\
                <span style="color: #666622; font-weight: bold;">else</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">naked</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">;</span> fi
&nbsp;
<span style="color: #339900; font-style: italic;">#$(addsuffix .n, $(wildcard *)):</span>
<span style="color: #339900; font-style: italic;">#       if test -d $(basename $@); then cd $(basename $@); make all.n;\</span>
<span style="color: #339900; font-style: italic;">#               else $(naked); fi</span>
&nbsp;
CT<span style="color: #004400;">.</span>README<span style="color: #004400;">.</span>CT<span style="color: #004400;">:</span>
        <span style="color: #004400;">@</span>cat ~<span style="color: #004400;">/</span>server<span style="color: #004400;">//</span>CT<span style="color: #004400;">.</span>README <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">"s/<span style="color: #000099; font-weight: bold;">\(</span>make [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/g"</span> <span style="color: #004400;">|</span>\
                sed <span style="color: #CC2200;">"s/'<span style="color: #000099; font-weight: bold;">\(</span>show [^']*<span style="color: #000099; font-weight: bold;">\)</span>/$${mkcmd}<span style="color: #000099; font-weight: bold;">\1</span>$${txtrst}/"</span> <span style="color: #004400;">|</span>\
                sed <span style="color: #CC2200;">"s/redoall/$${mkcmd}redoall$${txtrst}/"</span>
&nbsp;
<span style="color: #339900; font-style: italic;">#-----dir related---each sub Makefile should have the following two lines</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">##subdir=dir1 dir2 dir3 dir4</span>
<span style="color: #339900; font-style: italic;">##dir1.CT=file description</span>
<span style="color: #339900; font-style: italic;">##dir2.CT=file description</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
mksubdir<span style="color: #004400;">=</span>cd <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">;</span> redoall
sub<span style="color: #004400;">=</span>echo<span style="color: #004400;">;</span> echo Use <span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>mkcmd<span style="color: #004400;">&#125;</span>make <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">basename</span> <span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span><span style="color: #000088; font-weight: bold;">$$</span><span style="color: #004400;">&#123;</span>txtrst<span style="color: #004400;">&#125;</span> will rerun the subfolders<span style="color: #004400;">.;</span>echo
<span style="color: #990000;">.PHONY</span><span style="color: #004400;">:</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
        <span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">mksubdir</span><span style="color: #004400;">&#41;</span>
<span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #0000CC; font-weight: bold;">addsuffix</span> <span style="color: #004400;">.</span>CT<span style="color: #004400;">,</span> <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">subdir</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">&#41;</span><span style="color: #004400;">:</span>
        <span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">dsp</span><span style="color: #004400;">&#41;</span>
        <span style="color: #004400;">@</span>echo <span style="color: #004400;">$</span><span style="color: #004400;">&#40;</span><span style="color: #000088; font-weight: bold;">$@</span><span style="color: #004400;">&#41;</span>
        <span style="color: #004400;">@$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">sub</span><span style="color: #004400;">&#41;</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##########################################################</span>
<span style="color: #339900; font-style: italic;">#If this command have more than one output, rewrite $(nake) and $(touch)</span>
<span style="color: #339900; font-style: italic;">#.CT can not exist in any command only if used as the end.</span>
<span style="color: #339900; font-style: italic;">#file=echo 'test $@'</span>
<span style="color: #339900; font-style: italic;">#file:dependency</span>
<span style="color: #339900; font-style: italic;">#       $(naketouch)</span>
<span style="color: #339900; font-style: italic;">##This two lines not needed, but this command still can be used</span>
<span style="color: #339900; font-style: italic;">##file.n:</span>
<span style="color: #339900; font-style: italic;">##      $(naked)</span>
<span style="color: #339900; font-style: italic;">#file.CT:</span>
<span style="color: #339900; font-style: italic;">#       @$(cmd)</span>
<span style="color: #339900; font-style: italic;">#       @$(dsp)</span>
<span style="color: #339900; font-style: italic;">#       @echo ******************</span>
<span style="color: #339900; font-style: italic;">##########################################################</span>
&nbsp;
<span style="color: #339900; font-style: italic;">##New function added#######</span>
makefile<span style="color: #004400;">:</span>
        tar <span style="color: #004400;">-</span>czf makefile<span style="color: #004400;">.</span>tar<span style="color: #004400;">.</span>gz `find <span style="color: #004400;">.</span> <span style="color: #004400;">-</span>name <span style="color: #CC2200;">'Makefile'</span>`
<span style="color: #339900; font-style: italic;">##New function added#######</span>
<span style="color: #990000;">.DELETE_ON_ERROR</span><span style="color: #004400;">:</span>
  
<span style="color: #339900; font-style: italic;">#Extra command</span>
uniqc<span style="color: #004400;">=</span>uniq <span style="color: #004400;">-</span>c <span style="color: #004400;">|</span> sed <span style="color: #CC2200;">'s/^ *//g'</span> <span style="color: #004400;">|</span> awk <span style="color: #CC2200;">'{ss=$$1;$$1=$$2;$$2=ss; print $$0}'</span>
<span style="color: #339900; font-style: italic;">#--------another thing-----------------</span>
keg<span style="color: #004400;">=$</span><span style="color: #004400;">&#40;</span><span style="color: #000088;">ls</span> <span style="color: #004400;">|</span> grep <span style="color: #CC2200;">'keg$$'</span><span style="color: #004400;">&#41;</span>
<span style="color: #339900; font-style: italic;">#--------another thing-----------------</span></pre>
      </td>
    </tr>
  </table>
</div>

<div class="wp_codebox">
  <table>
    <tr id="p998120">
      <td class="code" id="p998code120">
        <pre class="make" style="font-family:monospace;">&nbsp;</pre>
      </td>
    </tr>
  </table>
</div>