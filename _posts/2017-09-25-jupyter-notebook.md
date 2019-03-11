---
layout: post
title: 远程登录jupyter notebook
categories: Tricks
tags: [jupyter notebook]
---

# 服务器端

## 1.生成配置文件

```bash
$ jupyter notebook --generate-config
```

<!--more-->

## 2.生成登录密码

进入ipython

```python
from notebook.auth import passwd
passwd()
```

会生成一个密钥'sha1...' 复制下来.

## 3.修改配置文件

```
c.NotebookApp.ip='localhost' 设置本地端口可访问
c.NotebookApp.password = u'sha:ce...刚才复制的那个密文'
c.NotebookApp.open_browser = False # 禁止自动打开浏览器
c.NotebookApp.port =8888 #随便指定一个端口
```

## 4.启动jupyter notebook

```bash
$ jupyter notebook
```

# 本地端

## 1.端口映射

*为了更方便使用,在使用ssh登录服务器时进行端口映射

```bash
ssh user@remote_server_ip -L 1024 127.0.0.1:8888
```

例如将服务器的本地端口8888映射到本机的1024端口

## 2.远程登录jupyter notebook

在本机浏览器登录127.0.0.1:1024,并输入在服务器设定的明文密码.
