---
description: 作者：金龙
---

# 安装zookeeper

## zookeeper docker-hub：

{% embed url="https://hub.docker.com/\_/zookeeper" %}

## zookeeper docker-doc：

{% embed url="https://docs.docker.com/samples/library/zookeeper/" %}

## 运行

目前最新版本是3.5 ，拉取这个版本的zookeeper

```bash
docker pull zookeeper:3.5
```

创建文件   /opt/conf/zoo.cfg，然后在里面添加如下配置：

```text
dataDir=/data
dataLogDir=/datalog
tickTime=2000
initLimit=5
syncLimit=2
autopurge.snapRetainCount=3
autopurge.purgeInterval=0
maxClientCnxns=60
standaloneEnabled=false
server.1=192.168.0.175:2888:3888;2181
server.2=192.168.0.175:2889:3889;2182
server.3=192.168.0.175:2890:3890;2183
4lw.commands.whitelist=stat, ruok, conf, isro
```

（其中192.168.0.175是内网ip）

然后依次运行3个zookeeper

```bash
docker run -e "ZOO_MY_ID=1" --name zk1 --network host -d -v /opt/conf/zoo.cfg:/conf/zoo.cfg zookeeper:3.5
docker run -e "ZOO_MY_ID=2" --name zk2 --network host -d -v /opt/conf/zoo.cfg:/conf/zoo.cfg zookeeper:3.5
docker run -e "ZOO_MY_ID=3" --name zk3 --network host -d -v /opt/conf/zoo.cfg:/conf/zoo.cfg zookeeper:3.5
```

## 检验

依次执行下面三个命令，来检测服务：

```bash
echo stat | nc 11.115.132.189 2181
echo stat | nc 11.115.132.189 2182
echo stat | nc 11.115.132.189 2183
```

其中11.115.132.189是外网ip，因为我是把zookeeper安装在了远程服务器，用我的个人笔记本来运行nc命令，所以用的是外网ip。

可以看到zk1是follower。

![](../../.gitbook/assets/image%20%2887%29.png)

## 使用客户端

在本地使用docker打开zookeeper客户端进行连接：

```bash
docker run -it --rm  zookeeper:3.5 zkCli.sh -server 114.115.132.189:2181
```





