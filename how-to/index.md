---
layout: page
title: The way to create this blog
comments: yes
---

There are three big steps listed below to construct a jekyll 
blog if I understand right.

* Accompliish the first step, you can write blogs already.
* For me, the second step is only used for testing. A local server 
may also be useful for you to browse blogs when you are off line.
* The third step gives you a setted domain name. 

#### Basic three steps
1. Create a Github repository, names as `USERNAME`.github.com.

2. Clone a constructed jekyll repository.
  * Linux: ```git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com```
  * Windows: Fork the repository [jekyll-bootstrap](https://github.com/plusjade/jekyll-bootstrap/fork) at [github](https://github.com) and clone it to local computer and put it into your local github repository. 

3. Write blogs in _post folder according to Markdown syntax and push to Github.

*Attention: Please be patient, it may take a while (about `10` minutes) for your blog to be accessed.*

Congratulations! You can write things now.

#### Install local server
Here only lists instructions for Windows system since I am not familar with it.

For Unix-like system, it should be very easy.

1. Download portable servers from [Madhur](http://www.madhur.co.in/blog/2013/07/20/buildportablejekyll.html)

*Set environmental variable from My computer->property->Advanced system settings
->Environmental Variables->PATH `for each program`*

2. Open a `cmd` window and set UTF-8 character by running `chcp 65001` to support Chinese characters.

3. Go to the directory contains the Github repository locally and run `jekyll serve` to run local server.

*Local sever may be helpful for debugging you posts.*

#### Get another domain name
1. Get a free domain name from [dot.tk](http://dot.tk).

_Forward this domain to USERNAME.github.com may be worked well_

*Remember set the global domain name in _config.xml*

2. Use [DNSpod](https://www.dnspod.cn/) to support domain name parsing.
  * Register at DNSpod and add the applied tk domain name.
  * Use DNSpod supported DNS server like `f1g1ns.dnspod.net.` to set your domain name DNS at [dot.tk](http://dot.tk).
  ![Set tk DNA server]({{ site.img_url }}/tk-set.png)
  * Manage domain `CNAME` and `A record` at DNApod.
  ![Set DNSpod]({{ site.img_url }}/DNApod-set.png)


#### Refs

[http://jekyllbootstrap.com/usage/jekyll-quick-start.html](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

[http://jekyllrb.com/docs/templates/](http://jekyllrb.com/docs/templates/)

[http://thinkinside.tk/2013/05/27/jekyll_mysite.html](http://thinkinside.tk/2013/05/27/jekyll_mysite.html)

[http://jiyeqian.github.io/2012/07/host-your-pages-at-github-using-jekyll/](http://jiyeqian.github.io/2012/07/host-your-pages-at-github-using-jekyll/)

[http://www.madhur.co.in/blog/2013/07/20/buildportablejekyll.html](http://www.madhur.co.in/blog/2013/07/20/buildportablejekyll.html)

[http://www.mceiba.com/develop/jekyll-introduction.html](http://www.mceiba.com/develop/jekyll-introduction.html)

[http://jiyeqian.github.io/2012/07/host-your-pages-at-github-using-jekyll/](http://jiyeqian.github.io/2012/07/host-your-pages-at-github-using-jekyll/)

[http://realasking.github.io/%E7%BD%91%E7%BB%9C%E5%86%B2%E6%B5%AA/2013/07/15/makeblog2/](http://realasking.github.io/%E7%BD%91%E7%BB%9C%E5%86%B2%E6%B5%AA/2013/07/15/makeblog2/)
