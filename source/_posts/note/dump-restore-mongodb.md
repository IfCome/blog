---
title: 备份和还原MongoDB
date: 2021-04-12 14:26:16
tags:
- MongoDB
categories:
- 零散笔记
---

记录MongoDB备份和还原的简单使用

## 备份
```
mongodump -h dbhost -d dbname -o dbdirectory
```

<!--more-->
参数|说明
---|---
-h|MongoDB 所在服务器地址，例如：127.0.0.1，也可以指定端口号：127.0.0.1:27017
-d|需要备份的数据库实例，例如：testDB
-o|备份的数据存放位置，例如：c:\data\dump，当然该目录需要提前建立，在备份完成后，系统自动在dump目录下建立一个testDB目录，这个目录里面存放该数据库实例的备份数据。

例如：
```
mongodump -h 127.0.0.1 -d demoDB -o C:\data\dump\demoDB
```

## 还原
```
mongorestore -h dbhost -d dbname <path>
```
参数|说明
---|---
-h|MongoDB 所在服务器地址，例如：127.0.0.1，也可以指定端口号：127.0.0.1:27017。默认为： localhost:27017
-d|需要备份的数据库实例，例如：testDB
`<path>`|备份的数据存放位置，例如：c:\data\dump\demoDB

例如，恢复`demoDB`到`localhost:27017`：
```
mongorestore -d demoDB C:\data\dump\demoDB
```
