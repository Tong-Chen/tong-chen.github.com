---
layout: page
title: The way to create this blog
comments: yes
---

#### Basic three steps
1. Create a Github repository, names as `USERNAME`.github.com.

2. Clone a constructed jekyll repository
{% highlight bash %}
git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com
{% endhighlight %}

3. Write blogs in _post folder according to Markdown syntax and push to Github.

*Attention: Please be patient, it may take a while for your blog to be accessed.*

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
1. Get a free domain name from [dot.tk](www.dot.tk).

_Forward this domain to USERNAME.github.com may be worked well_

*Remember set the global domain name in _config.xml*

2. Use [DNSpod](https://www.dnspod.cn/) to support domain name parsing.
  * Register at DNSpod and add the applied tk domain name.
  * Use DNSpod supported DNS server like `f1g1ns.dnspod.net.` to set your domain name DNS at [dot.tk](dot.tk).
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
[http://jiyeqian.github.io/](http://jiyeqian.github.io/ "ptential module")
