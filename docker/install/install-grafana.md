# 安装grafana

## grafana docker-hub

{% embed url="https://hub.docker.com/r/grafana/grafana" %}

目前最新版本是6.1.2 ，拉取这个版本的grafana：

```bash
docker pull grafana/grafana:6.1.2
```

## 运行

```text
docker run -d --name=grafana -p 3000:3000 grafana/grafana:6.1.2
```

## 打开grafana控制台

[http://localhost:3000](http://localhost:3000)，账号：admin，密码：admin





