---
description: 作者：金龙
---

# Error response from daemon

当执行docker pull 命令时，报了如下错误

```text
Error response from daemon: Get https://registry-1.docker.io/v2/: net/http: TLS handshake timeout
```

网上有多种解决方法，其中我参考了daocloud的方案（使用国内的daocloud的镜像），官网：

{% embed url="https://www.daocloud.io/mirror\#accelerator-doc" %}

Docker For Mac的方式：

右键点击桌面顶栏的 docker 图标，选择 Preferences ，在 Daemon 标签（Docker 17.03 之前版本为 Advanced 标签）下的 Registry mirrors 列表中加入下面的镜像地址:

```text
http://f1361db2.m.daocloud.io
```

然后点击 Apply & Restart 按钮使设置生效。



windows和linux的方式可以参考官网。官网首页的最下面介绍的很详细了。





