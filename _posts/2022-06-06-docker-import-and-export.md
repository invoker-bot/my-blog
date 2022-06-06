---
layout: post
title:  "Docker Import and Export"
date:   2022-06-06 13:53:30 +0800
categories: docker
---

# Docker的导入和导出

Docker拿给别人使用时，就需要将镜像或者容器导出给别人使用，一般可用分为从源码导出和二进制导出。

## Docker源码导出

如果镜像是从Dockerfile构建的，那么可用直接将整个仓库打包发给别人，使用时从Dockerfile再构建就行了，但这种方式比较耗时，且不能保护源码。

## Docker二进制导出

1. 从镜像文件导出

可以使用导出镜像

```shell
docker save IMAGE > IMAGE.tar
```

再使用

```shell
docker load < IMAGE.tar
```

即可加载镜像

2. 从容器中导出

导出容器成为镜像

```shell
docker export CONTAINER > CONTAINER.tar
```

从文件中导入

```shell
docker import - IMAGE:tag < CONTAINER.tar
```

3. 上传至Docker Hub

```shell
# 首先登录
docker login
# 打上标签
docker tag IMAGE Repository/IMAGE:latest
# 上传
docker push Repository/IMAGE:latest
```


