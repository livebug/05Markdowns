---
title : 'docker 设置容器自启动'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: ['docker']
categories: ['应用技术']
---
# docker 设置容器自启动

新容器

```bash
docker run --restart=always [container_id]
```

已经存在的容器

```bash
docker update --restart=always [container_id]
```

