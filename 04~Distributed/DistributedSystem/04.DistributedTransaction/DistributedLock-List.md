# Distributed Lock | 分布式锁

- [聊聊分布式锁](https://parg.co/RD4): 两种锁的实现方式都很简单，应用情景也很显然，悲观锁更适合写密集的情景；而乐观锁，通常需要借助 CAS 实现，形成一定程度上比较简单的无锁结构，更适合读密集的情景。

- [高并发下本地锁+分布式锁](https://adamswanglin.github.io/wllock/)

# Redis Lock

- [2017~Distributed locks with Redis](https://redis.io/topics/distlock): Distributed locks are a very useful primitive in many environments where different processes must operate with shared resources in a mutually exclusive way.

- [使用 Redis 实现分布式锁](http://blog.jobbole.com/95211/)

- [如何用 Redis 造一把分布式锁](http://sanyuesha.com/2016/08/20/distributed-lock-with-redis/):

# Consul Lock

- [基于 Consul 的分布式锁实现](http://blog.didispace.com/spring-cloud-consul-lock-and-semphore/)：我们在构建分布式系统的时候，经常需要控制对共享资源的互斥访问。这个时候我们就涉及到分布式锁(也称为全局锁)的实现，基于目前的各种工具，我们已经有了大量的实现方式，比如：基于 Redis 的实现、基于 Zookeeper 的实现。本文将介绍一种基于 Consul 的 Key/Value 存储来实现分布式锁以及信号量的方法。
