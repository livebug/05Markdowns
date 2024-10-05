---
title : 'ubuntu 永久挂载硬盘'
date : 2023-10-08T22:39:48+08:00
toc: true
tags: [ubuntu]
categories: ['应用技术']
---
# ubuntu永久挂载硬盘

> 转载 <https://blog.csdn.net/u013171226/article/details/107680262>

## 1. 查看服务器上未挂载的硬盘。

*   `fdisk -l`
*   `lsblk`
*   `blkid` 查已挂载的硬盘的 uuid

## 2. 将磁盘挂载在某个地方

*   `mount  <需要挂载的盘具体盘符（最小分支）> <需要挂载的路径>`

## 3. `df -h ` 查看磁盘信息

## 4. 自动挂载

```bash
sudo vim /etc/fstab
```

加入以下内容分

盘符路径  挂载路径  ext4  defaults 0  1

    # <file system> <mount point>   <type>  <options>       <dump>  <pass>
    UUID=CE7CBD917CBD74B5 /data ntfs defaults 0 0 

