---
layout: post
title: ssh-keygen实现密钥登录远程服务器
---

最近互联网上爆发了加密病毒，实验室的服务器疑似被入侵了。
最终定下来只使用一台32服务器连外网作为出口，另外两台通过32登录，且关闭ssh密码登录，转而使用ssh-keygen密钥实现自动登录。写篇短文以记录配置过程。
<!--more-->
## 1.首先在本地端生成RSA密钥和公钥
```
ssh-keygen -t rsa
```

然后一路回车就可以了。（中间有设置密码提示，用来加密密钥）
会生成`id_rsa`和`is_rsa.pub`两个文件，前者密钥保留在本地，公钥分配到需要登录的服务器上。
## 2.将SSH公钥上传到服务器
只需要一条命令就行
```
ssh-copy-id username@remote-server
```
中间输入一次远程登录密码，SSH公钥就会自动上传了。公钥保存在`/home/username/.ssh/authorized_keys`文件中。之后使用ssh登录或者scp传输文件都不需要登录了。


