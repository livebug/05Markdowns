docker 查看容器的IP

```bash
docker inspect opengauss | grep IPAddress # 查看IP

docker inspect opengauss | grep Gateway # 查看网关
```

