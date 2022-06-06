---
layout: post
title:  "Docker Proxy"
date:   2022-06-06 14:47:00 +0800
categories: docker
---

# Docker代理设置

## 一般代理

为了更方便地上传下载，通常我们会在本机开一个HTTP协议的代理，这种情况下设置`http_proxy`和`https_proxy`到**http://localhost:1081**即可(我喜欢Socks代理设为1080，而Http代理设为1081，当然根据个人喜好设置)

### 在VSCODE设置代理

一般只有Git会用到，所以只需在`settings.json`文件中添加如下即可，其中操作系统要根据实际情况更换。
```json
"terminal.integrated.env.windows": {
    "http_proxy":"http://localhost:1081",
    "https_proxy":"http://localhost:1081"
}
```

### 在Docker中使用代理

一般情况下只有在`build`时才需使用代理，因此添加
```
--build-arg http_proxy=http://host.docker.internal:1081 --build-arg https_proxy=http://host.docker.internal:1081
```
即可，注意从Docker访问宿主机不能使用`localhost`而要使用`host.docker.internal`。

## 使用镜像

通常，除了访问GitHub必须使用代理，下载包都可以配置镜像网站访问。
常用的一些办法是：

1. `Node.js`的包可以在`npm install`时加上`--registry https://registry.npm.taobao.org`(默认为`https://registry.npmjs.org`)，或者使用`cnpm`，或`nrm`。

2. `Python`可以在`pip3 install`时指定`--index-url https://pypi.tuna.tsinghua.edu.cn/simple`(默认为`https://pypi.org/simple`)，或者在全局设置`pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple`。
