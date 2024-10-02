docker 设置容器自启动

新容器

```bash
docker run --restart=always [container_id]
```

已经存在的容器

```bash
docker update --restart=always [container_id]
```

