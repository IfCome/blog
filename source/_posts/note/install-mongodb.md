---
title: 配置MongoDB + 安装为Windows服务
date: 2021-04-02 15:34:45
tags:
- MongoDB
categories:
- 零散笔记
---
为了方便在同一台服务器上配置多个版本的MongoDB服务，我选择了去[Mongodb官网](https://www.mongodb.com/download-center/community/releases/archive)下载zip文件，手动配置服务，以下以实例说明。文件解压至路径`“D:\Program Files\mongodb\Server\4.0.6\”` 。

<!--more-->

## 创建配置文件
新建文件`D:\Program Files\mongodb\Server\4.0.6\bin\mongod.cfg` :

```
# Where and how to store data.
storage:
  dbPath: D:\Program Files\mongodb\Data\4.0.6
  journal:
    enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path:  D:\Program Files\mongodb\Log\4.0.6\mongod.log

# network interfaces
net:
  port: 27017
# bindIp: 127.0.0.1
  bindIp: 0.0.0.0
```
## 注册服务
使用CMD执行命令：
```
"D:\Program Files\mongodb\Server\4.0.6\bin\mongod.exe" --config "D:\Program Files\mongodb\Server\4.0.6\bin\mongod.cfg" --install --serviceName "MongoDB406"
```
> 注意：避免使用Powershell，可能会报错

## 启动与关闭MongoDB服务
```
net start MongoDB406
net stop MongoDB406
```

## 移除MongoDB服务
```
"D:\Program Files\mongodb\Log\4.0.6\bin\mongod.exe" --remove --serviceName "MongoDB406"
```

