---
title : 'Antlt4 基础介绍-安装'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: ['antlr4']
categories: ['应用技术']
---
# Antlt4

## Install  ANTLR v4 on unix

*   Install Java (version 1.7 or higher)
    Download
    `$cd /usr/local/lib
     $` curl -O <https://www.antlr.org/download/antlr-4.9-complete.jar>
    Or just download in browser from website: <https://www.antlr.org/download.html> and put it somewhere rational like /usr/local/lib.

*   Add antlr-4.9-complete.jar to your CLASSPATH:
    `$ export CLASSPATH=".:/usr/local/lib/antlr-4.9-complete.jar:$`CLASSPATH"
    It's also a good idea to put this in your .bash\_profile or whatever your startup script is.

*   Create aliases for the ANTLR Tool, and TestRig.
    `$ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$`CLASSPATH" org.antlr.v4.Tool'
    `$ alias grun='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$`CLASSPATH" org.antlr.v4.gui.TestRig'

## antlr4 安装 2

不多说先放地址 <https://github.com/antlr/antlr4/blob/master/doc/getting-started.md>

```bash
$ cd /usr/local/lib
$ curl -O https://www.antlr.org/download/antlr-4.10.1-complete.jar
# 后面的写到 .bashrc 中
$ export CLASSPATH=".:/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH"
$ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.Tool'
$ alias grun='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.gui.TestRig'
```

## Book source code

The book has lots and lots of examples that should be useful too. You can download them here for free:

<http://pragprog.com/titles/tpantlr2/source_code>

Also, there is a large collection of grammars for v4 at github:

<https://github.com/antlr/grammars-v4/>



---
---

# wsl-ubuntu20使用与antlr安装

## wsl Ubuntu20.04 初始化

### 新增 sha 用户

```bash
$ adduser sha
```

### 指定进入根目录

```bash
$ vi /etc/passwd

找到类似的（应该是最后一个）
sha:x:1000:1001:sharif,sharif,,:/sha:/bin/bash
```

### 指定目录权限

```bash
# 为 sha 用户赋 /sha 目录权限
$  chown -R sha:sha /sha
# 赋权
$ chmod 700 /sha
```

### 将用户加入到sudo组

```bash
sudo usermod -G sudo username 
或
sudo vim /etc/sudoers
```

## antlr4 安装

不多说先放地址 <https://github.com/antlr/antlr4/blob/master/doc/getting-started.md>

```bash
$ cd /usr/local/lib
$ curl -O https://www.antlr.org/download/antlr-4.9-complete.jar
# 后面的写到 .bashrc 中
$ export CLASSPATH=".:/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH"
$ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.Tool'
$ alias grun='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.gui.TestRig'
```

