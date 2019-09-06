---
description: 作者：金龙
---

# 安装redis

redis docker-hub：

{% embed url="https://hub.docker.com/\_/redis" %}

redis docker-doc：

{% embed url="https://docs.docker.com/samples/library/redis/" %}

目前最新版本是5.0.4 ，拉取这个版本的redis：

```text
docker pull redis:5.0.4
```

## 启动server

方式一：指定持久化路径：

```text
docker run -p 6379:6379 --name redis -v /opt/data/redis:/data  -d redis:5.0.4 redis-server --appendonly yes
```

方式二：指定配置文件启动：

```text
docker run -p 6379:6379 -v /redis/data:/data -v /redis/redis.conf:/redis/r.conf  -d redis:latest redis-server /redis/r.conf
```

## 启动client

如果是在同一台机器上client连接自己的server，那么ip就是内网ip。

如果是client去连接远程server，那么ip处填写外网ip。

```text
docker run -it --rm redis:5.0.4 redis-cli -h 192.168.0.175
```





