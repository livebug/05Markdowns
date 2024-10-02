# 离线安装nuget库

1. 登录 nuget官网下载包
2. 使用如下命令安装

    ```
    dotnet add package  [库名] -s [存放库的本地文件夹] 
    ```

* 如果是预览包 需要加上 `--prerelease` 允许安装预发行包。