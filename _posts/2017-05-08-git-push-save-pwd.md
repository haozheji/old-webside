---
layout: page
title: git push repo 时保存密码的命令
---
在git push之前输一条命令可将密码保存到硬盘.
```terminal
$ git config credential.helper store
```
密码保存在用户目录的.git-credentials文件中.
