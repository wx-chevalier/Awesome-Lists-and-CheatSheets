# Cluster | 集群架构

## Sharding

- [2016~这可能是最全的 Redis 集群方案介绍了](https://parg.co/Kne): 各大企业在 3.0 版本还没发布前为了解决 Redis 的存储瓶颈，纷纷推出了各自的 Redis 集群方案。这些方案的核心思想是把数据分片（sharding）存储在多个 Redis 实例中，每一片就是一个 Redis 实例。

- [2017~Redis 集群实现原理探讨](https://parg.co/by5)：Redis 集群是一个 distribute、fault-tolerant 的 Redis 实现，主要设计目标是达到线性可扩展性、可用性、数据一致性。

## Redis Cluster

- [Redis 集群的合纵与连横](http://blog.csdn.net/mindfloating/article/details/50458768)

- [全面剖析 Redis Cluster 原理和应用](http://blog.csdn.net/dc_726/article/details/48552531)

- [Redis Cluster 分区实现原理](http://my.oschina.net/andylucc/blog/704440)

- [深入浅出 Redis Cluster 原理](http://mp.weixin.qq.com/s?__biz=MzA3MzYwNjQ3NA==&mid=2651296996&idx=2&sn=5f4811d73e74e2a63b1cb0d3d532862a)

## HA | 高可用架构

- [2016~Redis 集群“倾斜”问题 ](https://zhuoroger.github.io/2016/08/03/redis-cluster-imbalance/)

- [Redis Cluster 架构优化](http://blog.csdn.net/dc_726/article/details/48733265)

- [如何部署高可用的 Redis 集群架构](http://rdc.hundsun.com/portal/article/669.html)：本文主要介绍 redis 在不同模式下的部署方式，并且对几种模式进行了一些简单的对比。
