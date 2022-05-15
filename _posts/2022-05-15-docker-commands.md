---
layout: post
title:  "Docker Commands Cheat Sheet"
date:   2022-05-15 16:26:29 +0800
categories: docker
---

# Docker 常用命令

## 检查安装
 
### 1.检查信息

*语法*

```shell
docker info
```

*作用*

查看镜像(Image)，容器(Container)，系统(Operating System)及配置(CPU)。

### 2.检查版本

*语法*

```shell
docker version
```

*作用*

查看Docker(Client/Server)的版本。

## 镜像操作

### 1.查看镜像

*语法*

```shell
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

**OPTIONS:**
+ -a : 所有镜像
+ --digetsts : 详细

*作用*

列出本地属于**REPOSITORY**或**TAG**的所有镜像。

### 2.查看镜像历史

*语法*

```shell
docker history [OPTIONS] IMAGE
```

*作用*

查看某镜像的使用历史。

### 3.构建镜像

*语法*

```shell
docker build [OPTIONS] PATH | URL
```

**OPTIONS:**
+ -f path : Dockerfile的路径
+ --build-arg [] : 构建传入的参数
+ --tag, -t name:tag : 镜像的名字和标签
+ --rm : 删除中间容器

*作用*

从Dockerfile中构建镜像并添加到本地。

### 4.拉取镜像

*语法*

```shell
docker pull NAME[:TAG|@DIGEST]
```

*作用*

从**Docker Hub**上下载镜像。

### 5.推送镜像

*语法*

```shell
docker push NAME[:TAG]
```

*作用*

上传本地镜像到**Docker Hub**，必须先登录才能上传。

### 6.登录登出

*语法*

```shell
docker login [OPTIONS]
```

```shell
docker logout
```

**OPTIONS:**
+ -u USER : 用户名
+ -p PASSWORD : 密码

*作用*

登录登出仓库。

### 7.查找镜像

*语法*

```shell
docker search TERM
```

*作用*

查找可用的镜像。

### 8.删除镜像

*语法*

```shell
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

**OPTIONS:**
+ -f 强制删除

*作用*

移除镜像。

### 9.增加标签

*语法*

```shell
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

*作用*

增加一个标签，可以命名为**REPOSITORY/NAME:VERSION**。

### 10.保存镜像

*语法*
 
```shell
docker save -o ARCHIEVE IMAGE [IMAGE...]
```

*作用*

将镜像存储到压缩归档文件中。

### 11.加载镜像

*语法*
 
```shell
docker load -i ARCHIEVE
```

*作用*

将压缩归档文件中的所有镜像加载出来。

## 容器操作

### 1.导入

*语法*

```shell
docker import [OPTIONS] file|URL [REPOSITORY[:TAG]]
```

**OPTIONS:**
* -c IMAGE : 指定镜像
* -m MESSAGE : 描述

*作用*

其实是导入镜像，可用于生成容器。

### 2.导出

*语法*

```shell
docker export -o ARCHIEVE CONTAINER
```

*作用*

从容器生成归档。

### 3.查看容器

*语法*

```shell
docker ps [OPTIONS]
```

**OPTIONS:**
* -a : 显示所有
* -l : 显示最近
* -s : 显示大小

*作用*

检查容器的状态。


### 4.查看容器信息

*语法*

```shell
docker inspect CONTAINER
```

*作用*

查看容器的配置信息。

### 5.查看容器进程

*语法*

```shell
docker top CONTAINER [ps OPTIONS]
```

*作用*

查看容器中有哪些进程。

### 6.运行

*语法*

```shell
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

**OPTIONS:**
* -d : 后台运行
* -it : 交互运行
* --name NAME : 容器名字
* -p HOST_PORT:CONTAINER_PORT : 端口映射
* -e KEY="VALUE" : 环境变量
* --env-file FILENAME : 从文件中读取
* --gpus GPUS : 使用GPU数量,用all使用所有
* --cpus CPUS : 限制CPU数量
* -m, --memory MEMORY : 限制内存
* --runtime RUNTIME : 使用的内核
* --stop-timeout TIMEOUT : 最大运行时间,默认单位秒
* -v, --volume HOST_VOLUME:CONTAINER_VOLUME : 数据映射
* -w, --workdir WORKDIR : 工作目录
* -u, --user USER : 工作用户
* --rm : 工作完后移除容器

*作用*

调用容器执行指定的命令，可用于临时容器和持久容器。


### 7.状态

*语法*

```shell
docker start/stop/restart/kill CONTAINER
```

```shell
docker pause/unpause
```

*作用*

启动、停止、重启、暂停一个容器。

### 8.创建删除

*语法*

```shell
docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

同`run`命令。

```shell
docker rm [OPTIONS] CONTAINER
```

**OPTIONS:**
* -f : 强制删除
* -l CONNECT : 移除连结
* -v : 删除卷

*作用*

移除容器。

### 9.附加

*语法*

```shell
docker attach [OPTIONS] IMAGE
```

**OPTIONS:**
* --sig-proxy BOOL : 是否转发所有信号,可设为false避免容器退出

```shell
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

**OPTIONS:**
* -d : 后台命令
* -it : 交互命令

*作用*

连接到容器并执行一些操作。

```shell
docker wait [OPTIONS] CONTAINER
```

阻塞等待容器退出。

### 10.查看端口映射

*语法*

```shell
docker port CONTAINER
```

*作用*

查看容器的端口映射。

### 11.日志

*语法*

```shell
docker logs [OPTIONS] CONTAINER
```

**OPTIONS:**
* -f : 跟踪输出
* --since DATE : 开始日期
* -t : 显示时间
* --tail N : 仅列出N条日志

*作用*

获取容器日志。

### 12.事件

*语法*

```shell
docker events [OPTIONS]
```

**OPTIONS:**
* --since DATE : 开始日期
* --until DATE : 截止日期

*作用*

获取Docker事件。
