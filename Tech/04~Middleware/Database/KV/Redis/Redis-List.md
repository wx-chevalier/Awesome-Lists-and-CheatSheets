# Redis List

- [Redis 存储海量小数据，如何优化内存使用](http://zzyongx.github.io/blogs/redis-memory-optimization-when-store-small-data.html) s

- [Redis 的内存优化](https://cachecloud.github.io/2017/02/16/Redis%E5%86%85%E5%AD%98%E4%BC%98%E5%8C%96/)

- [Redis 架构之防雪崩设计：网站不宕机背后的兵法](http://mp.weixin.qq.com/s/TBCEwLVAXdsTszRVpXhVug)：互联网系统中不可避免要大量用到缓存，在缓存的使用过程中，架构师需要注意哪些问题？本文以 Redis 为例，详细探讨了最关键的 3 个问题。

# Overview

- [你不可不知的 Redis 常用命令](http://www.epubit.com.cn/article/504)

- [data-types-intro](https://github.com/antirez/redis-doc/blob/master/topics/data-types-intro.md)

- [Redis 的数据类型和抽象概念介绍](http://ifeve.com/redis-data-types-intro/)

- [Redis 缓存失效机制](http://my.oschina.net/andylucc/blog/679222)

## Case Study

- [2018\_携程 Redis 容器化实践](https://mp.weixin.qq.com/s/uqMrYp7FTI11zBIm8kiTLg): 携程的 Redis 使用规模有 200T+，并且每天有百万亿次的访问频率，如此大规模的 Redis 容器化对于我们来说是个不小的挑战，本文分享携程 Redis 容器化落地的一些实践经验。

# Resources

- [The Little Redis Book 中文教程](https://github.com/JasonLai256/the-little-redis-book/blob/master/cn/redis.md)

# OpenSource

- [RedisGraph ![code](https://ng-tech.icu/assets/code.svg)](http://redisgraph.io/design/): A High Performance In-Memory Graph Database as a Redis Module.

- [2018_RDR ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/xueqiu/rdr): RDR(redis data reveal) is a tool to parse redis rdbfile. Comparing to redis-rdb-tools, RDR is implemented by golang, much faster (5GB rdbfile takes about 2mins on my PC).

## Extended Edition

- [2018_KeyDB ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/JohnSully/KeyDB): A Multithreaded Fork of Redis

- [2020_Kvrocks ![code](https://ng-tech.icu/assets/code.svg)](https://mp.weixin.qq.com/s/fJi5JEATVcuQVtysqqJp_w): Kvrocks 是基于 RocksDB 之上兼容 Redis 协议的 NoSQL 存储服务，设计目标是提供一个低成本以及大容量的 Redis 服务，作为 Redis 在大数据量场景的互补服务，选择兼容 Redis 协议是因为简单易用且业务迁移成本低。目前线上使用的公司包含: 美图、携程、百度以及白山云等，在线上经过两年多大规模实例的验证。

## Management

- [Redis-shake ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/alibaba/RedisShake): Redis-shake 是一个用于在两个 redis 之间同步数据的工具，满足用户非常灵活的同步、迁移需求。

- [2019_Redis Manager ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/ngbdf/redis-manager): Redis 一站式管理平台，支持集群的监控、安装、管理、告警以及基本的数据操作。

- [2019_Medis ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/luin/medis): 💻 Medis is a beautiful, easy-to-use Mac database management application for Redis.

- [2023_Tiny RDM ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/tiny-craft/tiny-rdm)](https://github.com/tiny-craft/tiny-rdm): Tiny RDM is a modern lightweight cross-platform Redis desktop manager available for Mac, Windows, and Linux.

- [2024_RedisInsight ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/RedisInsight/RedisInsight)](https://github.com/RedisInsight/RedisInsight): Redis Insight is a visual tool that provides capabilities to design, develop, and optimize your Redis application. Query, analyse and interact with your Redis data. Download it here!
