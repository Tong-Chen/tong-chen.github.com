---
title: 配置ftp用户上传到特定目录
author: ct
layout: post
categories:
  - Docker
tags:
  - Docker
---

在Centos 6.6环境使用系统自带的internal-sftp搭建SFTP服务器。


### 查看openssh的版本   

使用`ssh -V`命令来查看openssh的版本，版本必须大于4.8p1，低于的这个版本需要升级。

### 创建sftp组

```bash
groupadd sftp
```

### 创建一个sftp用户，用户名为mysftp，密码为mysftp

```bash
useradd -g sftp -s /bin/false mysftp  //用户名
passwd mysftp  //密码
```

### sftp组的用户的home目录统一指定到/data/sftp下，按用户名区分，这里先新建一个mysftp目录，然后指定mysftp的home为/data/sftp/mysftp

```bash
mkdir -p /data/sftp/mysftp  
usermod -d /data/sftp/mysftp mysftp  
```

### 配置sshd_config

文本编辑器打开 /etc/ssh/sshd_config

```bash
找到如下这行，用#符号注释掉，大致在文件末尾处。
# Subsystem      sftp    /usr/libexec/openssh/sftp-server  
在文件最后面添加如下几行内容，然后保存。

Subsystem       sftp    internal-sftp    
Match Group sftp    
ChrootDirectory /data/sftp/%u    
ForceCommand    internal-sftp    
AllowTcpForwarding no    
X11Forwarding no  
```

### 设定Chroot目录权限

```bash
chown root:sftp /data/sftp/mysftp  
chmod 755 /data/sftp/mysftp  
```

### 建立SFTP用户登入后可写入的目录

照上面设置后，在重启sshd服务后，用户mysftp已经可以登录。但使用chroot指定根目录后，根应该是无法写入的，所以要新建一个目录供mysftp上传文件。这个目录所有者为mysftp，所有组为sftp，所有者有写入权限，而所有组无写入权限。命令如下：

```
mkdir /data/sftp/mysftp/upload  
chown mysftp:sftp /data/sftp/mysftp/upload  
chmod 755 /data/sftp/mysftp/upload  
```

### 修改/etc/selinux/config

```bash
# /etc/selinux/config 中
将文件中的SELINUX=enforcing 修改为 SELINUX=disabled ，然后保存。

#bash终端在输入命令
setenforce 0  
```

### 重启sshd服务

```
service sshd restart  
```

### 验证sftp环境
用mysftp用户名登录，yes确定，回车输入密码。

sftp mysftp@127.0.0.1  

显示 sftp> 则sftp搭建成功。

### Reference
* http://www.cnblogs.com/reed/p/5516474.html
