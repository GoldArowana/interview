### 从github上clone代码的时候太慢了，可以借助`码云`做个中转，提个速

1. 在`码云`上新建一个仓库，选择`导入已有仓库`，然后填入`github`中用于`git clone`的http地址。例如以本项目为例那就是：`https://github.com/GoldArowana/learning.git`  
![](picture/码云导入2.jpg)
1. 点击`创建`，然后等待`码云`从`github`上拉取资源。大概在1分钟以内。
1. 然后使用`码云`的地址，进行`git clone`。
1. `git clone`完之后，在本地打开项目，然后在项目根目录执行命令。这样就把远程地址修改为了github里的地址
```shell
git remote set-url origin xxxx.git
```
（其中xxx.git替换为github里的项目地址，以本项目为例那就是：`git@github.com:GoldArowana/learning.git`）

