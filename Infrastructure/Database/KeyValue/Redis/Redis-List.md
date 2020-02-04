# Redis List

- [Redis 存储海量小数据，如何优化内存使用](http://zzyongx.github.io/blogs/redis-memory-optimization-when-store-small-data.html) s

- [Redis 的内存优化](https://cachecloud.github.io/2017/02/16/Redis%E5%86%85%E5%AD%98%E4%BC%98%E5%8C%96/)

- [Redis 架构之防雪崩设计：网站不宕机背后的兵法](http://mp.weixin.qq.com/s/TBCEwLVAXdsTszRVpXhVug)：互联网系统中不可避免要大量用到缓存，在缓存的使用过程中，架构师需要注意哪些问题？本文以 Redis 为例，详细探讨了最关键的 3 个问题。

# Overview

- [你不可不知的 Redis 常用命令](http://www.epubit.com.cn/article/504)

- [data-types-intro](https://github.com/antirez/redis-doc/blob/master/topics/data-types-intro.md)

- [Redis 的数据类型和抽象概念介绍](http://ifeve.com/redis-data-types-intro/)

- [Redis 缓存失效机制](http://my.oschina.net/andylucc/blog/679222)

## Resource

- [The Little Redis Book 中文教程](https://github.com/JasonLai256/the-little-redis-book/blob/master/cn/redis.md)

## Case Study

- [2018-携程 Redis 容器化实践](https://mp.weixin.qq.com/s/uqMrYp7FTI11zBIm8kiTLg): 携程的 Redis 使用规模有 200T+，并且每天有百万亿次的访问频率，如此大规模的 Redis 容器化对于我们来说是个不小的挑战，本文分享携程 Redis 容器化落地的一些实践经验。

# Cluster | 集群架构

## Sharding

- [2016-这可能是最全的 Redis 集群方案介绍了](https://parg.co/Kne): 各大企业在 3.0 版本还没发布前为了解决 Redis 的存储瓶颈，纷纷推出了各自的 Redis 集群方案。这些方案的核心思想是把数据分片（sharding）存储在多个 Redis 实例中，每一片就是一个 Redis 实例。

- [2017-Redis 集群实现原理探讨](https://parg.co/by5)：Redis  集群是一个 distribute、fault-tolerant 的 Redis 实现，主要设计目标是达到线性可扩展性、可用性、数据一致性。

## Redis Cluster

- [Redis 集群的合纵与连横](http://blog.csdn.net/mindfloating/article/details/50458768)

- [全面剖析 Redis Cluster 原理和应用](http://blog.csdn.net/dc_726/article/details/48552531)

- [Redis Cluster 分区实现原理](http://my.oschina.net/andylucc/blog/704440)

- [深入浅出 Redis Cluster 原理](http://mp.weixin.qq.com/s?__biz=MzA3MzYwNjQ3NA==&mid=2651296996&idx=2&sn=5f4811d73e74e2a63b1cb0d3d532862a)

## HA | 高可用架构

- [2016-Redis 集群“倾斜”问题 ](https://zhuoroger.github.io/2016/08/03/redis-cluster-imbalance/)

- [Redis Cluster 架构优化](http://blog.csdn.net/dc_726/article/details/48733265)

- [如何部署高可用的 Redis 集群架构](http://rdc.hundsun.com/portal/article/669.html)：本文主要介绍 redis 在不同模式下的部署方式，并且对几种模式进行了一些简单的对比。

# Engineering Practices

## Optimization

- [Redis 内存使用优化与存储](http://blog.jobbole.com/106466/)

- [Redis 时延问题分析及应对](http://blog.jobbole.com/99099/): 在笔者自己的 Redis 的实践中，发现 Redis 本身的并发能力还是非常强悍的，但是往往瓶颈会发生在网络延迟中。

- [Redis 数据丢失问题](https://zhuoroger.github.io/2016/08/14/redis-data-loss/)

- [如何优雅地删除 Redis 大键](https://zhuoroger.github.io/2016/08/12/redis-delete-large-keys/)

- [Redis 的性能幻想与残酷现实](http://mp.weixin.qq.com/s?__biz=MzAxMTEyOTQ5OQ==&mid=401738746&idx=1&sn=281af530d5abec981f3607d6e729914a&scene=21#wechat_redirect)

- [Under the Hood of Redis](http://redisplanet.com/redis/under-the-hood-of-redis-hash-part-1/)
