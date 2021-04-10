---
title: Navigator.sendBeacon-关闭页面提交数据
date: 2021-04-10 22:15:48
tags:
- JavaScript
- Web
categories:
- 零散笔记
---
navigator.sendBeacon() 方法可用于通过HTTP将少量数据异步传输到Web服务器
> 适用于当用户关闭页面、刷新页面或者跳转到其他页面时，需要向服务器发送一些记录数据，并且不关心服务器返回值的场景

<!--more-->

## 描述
使用`sendBeacon()`方法会使用户代理在有机会时异步地向服务器发送数据，同时不会延迟页面的卸载或影响下一导航的载入性能。这就解决了提交分析数据时的所有的问题：数据可靠，传输异步并且不会影响下一页面的加载。

## 语法
```
navigator.sendBeacon(url, data);
```

参数|说明
---|---
url|表明 data 将要被发送到的网络地址
data|将要发送的`ArrayBufferView`、`Blob`、`DOMString`或`FormData`类型的数据

## 参考代码

一般常用 DOMString , Blob 和 Formdata 这三种对象作为数据发送到后端，下面以这三种方式为例进行说明：
```
// 1. DOMString类型，该请求会自动设置请求头的 Content-Type 为 text/plain
const reportData = (url, data) => {
  navigator.sendBeacon(url, data);
};

// 2. 如果用 Blob 发送数据，这时需要我们手动设置 Blob 的 MIME type，
// 一般设置为 application/x-www-form-urlencoded。
const reportData = (url, data) => {
  const blob = new Blob([JSON.stringify(data), {
    type: 'application/x-www-form-urlencoded',
  }]);
  navigator.sendBeacon(url, blob);
};

// 3. 发送的是Formdata类型，
// 此时该请求会自动设置请求头的 Content-Type 为 multipart/form-data。
var data = {
   name: '前端名狮子'  ,
   age: 20
};
const reportData = (url, data) => {
  const formData = new FormData();
  Object.keys(data).forEach((key) => {
    let value = data[key];
    if (typeof value !== 'string') {
      // formData只能append string 或 Blob
      value = JSON.stringify(value);
    }
    formData.append(key, value);
  });
  navigator.sendBeacon(url, formData);
};

```
