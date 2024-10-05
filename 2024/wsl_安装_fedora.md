---
title : 'wsl 安装 fedora'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: [wsl,fedora]
categories: ['应用技术']
---
# wsl 安装 fedora

# 初始化Fedora

## 安装wsl

直接软件商店安装就行，使用命令行总是因为网络问题加载慢

安装后是默认root用户，Fedora的密码要求比较高

## WSL挪动位置

[WSL2迁移至其他目录 - 槑孒 - 博客园](https://www.cnblogs.com/echohye/p/17712482.html)

```powershell
wsl --shutdown
wsl --export Fedora E:\WSL\Fedora.tar
wsl --unregister Fedora
wsl --import Fedora E:\WSL\Fedora E:\WSL\Fedora.tar --version 2
fedora.exe config --default-user app
```

## WSL指定用户登录

```bash
wsl --user root
```

## ROOT用户执行的脚本

```bash
# 增加用户和目录空间
useradd app 
mkdir /app 
chown -R app:app /app
```

## APP用户需要配置的

### .bashrc 文件

```bash
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

# User specific environment
if ! [[ "$PATH" =~ "$HOME/.local/bin:$HOME/bin:" ]]; then
    PATH="$HOME/.local/bin:$HOME/bin:$PATH"
fi
export PATH

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
if [ -d ~/.bashrc.d ]; then
    for rc in ~/.bashrc.d/*; do
        if [ -f "$rc" ]; then
            . "$rc"
        fi
    done
fi
unset rc 
alias l='ls -ltr'
export PS1='[\u@\h $PWD]$' # 命令行-展示全部路径
```

### 当设置app用户的启动目录：

* Q: `# usermod: user xxx is currently used by process xxxx`​

需要用root用户登录调整，且要求app用户未登录，wsl登录用root用户，然后调整

```bash
usermod -d /app app
```

> 修改启动目录，需要把用户配置文件同步复制到新目录中，不然就都失效啦!
