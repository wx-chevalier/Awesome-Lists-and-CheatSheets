

# Redis Internals List

# Internals | 内部原理

## Event Loop

- [Redis 网络架构及单线程模型 ](http://my.oschina.net/andylucc/blog/679222)

- [Redis 异步组件化模型](http://my.oschina.net/andylucc/blog/693981)

- [2016-Redis 中的事件循环](https://draveness.me/redis-eventloop): 在目前的很多服务中，由于需要持续接受客户端或者用户的输入，所以需要一个事件循环来等待并处理外部事件，这篇文章主要会介绍 Redis 中的事件循环是如何处理事件的。

- [2018-Redis 源码阅读——基于 epoll 的事件模型](https://blog.csdn.net/idwtwt/article/details/79460217): Redis 的事件模型实现基于 linux 的 epoll，sun 的 export,FreeBSD 和 Mac osx 的 queue，还有 select。

## Commands

- [深入理解 Redis：命令处理流程 ](http://blog.csdn.net/hanhuili/article/details/17339005)

## Communication

- [深入浅出 Redis client/server 交互流程](http://www.infoq.com/cn/articles/communication-redis-clientserver)

- [深入浅出 Redis client/server 交互流程 ](http://mp.weixin.qq.com/s/M_8JYKounmZWHPOXVJFNuQ)

- [Redis 客户端查询缓冲区和输出缓冲区 ](https://zhuoroger.github.io/2016/07/30/redis-client-two-buffers/)

## DataTypes

- [Redis 压缩列表原理与应用分析](http://my.oschina.net/andylucc/blog/715325)

- [Redis 内部数据结构详解之跳跃表(skiplist) ](http://blog.csdn.net/acceptedxukai/article/details/17333673)
