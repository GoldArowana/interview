---
description: 作者：金龙
---

# 安装mysql5.7

mysql docker-hub：

{% embed url="https://hub.docker.com/\_/mysql" %}

mysql docker-doc：

{% embed url="https://docs.docker.com/samples/library/mysql/" %}

以5.7.25版为例 ，拉取这个版本的mysql：

```text
docker pull mysql:5.7.25
```

## 运行服务

```text
docker run -p 3306:3306 --name mysql5 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7.25
```

### 运行客户端

```text
docker exec -it mysql5 /usr/bin/mysql -u root -p
```

## 异常问题记录

### docker0: iptables: No chain/target/match by that name

```text
错误原因：修改iptables规则后，重启了iptables，但没有重启docker

解决方案：重启docker: service restart docker
```

### docker 启动mysql 闪退 无法启动问题

{% embed url="https://blog.csdn.net/white\_bird\_shit/article/details/87343187" %}

{% embed url="https://blog.csdn.net/shinaiqing/article/details/70132424" %}









