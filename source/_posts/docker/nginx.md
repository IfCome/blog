---
title: Docker部署简单Nginx
date: 2021-04-14 10:07:38
tags:
- docker nginx
categories:
- Docker
---

## 1. 使用Dockerfile部署
首先来看下目录结构及配置文件：

{% asset_img folder.png 文件夹目录 %}

<!--more-->

``` config mydefault.conf
server {
    #这里就是把默认config的80端口改为8080端口
    listen       8080;
    listen  [::]:8080;
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```

``` config Dockerfile
FROM nginx:alpine
COPY demoWeb /usr/share/nginx/html
COPY mydefault.conf /etc/nginx/conf.d/default.conf
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### 执行docker build进行构建
```
docker build -t my_nginx:v1 .
```

### 运行
```
docker run -d -p80:8080 my_nginx:v1
```
