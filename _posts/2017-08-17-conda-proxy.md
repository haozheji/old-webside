---
layout: post
title: conda proxyerror 解决办法
categories: Tricks
tags: [conda]
---
长时间没在本机上用conda安装包了,最近一段时间想装一些东西,发现总是报httperror的错误.

<!--more-->

```bash
CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://repo.continuum.io/pkgs/free/linux-64/repodata.json.bz2>
Elapsed: -

An HTTP error occurred when trying to retrieve this URL.
HTTP errors are often intermittent, and a simple retry will get you on your way.
ConnectionError...
```
之前在服务器端的conda配置了代理,所以怀疑本机上也是代理的问题.
之前用meow设置了全局代理,应该包括bash也是.所以应该要让conda越过代理(其实感觉bash开代理意义不大).
找到一篇相关问题的贴[https://github.com/ContinuumIO/anaconda-issues/issues/1326](https://github.com/ContinuumIO/anaconda-issues/issues/1326),但我的问题没有详细说是proxyerror,估计因为不是conda内部的代理的缘故.
有一个解决方法是在bash设置环境变量:
```bash
set NO_PROXY=continuum.io,anaconda.org
```
不过这个方法好像不能永久有效(?)
