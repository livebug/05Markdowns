---
title : 'ubuntu openssh 说明'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: [ubuntu]
categories: ['应用技术']
---
# ubuntu-openssh说明

## OpenSSH Server

<https://ubuntu.com/server/docs/service-openssh>

## Installation

Installation of the OpenSSH client and server applications is simple. To install the OpenSSH client applications on your Ubuntu system, use this command at a terminal prompt:

    sudo apt install openssh-client

To install the OpenSSH server application, and related support files, use this command at a terminal prompt:

    sudo apt install openssh-server

## 安装 `net-tools`

    apt-get install net-tools

## 设置允许Root登录

    #sudo vim /etc/ssh/sshd_config

找到并用#注释掉这行：`PermitRootLogin prohibit-password`

新建一行 添加：`PermitRootLogin yes`

重启服务

    sudo service ssh restart

    sudo passwd root   #设置密码

然后ssh root\@192.168.2.21就可以登录了

### 设置开机自启动

sudo systemctl enable ssh
