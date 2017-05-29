---
title: Ways to login remote server using ssh without inputting password
author: 悟道
layout: post
categories:
  - linux
  - letter
tags:
  - linux
---

## 最简单的操作

在本地电脑执行 `/usr/bin/ssh-keygen -t rsa`，安装提示一直回车即可，最后会看到`~/.ssh`目录下多了几个文件`id_rsa id_rsa.pub`.

在本地电脑执行 `scp ~/.ssh/id_rsa.pub user@remote_server:`拷贝`~/.ssh/id_rsa.pub`到需要远程登录的服务器的家目录下。

使用密码登录远程服务器，执行`mkdir -p ~/.ssh; cat ~/id_rsa.pub >>~/.ssh/authorized_keys; chmod 700 ~/.ssh; chmod 600 >>~/.ssh/authorized_keys`.

退出，再尝试登录，应该就不需要输入密码了。

## 操作详细解释

### 密钥认证原理：公钥和私钥

原理： 密匙认证需要依靠密匙，首先创建一对密匙（包括公匙和密匙，并且用公匙加密的数据只能用密匙解密），并把公匙放到需要远程服务器上。这样当登录远程服务器时，客户端软件就会向服务器发出请求，请求用你的密匙进行认证。服务器收到请求之后，先在你在该服务器的宿主目录下寻找你的公匙，然后检查该公匙是否是合法，如果合法就用公匙加密一随机数（即所谓的challenge）并发送给客户端软件。客户端软件收到 “challenge”之后就用私匙解密再把它发送给服务器。因为用公匙加密的数据只能用密匙解密，服务器经过比较就可以知道该客户连接的合法性。

### 操作环境和步骤详解

条件：客户机：1.1.1.1 远端主机：2.2.2.2

在客户机执行下述命令产生公钥和私钥,	输入命令后，一直回车就可。执行完成后用户的主目录/.ssh目录下面产生一对密钥。一般采用的ssh的rsa密钥: id_rsa 私钥 id_rsa.pub 公钥。

```bash
[user@localhost .ssh]# /usr/bin/ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/user/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again: Your identification has been saved in /user/.ssh/id_rsa.
Your public key has been saved in /user/.ssh/id_rsa.pub.
The key fingerprint is: 30:f6:d7:2a:ac:56:eb:3f:fa:40:25:8d:90:96:68:cb user@localhost.localdomain
```

也可以获得其它加密类型的密钥

```bash
ssh-keygen -t dsa
ssh-keygen -t rsa1
```

把公钥拷贝到远程服务器的`.ssh/authorized_keys`文件中 (若文件`.ssh/authorized_keys`非空，采用上述方式追加)

```bash
[user@localhost .ssh]# scp /user/.ssh/id_rsa.pub user@2.2.2.2:/user/.ssh/authorized_keys
user@2.2.2.2's password:

```

操作完毕，登陆检查。

```bash
[user@localhost .ssh]# ssh 2.2.2.2
user@2.2.2.2's password:
```
请注意此时如果仍提示输入密码，请检查如下文件夹和文件的操作权限，这是非常重要的， 否则ssh公钥认证体制不能正常工作：


```bash
#1.1.1.1（客户端）
~/.ssh文件夹的权限是700 （好像这个权限关系不是很大）
~/.ssh/id_rsa私钥的权限600
~/.ssh/id_rsa.pub私钥的权限644
 
#2.2.2.2（远端主机）

~/.ssh文件夹的权限是700 
~/authorized_keys公钥的权限600
```
 

```bash
[user@localhost ~]# ssh 2.2.2.2
Last login: Sat Dec 15 21:10:17 2016 from 1.1.1.1
[user@localhost ~]#

```

无密码SSH登陆成功！

 
问题1：Agent admitted failure to sign using the key

解決: 在客户端使用 ssh-add 指令将私钥添加至SSH `ssh-add ~/.ssh/id_rsa`（根据个人的密匙命名不同更改 id_rsa）

## 使用sshpass非交互的ssh密码验证

sshpass是非交互性ssh登录工具，把密码作为参数或存储在配置文件中提供，省去了多次输入密码的麻烦。

sshpass安装：

```
wget 'https://downloads.sourceforge.net/project/sshpass/sshpass/1.06/sshpass-1.06.tar.gz?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fsshpass%2F&ts=1496021628&use_mirror=jaist' -O sshpass-1.06.tar.gz

tar xvzf sshpass-1.06.tar.gz

cd sshpass*
./configure --prefix=/install_path
make
make install
# 加入环境变量
```

```bash
# 登录远程服务器
sshpass -p 'password' ssh user@remote_host  

# execute command from remote server
sshpass -p 'password' ssh user@remote_host 'ls' 

# Remote login multiple servers; -tt should be used when error 
# 'Pseudo-terminal will not be allocated because stdin is not a terminal' appears.
sshpass -p 'password' ssh -tt user@remote_host \
	'source ~/.bashrc; sshpass -p "password" ssh -tt user@another_remote_host "Execute other command"' 

```

## 参考

<http://hi.baidu.com/meloidea/blog/item/63779f222b39faf0d7cae205.html>
<http://sakananote2.blogspot.com/2010/07/agent-admitted-failure-to-sign-using.html>
<http://linuxtoy.org/archives/sshpass.html>
