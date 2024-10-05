---
title : 'C# dotnet 离线安装nuget库'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: ['C#']
categories: ['应用技术']
---
# 离线安装nuget库

1. 登录 nuget官网下载包
2. 使用如下命令安装

    ```
    dotnet add package  [库名] -s [存放库的本地文件夹] 
    ```

* 如果是预览包 需要加上 `--prerelease` 允许安装预发行包。