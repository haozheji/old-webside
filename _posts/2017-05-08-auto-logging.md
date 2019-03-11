---
layout: post
title:  Git和ssh自动登录
categories: Tricks
tags: [git, ssh]
---

## Git自动登录
在git push之前输一条命令可将密码保存到硬盘.
```terminal
$ git config credential.helper store
```
密码保存在用户目录的.git-credentials文件中.

## ssh-keygen实现自动登陆ssh

### 生成RSA密钥和公钥
```
ssh-keygen -t rsa
```

然后一路回车就可以了。（中间有设置密码提示，用来加密密钥）
会生成`id_rsa`和`is_rsa.pub`两个文件，前者密钥保留在本地，公钥分配到需要登录的服务器上。

### 公钥同步到服务器
只需要一条命令就行
```
ssh-copy-id username@remote-server
```
中间输入一次远程登录密码，SSH公钥就会自动上传了。公钥保存在`/home/username/.ssh/authorized_keys`文件中。之后使用ssh登录或者scp传输文件都不需要登录了。



