# ubuntu 安装java8.md

## 下载java jdk 

http://www.codebaoku.com/jdk/jdk-oracle-jdk1-8.html

jdk-8u351-linux-x64.tar.gz

## 安装
```bash
sudo cp jdk-8u351-linux-x64.tar.gz /usr/local/
sudo tar -zxvf jdk-8u351-linux-x64.tar.gz
```

## 配置全局变量
``` bash
# 可以配置 etc/profile 或者 用户目录下的 .profile 或者 .bashrc


export JAVA_HOME=/usr/local/jdk1.8.0_351

export JRE_HOME=$JAVA_HOME/jre

export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib/rt.jar

export PATH=$PATH:$JAVA_HOME/bin
```