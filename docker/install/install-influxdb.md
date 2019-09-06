---
description: 作者：金龙
---

# 安装influxdb

influxdb docker-hub：

{% embed url="https://hub.docker.com/\_/influxdb" %}

influxdb docker-doc：

{% embed url="https://docs.docker.com/samples/library/influxdb/" %}

目前最新版本是1.7 ，拉取这个版本的influxdb：

```text
docker pull influxdb:1.7
```

## 运行

```text
docker run -d -p8083:8083 -p8086:8086 --expose 8090 --expose 8099 --name influx01 influxdb:1.7
```

## 官方文档

有些API照着网上的博客使用，发现并不好使。最好是参考官网文档，对应1.7版：

{% embed url="https://docs.influxdata.com/influxdb/v1.7" %}

## 使用HTTP接口来操作influxdb数据库

### 创建数据库

```text
curl -XPOST 'http://localhost:8086/query' --data-urlencode 'q=CREATE DATABASE "mydb"'
```

### 显示所有数据库

```text
curl -XPOST 'http://localhost:8086/query' --data-urlencode 'q=SHOW DATABASES'
```

### 删除数据库

```text
curl -XPOST 'http://localhost:8086/query' --data-urlencode 'q=DROP DATABASE "mydb"'
```





## 客户端

```text
docker exec -it influx01 /usr/bin/influx
```

