---
title: Git 同时 push 到多个远程仓库
date: 2021-03-29 16:07:38
tags:
- git
categories:
- 零散笔记
---

使用以下命令添加第二个远程地址：
```
git remote set-url --add origin https://gitee.com/notop/blog.git
```

<!--more-->

查看远程分支：
```
$ git remote -v
origin  https://github.com/IfCome/blog.git (fetch)
origin  https://github.com/IfCome/blog.git (push)
origin  https://gitee.com/notop/blog.git (push)
```

这样就能同时 push 到多个远程地址
```
$ git push origin master
Everything up-to-date
Everything up-to-date
```