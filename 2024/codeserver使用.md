---
title : 'codeserver 介绍'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: ['codeserver']
categories: ['应用技术']
--- 
# codeserver 启动和使用

这个就是web端的的vscode，但是是开源社区的，不是微软的。

## 下载 github

[Release v4.90.3 · coder/code-server · GitHub](https://github.com/coder/code-server/releases/tag/v4.90.3)

## 安装

```bash
mkdir -p ~/.local/lib ~/.local/bin
tar -C ~/.local/lib -xz  code-server-4.90.3-linux-amd64.tar.gz
tar -C ~/.local/lib -xzf code-server-4.90.3-linux-amd64.tar.gz
mv ~/.local/lib/code-server-4.90.3-linux-amd64/ ~/.local/lib/code-server-4.90.3
ln -s ~/.local/lib/code-server-4.90.3/bin/code-server ~/.local/bin/code-server
```

## bashrc 需要把`.local/bin`添加到PATH

```bash
export PATH="~/.local/bin/:$PATH"
```

正常一般都已经加入了

## 启动codeserver

直接执行 `code-server`  就可以；启动配置文件目录：`~/.config/code-server/config.yaml`

```yaml
bind-addr: 0.0.0.0:7891
auth: password
password: ssssss
cert: false
```

安装插件的目录: `~/.local/share/code-server/extensions`

Fedora 安装 python3.11

[Linux 无root 无sudo 安装python3_无sudo权限安装python 3.10.9 linux-CSDN博客](https://blog.csdn.net/qq_36303832/article/details/119090299#:~:text=Linux%20%E6%97%A0root%20%E6%97%A0sudo%20%E5%AE%89%E8%A3%85python3)

Q1: 检查失败时，因为缺少关键开发组件

```bash
dnf groupinstall "Development Tools"
```

dotnet无法执行

```bash
C# 插件是针对vscode特色开发的，codeserver是开源搞的，虽然可以修改插件库，安装C#插件，但是无法使用官方调试。
只能用开源的进行调试
```
