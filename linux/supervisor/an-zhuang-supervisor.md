# 安装supervisor

## 建议安装python3

```text
brew install python3
```

## 使用python安装supervisor：

```text
python3 -m pip install supervisor
```

## 生成配置文件

```text
echo_supervisord_conf > /opt/conf/supervisord.conf
```

## supervisord.conf配置

```text
[unix_http_server]
file=/tmp/supervisor.sock   ; the path to the socket file
chmod=0766                 ; socket file mode (default 0700)
;chown=nobody:nogroup       ; socket file uid:gid owner
;username=user              ; default is no username (open server)
;password=123               ; default is no password (open server)
```

最下方添加：

```text
[program:hera01]     # 程序名字
directroy=/home/user01/arowana  # 程序所在的主目录
command=java -jar -server Hera-jar-with-dependencies.jar  # 执行程序的命令  
autostart=true   # 是否自动启动程序
startsecs=5      # 程序启动5秒种没有中断默认启动成功
autorestart=true # 是否重启
startretries=3   # 重启失败尝试次数
user=root        # 执行程序的用户
```

## 启动supervisor

```text
supervisord -c /opt/conf/supervisord.conf
```

## 打开supervisorctl

```text
supervisorctl -c /opt/conf/supervisord.conf
```













