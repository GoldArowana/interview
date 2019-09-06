---
description: 作者：金龙
---

# homebrew安装jdk8

## 概念引入

> **brew 是从下载源码解压然后./configure && make install,同时会包含相关依存库。并自动配置 好各种环境变量，而且易于卸载。**
>
> **而brew cask是已经编译好了的应用包\(.dmg/.pkg\). 仅仅是下载解压，放在统一的目录中\(/opt/homebrew-cask/Caskroom\),**
>
> **省掉了自己去下载、解压、拖拽\(安装\)等蛋疼的步骤，同样，卸载相当容易与干净。**
>
> _作者：野沐沐 来源：CSDN 原文：_[_https://blog.csdn.net/yanxiaobo1991/article/details/78455908_](https://blog.csdn.net/yanxiaobo1991/article/details/78455908) _版权声明：本文为博主原创文章，转载请附上博文链接！_

## 帮助文档

可以执行--help来看帮助文档

```bash
brew cask --help
```

## 搜索不到jdk8？

通过这两行命令是获取不到jdk8信息的

```bash
brew cask info java
```

```bash
brew search java
```

## 如何能搜到jdk8?

需要你先执行一下这行命令： 

```bash
brew tap caskroom/versions
```

之后再执行

```text
brew cask info java8
```

或

```bash
brew search java
```

## 安装jdk8

```bash
brew cask install java8
```

## 验证安装成功

执行命令

```bash
java -version
```

看到java版本信息就表示成功了

## 如何卸载？

卸载也只需要一句命令

```bash
brew cask uninstall java8
```

## tap如何删除？

使用untap命令

```bash
brew untap caskroom/versions
```

## 如何安装jdk11/jdk12?

与安装jdk8同理，只需要把数字8改为对应的大版本号就可以了。

