安装前提是要安装git&#x20;

下载 下载页面：[Gitea | gitea](https://dl.gitea.com/gitea/)

解压之后把文件提升为可执行

```bash
chmod +x gitea
```

剩下的就是给gitea找个目录作为网站的根目录

**关键：linux配置服务**

```bash
$ cat gitea.service
[Unit]
Description=Gitea (Git with a cup of tea)
After=syslog.target
After=network.target

[Service]
RestartSec=2s
Type=simple
User=nuc # gitea的系统用户 这个启动时会有认证
Group=nuc
#WorkingDirectory=/var/lib/gitea/  # 这个没必要设置
ExecStart=/gitea/gitea web --config /gitea/conf/app.ini  # 必须写清楚目录，且用户在该目录存在权限 
Restart=always
#Environment=USER=nuc HOME=/home/nuc GITEA_WORK_DIR=/gitea

[Install]
WantedBy=multi-user.target
```

将 `gitea.service` 文件放到 `/etc/systemd/system` 下

启动服务

```bash
# 运行
systemctl start gitea
# 查看是否成功运行
ps -aux | grep gitea
# 如果成功会看到一条git用户运行的gitea进程
ps -aux | grep gitea
nuc        81764  0.1  0.5 1981092 171708 ?      Ssl  3月04   2:10 /gitea/gitea web --config /gitea/conf/app.ini
nuc        88083  0.0  0.0  12132   720 pts/0    S+   12:44   0:00 grep --color=auto gitea
# 开机启动
systemctl enable gitea

```

也可以不使用服务，直到目录下执行 gitea 程序就行
