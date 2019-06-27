# Distributed Lock | 分布式锁

- [聊聊分布式锁](https://parg.co/RD4): 两种锁的实现方式都很简单，应用情景也很显然，悲观锁更适合写密集的情景；而乐观锁，通常需要借助 CAS 实现，形成一定程度上比较简单的「无锁」结构，更适合读密集的情景。

# Redis-Based Lock

- [2017-Distributed locks with Redis](https://redis.io/topics/distlock): Distributed locks are a very useful primitive in many environments where different processes must operate with shared resources in a mutually exclusive way.

- [使用 Redis 实现分布式锁](http://blog.jobbole.com/95211/)

- [如何用 Redis 造一把分布式锁](http://sanyuesha.com/2016/08/20/distributed-lock-with-redis/):
