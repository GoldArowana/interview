## redis学习路线

1. 建议先到[redis中文网][1]、[菜鸟教程][6]、[redisfans][7]去浏览一下redis相关的内容，先对它有一个简单的了解
1. 看书的话，建议先看[《Redis实战》][2]。书里的示例代码是python。
    - 书中语言：python
    - 随书代码：书里还提供了一个链接，可以下载示例代码，里面有全书的python代码，也有全套对应的java代码。
    - 推荐原因：我觉得这本书是讲redis的书中讲的最简单的。而且作者不仅仅是把redis的相关命令使用了一遍，还把redis的相应结构和命令应用到了项目中。虽然项目很小，但是作者能给出每种结构的应用场景，非常有助于对redis使用和应用的理解。
    - 预期收获：看完这本书后，可以根据场景，在自己的项目中试着加入redis技术了。
1. 看完《Redis实战》之后，建议看看[《Redis设计与实现》][3]的第1部分（全书分为4部分）。
    - 书中语言：伪代码(c/c++/java系的同学都可以看懂)
    - 相关代码：我不记得书中有没有代码链接了，不过可以去看看《Redis设计与实现》作者的github，里面或许有你想要的：https://github.com/huangz1990
    - 推荐原因：第1部分讲的是redis的一些数据结构，可以对redis内部有一些简单的了解。
    - 预期收获：看完第1部分后，如果掌握的还不错，这个阶段就可以`简单`应对一些`校招`面试中的redis相应问题了。
1. 看完《Redis设计与实现》的第1部分后，可以看看[《redis深度历险》][4]，里面讨论了实践中的一些问题，原理也更加深入。
    - 预期收获：估计不用看完这本，就可以应对`校招`中的大多数面试题了。
1. 如果对源码有更高的追求，可以看看[《深入理解redis》][5]，这本书我刚入门的时候看过，看的我经常睡着，后来就不怎么看了，也找不到了。但是根据我印象，这本书讲的还是很细节的。
    - 建议：可读可不读。（我就没读完...）
1. 想直接通过源码来学习redis的同学，可以直接到github下载redis源码。但是github上能搜到的最低版本是redis2.0，我这里给出一个更低的版本redis0.1版的源码：链接:https://pan.baidu.com/s/1bRZKFPGWBVFzA7dgsYIyug  密码:udpy
    - 建议：0.1的我倒是简单看了看。（高版本的源代码我还没看过）
1. 如果对redis比较熟悉了，那么可以再翻一翻《Redis设计与实现》的后3个部分。（后三个部分是我强忍着看完的，因为有不理解的地方或者看完总忘得地方。准备再刷第二遍）
    - 预期收获：到这个程度的话，对redis是蛮熟悉了。在公司内做个小规模的技术分享应该不是问题。
## redis学习资料
- [【菜鸟教程】redis教程](https://www.runoob.com/redis/redis-tutorial.html)
- [【redisfans】Redis 命令参考](http://doc.redisfans.com/)
- [【redis中文网】redis命令手册](https://www.redis.net.cn/order/)
- [【京东】Redis实战](https://item.jd.com/11791607.html)
- [【京东】Redis设计与实现](https://item.jd.com/11486101.html)
- [【京东】Redis 深度历险：核心原理与应用实践](https://item.jd.com/12464009.html)
- [【掘金手册】Redis 深度历险：核心原理与应用实践](https://juejin.im/book/5afc2e5f6fb9a07a9b362527)
- [【京东】深入理解Redis](https://item.jd.com/12069785.html)

[1]: https://www.redis.net.cn/order/ "【菜鸟教程】redis教程"
[6]: https://www.runoob.com/redis/redis-tutorial.html "【菜鸟教程】redis教程"
[2]: https://item.jd.com/11791607.html "【京东】Redis实战"
[3]: https://item.jd.com/11486101.html "【京东】Redis设计与实现"
[4]: https://item.jd.com/12464009.html "【京东】Redis 深度历险：核心原理与应用实践"
[5]: https://item.jd.com/12069785.html "【京东】深入理解Redis"
[7]: http://doc.redisfans.com/ "【redisfans】Redis 命令参考"

## 备注
当然，这些只是我的一个总结，如果有更好的建议，也欢迎大家提出来。