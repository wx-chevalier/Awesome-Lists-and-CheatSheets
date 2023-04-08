# Distributed Transaction List

# Overview

- [2016-分布式系统事务一致性解决方案](http://www.infoq.com/cn/articles/solution-of-distributed-system-transaction-consistency): 大型互联网平台往往是由一系列分布式系统构成的，开发语言平台和技术栈也相对比较杂，尤其是在 SOA 和微服务架构盛行的今天，一个看起来简单的功能，内部可能需要调用多个“服务”并操作多个数据库或分片来实现，情况往往会复杂很多。单一的技术手段和解决方案，已经无法应对和满足这些复杂的场景了。

- [2021-微服务下分布式事务模式的详细对比](https://www.infoq.cn/article/qrsqlqqpboboud3z5mfy): 本文不会深入介绍事务的细节，而是总结了向多个数据源协调写入操作的主要方式和模式。我知道，你可能对这些方法有过美好或糟糕的经验。但是实践中，在正确的环境和正确的限制条件下，这些方法都能很好地工作。技术领导者要为自己的环境选择最好的方式。

# 多阶段提交

- [分布式协议之两阶段提交协议(2PC)和改进三阶段提交协议(3PC)](http://www.mamicode.com/info-detail-890945.html)

- [关于分布式事务、两阶段提交、一阶段提交、Best Efforts 1PC 模式和事务补偿机制的研究](http://blog.csdn.net/bluishglc/article/details/7612811)

- [分布式事务 2PC && 3PC](http://int64.me/2016/%E5%88%86%E5%B8%83%E5%BC%8F%E4%BA%8B%E5%8A%A12PC%20&&%203PC.html)

- [深入理解分布式系统的 2PC 和 3PC](http://www.hollischuang.com/archives/1580)

- [关于分布式事务、两阶段提交协议、三阶提交协议](http://www.hollischuang.com/archives/681)

# 事务消息

# 分布式锁的实现

## Redis

- [使用 Redis 实现分布式锁](http://blog.jobbole.com/95211/)
