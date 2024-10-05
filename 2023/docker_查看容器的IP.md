---
title : 'docker 查看容器的IP'
date : 2023-10-08T22:39:48+08:00
toc: true
tabs: ['docker']
categories: ['应用技术']
---
docker 查看容器的IP

```bash
docker inspect opengauss | grep IPAddress # 查看IP

docker inspect opengauss | grep Gateway # 查看网关
```

