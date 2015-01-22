---
title: Record of circos usage 
layout: post
categories:
  - circos
  - letter
tags:
  - circos
---

#### Install circos

* Download circos from http://circos.ca/software/download/circos/ and run following command:
```
tar xvzf circos-0.67.tgz
ln -s `pwd`/circos-0.67/bin ~/bin #make sure ~/bin is in $PATH
```

* Install required perl modules
		* Check required perl modules by running `circos -module`.
		* Configure CPANM by typing following commands in `terminal`
```
		wget -O- http://cpanmin.us | perl - -l ~/perl5 App::cpanminus local::lib
		eval `perl -I ~/perl5/lib/perl5 -Mlocal::lib`
		echo 'eval `perl -I ~/perl5/lib/perl5 -Mlocal::lib`' >> ~/.bash_profile
		echo 'export MANPATH=$HOME/perl5/man:$MANPATH' >> ~/.bash_profile
```
		* Install needed modules by typing `cpanm YAML Clone Config::General Font::TTF::Font GD GD::Polyline List::MoreUtils Math::Bezier Math::Round Math::VecStat Params::Validate Readonly Regexp::Common SVG Set::IntSpan Statistics::Basic Text::Format` in `terminal`.
		* Install `libgd` from http://libgd.bitbucket.org if `GD` can not be installed. Make sure `gdlib-config` is $PATH.



