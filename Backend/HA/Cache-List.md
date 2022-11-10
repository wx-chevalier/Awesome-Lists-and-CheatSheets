# Cache List

# Overview

## Case Study | 案例分析

- [2019-知乎已读服务的前生今世与未来](https://zhuanlan.zhihu.com/p/68383301): 为了避免给用户推荐重复的内容，已读服务会将所有知乎站上用户深入阅读或快速掠过的内容长期保存，并将这些数据应用于首页推荐信息流和个性化推送的已读过滤。

# Concept | 缓存概念

- [2018-The hidden components of Web Caching](https://parg.co/UFt): Let’s take a bottom-up approach to understanding the various layers of caching.

- [深入浅出 Cache](http://tech.youzan.com/cache-background/)

- [Caching Explained](https://cachingexplained.com/#caching-explained)

# Strategy | 缓存策略

- [2016-缓存架构设计细节二三事](https://parg.co/UFN): 本文主要讨论这么几个问题：“缓存与数据库”需求缘起，“淘汰缓存”还是“更新缓存”，缓存和数据库的操作时序，缓存和数据库架构简析。

- [缓存使用总结](https://fdx321.github.io/2016/09/09/%E7%BC%93%E5%AD%98%E4%BD%BF%E7%94%A8%E6%80%BB%E7%BB%93/)

- [2017-美团缓存那些事](http://geek.csdn.net/news/detail/172308)：在网络分层应用服务中，缓存的使用已比较普及，本文将结合作者实际工作经验总结，讲述在不同的场景下如何选择和使用适用的缓存框架，以达到提升服务质量，优化系统架构的目的。

- [腾讯互娱技术总监：不止于思路，谈高性能服务器架构之道中的缓存策略](http://dbaplus.cn/news-21-504-1.html)

- [缓存系统在游戏业务中的特异性](https://parg.co/UFM)

- [缓存级别与缓存更新问题](https://parg.co/bs3)：缓存失效问题被认为是计算机科学中最难的两件事之一，这篇文章来自翻译，内容主要包括缓存级别与缓存更新常见的几种模式。

- [2016-Design of a Modern Cache](http://highscalability.com/blog/2016/1/25/design-of-a-modern-cache.html): In this article we will explore the modern methods used by Caffeine, an open-source Java caching library, that yield high hit rates and excellent concurrency.

# Architecture | 缓存架构

- [2019-这些年，我们一起追过的缓存数据库](https://mp.weixin.qq.com/s/zJnqmZqlwYGkC8BXHwjzjw): 畅途网为了解决节假日或高峰期的车次查询、抢票等大数据量的访问请求，很早以前就引进了 Redis，来作为数据库的上游缓存层，缓解底层数据库的读写压力。
