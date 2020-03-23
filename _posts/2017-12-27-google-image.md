---
title: 谷歌和SCI-HUB镜像, SSH隧道访问内网
author: ct
layout: post
categories:
  - Bioinfo
tags:
  - Bioinfo
---

搜索一直是个难题，不管是学术，还是解决日程程序遇到的问题。马无夜草不肥，人不搜索作废。生信宝典推出过三篇搜索系列文章

* [基于人工智能的文献检索，导师查找，更聪明](http://mp.weixin.qq.com/s/ikU0mVyX6BQNgljD1jCrRA)
* [GeenMedical：文献查询、筛选、引用排序、相似文献、全文下载、杂志分区、影响因子、结果导出、杂志评述、直
接投稿，一站服务 (现在也支持**SCI-hub镜像自动选择**了)](http://mp.weixin.qq.com/s/hc8g64aHN7qv8YhVfrsuvQ)
* [YANDEX搜索，不翻墙稳定使用近谷歌搜索](http://mp.weixin.qq.com/s/fZ2Nm7Wck5mZLiESHcPusA)

今天再分享一些稳定的谷歌镜像、SCI-hub镜像和全渠道搜索工具，也算做个记录，省得每次都去查。

### yaguge 呀谷歌

<https://yaguge.com/>

全网真正24小时可用的谷歌镜像导航，每隔5分钟自动严格检测镜像池里所有镜像的可用性，并提取打开速度最快的前5个给大家，所有镜像均可正常打开、正常搜索、无验证码。

![](www.ehbio.com/ehbio_resource/yaguge.png)

### SCMOR全渠道搜素

<http://dir.scmor.com/>自带两个谷歌镜像，还有谷歌镜像导航网站<http://ac.scmor.com/>。

![](www.ehbio.com/ehbio_resource/scmor.png)

### dirmor.top

<http://www.dirmor.top/>也是一组镜像网站，留作备用。不是所有的链接都会好使，但应急还是可以的。

![](http://www.dirmor.top/)

### 如果你有服务器

如果你有国外服务器的账户，可以使用`SSH tunnel`，不只可以享受外网，还能对信息加密，使用更安全。如果你单位有服务器，又有权限下载文章，那么不在单位时也可以使用`SSH Tunnel`，潜入单位**下载文献或者访问内网**。


以`XShell`和火狐的插件`FoxyProxy`为例，其它工具类似。

1. 在XShell设置中，SSH的Tunnel (隧道)选项中，选择Dynamic项, 自定义一个Source port(12345)。

   ![](www.ehbio.com/ehbio_resource/xshell_tunnel.png)

2. 连接到服务器，输入用户名和密码，此时就在本地和服务器之间建立了一个SSH隧道，使用SOCKS代理。

3. 在Firefox的插件FoxyProxy中，按如下操作添加SOCKS代理，IP设为127.0.0.1，端口号设为刚才在XShell中设置的端口号(12345)。

   ![](www.ehbio.com/ehbio_resource/Foxyproxy_addserver.png)

4. 如果我们只想对**部分URL**使用这个代理，或想根据不同的URL选择**不同的代理**，可以给每个代理设置支持的URL模式。

   ![](www.ehbio.com/ehbio_resource/FoxyProxy_pattern.png)

5. 这样通过Firefox发出的符合特定模式的网页请求都通过主机与服务器之间的SSH隧道传输，相当于使用远程服务器的网络，比如访问内网，利用研究所的数据库下载文献，利用研究所的VPN访问外网等。

6. 需要注意两点

   * 先建立好SSH连接，代理才可以使用。
   * 多次SSH登陆服务器，系统会自动判断是否有SSH通道存在，若有则不再建立。这时就会发生一种情况，Xshell连接完好，但代理不能用，可能是因为有代理通道的连接被关掉了，需要再建立一次SSH连接。








#### 生信宝典，一起学生信

[http://mp.weixin.qq.com/s/i71OMaUu6QtcY0pt1njHQA](http://mp.weixin.qq.com/s/i71OMaUu6QtcY0pt1njHQA)

#### 生信宝典，生物信息学习系列教程，转录组，宏基因组，外显子组，R作图，Python学习，Cytoscape视频教程

[http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg](http://mp.weixin.qq.com/s/d1KCETQZ88yaOLGwAtpWYg)

#### 生信宝典，最好的生物信息培训课程，培训课程资料

[www.ehbio.com/Training](www.ehbio.com/Training)

