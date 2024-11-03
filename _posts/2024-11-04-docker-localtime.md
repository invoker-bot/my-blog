---
layout: post
title:  "Docker Local Time"
date:   2024-11-04 00:50:55 +0800
categories: code
---

# Docker时间本地化

在Docker中容器默认的时间是+0000时区的标准时间，这是因为Docker容器没有主机本地化时区的信息，如果想将Docker时区设置为本地时间，在Linux上只需要将时间挂载到相应卷上即可，在`docker-compose.yml`中可以写作：

```yaml
volumes:
  - /etc/localtime:/etc/localtime:ro
  - /etc/timezone:/etc/timezone:ro
```
