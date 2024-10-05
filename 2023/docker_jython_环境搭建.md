# docker jython 环境搭建

1.  建立容器环境  ubuntu
    ```bash
    # 拉取容器
    docker run -d --name jypthon_dev_ubuntu ubuntu
    # 进入容器
    docker exec -it jypthon_dev_ubuntu  /bin/bash
    ```
2.  下载文件 jython 与 jdk7 安装包
3.  安装jdk7
    ```bash
    mkdir /usr/java/
    tar -zxvf jdk-7u80-linux-x64.tar.gz -C /usr/java/

    # 临时配置变量
    export JAVA_HOME=/usr/java/jdk1.8.0_351
    export JRE_HOME=${JAVA_HOME}/jre
    export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
    export PATH=${JAVA_HOME}/bin:$PATH
    java -version

    # 永久配置变量 注意变量哈跟前面的临时一起执行
    echo "
    export JAVA_HOME=/usr/java/jdk1.7.0_80
    export JRE_HOME=${JAVA_HOME}/jre
    export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
    export PATH=${JAVA_HOME}/bin:$PATH
    " >> /etc/bash.bashrc      
    ```

