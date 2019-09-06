---
description: 作者：金龙
---

# homebrew安装maven

## brew查找maven版本：

```bash
brew search maven
```

## brew安装其中的3.5版：

\(安装maven需要有jdk环境，也就是需要提前装好java\)

```bash
brew install maven@3.5
```

## 设置环境变量

```bash
echo 'export PATH="/usr/local/opt/maven@3.5/bin:$PATH"' >> ~/.bash_profile
```

```bash
source ~/.bash_profile
```

（如果使用的是zsh，那么需要把.bash\_profile改为.zshrc文件）

## 验证安装成功

```bash
mvn -version
```

看到版本信息表示安装正确

## 如何卸载

使用brew install 命令安装的，可以用brew uninstall进行卸载。

