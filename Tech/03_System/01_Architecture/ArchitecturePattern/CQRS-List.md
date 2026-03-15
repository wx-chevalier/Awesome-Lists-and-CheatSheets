# Architectural Pattern List

# CQRS

- [2014-CQRS 架构简介](https://www.cnblogs.com/netfocus/p/4055346.html): 要想高性能，需要尽量：避开网络开销（IO），避开海量数据，避开资源争夺。对于这 3 点，我觉得很有道理。所以也想谈一下，CQRS 架构下是如何实现高性能的。

- [Building Scalable Applications Using Event Sourcing and CQRS](https://medium.com/@ikem/event-sourcing-and-cqrs-a-look-at-kafka-e0c1b90d17d8#.bqrq7j3fa)

- [2017~分享一个 CQRS/ES 架构中基于写文件的 EventStore 的设计思路](https://blog.csdn.net/kxinyu/article/details/78140970): EventStore 是在 Event Sourcing（下面简称 ES）模式中，用于存储事件用的。从 DDD 的角度来说，每个聚合根在自己的状态发生变化时都会产生一个或多个领域事件，我们需要把这些事件持久化起来。

- [2019~cqrs-hotel ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/luontola/cqrs-hotel): Example application about CQRS and Event Sourcing #NoFrameworks

- [2019~event-sourcing-cqrs-examples ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/andreschaffer/event-sourcing-cqrs-examples): Event Sourcing and CQRS in practice.
