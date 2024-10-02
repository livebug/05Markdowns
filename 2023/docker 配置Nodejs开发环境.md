# docker 配置Nodejs开发环境

## 配置私有npm库

详见 \[docker Running Verdaccio]\
注意：` docker network  inspect bridge` 查看 Verdaccio 容器地址

## 拉取镜像并启动

    docker pull node:16.14.2 # LTS版本

    docker run -itd --name node-dev node:16.14.2 # 启动
    docker run -itd --rm -p 6666:22 --name node-ng node  

替换`source.list`文件

    echo '
    deb https://mirrors.aliyun.com/debian/ bullseye main non-free contrib
    deb-src https://mirrors.aliyun.com/debian/ bullseye main non-free contrib
    deb https://mirrors.aliyun.com/debian-security/ bullseye-security main
    deb-src https://mirrors.aliyun.com/debian-security/ bullseye-security main
    deb https://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib
    deb-src https://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib
    deb https://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib
    deb-src https://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib
    ' > /etc/apt/sources.list

安装 openssh

保存当前镜像

    docker ps
    docker commit 9041ea324bd0 node-ng

## 配置NPM源为 私有库

    npm set registry http://172.17.0.3:4873/  # localhost 换为 Verdaccio 容器地址

## 试运行

     npm install -g @angular/cli

能成功运行即可
