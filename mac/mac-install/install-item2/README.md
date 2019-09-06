---
description: 作者：金龙
---

# 安装iterm2及一些快捷键

## 简介

item2是mac下的终端工具。具体有点可以参考这里：

{% embed url="https://www.jianshu.com/p/558d6ea9d0db" %}

## 下载

打开官网进行下载：

{% embed url="https://iterm2.com/" %}

## 安装

解压后双击即可安装。

之后会弹出一个选项，让你选择是否将item放进应用列表里，选择“move to Application”。

## 后续

安装完成后，在/bin目录下会有zsh

可以使用命令修改默认使用zsh作为终端：

```bash
chsh -s /bin/zsh
```

以后可以通过这个命令修改回默认终端dash：

```bash
chsh -s /bin/bash
```

## 效果

![](../../../.gitbook/assets/image%20%2866%29.png)

## 快捷键

打开偏好

![](../../../.gitbook/assets/image%20%288%29.png)

然后录入快捷键，我录入的是command + .

以后就可以根据快捷键 显示/隐藏 iterm了

![](../../../.gitbook/assets/image%20%2847%29.png)

## iterm其他自带功能

### 基础

1. 选中即复制，不需要额外进行ctrl + c操作
2. 搜索，快捷键 command + f
3. 可以拖拽选中的字符串
4. 访问url链接，按住command键点击url
5. 访问文件，按住command键点击文件名
6. 矩形选中，按住command键和opt键进行选中操作
7. iterm最大化，command + enter
8. 聚焦到光标位置，command + /
9. 在所有窗口中进行搜索，command + alt + e
10. 打开剪贴板历史，command + shift + h
11. 自动补全，command + ;

### 分屏

1. 纵向分屏，command + d
2. 横向分屏，command + shift + d
3. 关闭分屏，command + w
4. 分屏后进行小屏之间的跳转，command + opt + 方向键（或 command + \[ ）
5. 隐藏/显示 其他的分屏，command + shift + enter

### tab

1. 新建tab，command + t
2. tab之间跳转，command + 方向键
3. 将当前的tab与右边的tab交换位置，command + shift + 右方向键
4. 快速跳转到指定的tab上，command + 数字键

### 标记

1. 标记一行，command + shift + m
2. 跳转到上个标记，command + shift + 上
3. 清除所有标记，command + shift + k

### **回放**

**回访可以看到iterm里的历史操作，在回放中按住“左”键，就像是在看监控录像似的。**

1. 进入回放，command + opt + b
2. 进/退回访，方向键左/右
3. 退出回放，esc

### 最近目录

快捷键command + opt + /    可以查看iterm中使用的最近目录。

第一次输入这个快捷键的时候回提示安装，点击“Install Now”

![](../../../.gitbook/assets/image%20%289%29.png)

然后还会弹出一个弹窗，点击安装

![](../../../.gitbook/assets/image%20%2876%29.png)

之后还会弹出一个弹窗，点击OK就好了。之后就会开始执行安装操作

安装完毕后，退出iterm，重新打开iterm，然后使用快捷键command + opt + /   即可查看最近目录。

![](../../../.gitbook/assets/image%20%2877%29.png)





