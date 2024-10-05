[enmotech/opengauss - Docker Image | Docker Hub](https://hub.docker.com/r/enmotech/opengauss)

拉取集群启动

```bash
docker run --name opengauss --privileged=true -d -e GS_PASSWORD=Secretpassword@123 -u root -p 15432:5432 enmotech/opengauss:latest

遇到的问题：配置文件报错不存在，手工创建一个
touch /usr/local/opengauss/etc/gscgroup_omm.cfg
```

连接 dbeaver

![image.png](https://note.youdao.com/yws/res/756/WEBRESOURCE2877b8e1d97cf8ccbecbb2296a752247)
