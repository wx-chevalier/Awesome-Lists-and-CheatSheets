# Architectural Pattern List

# CQRS

- [2014-CQRS 架构简介](https://www.cnblogs.com/netfocus/p/4055346.html): 要想高性能，需要尽量：避开网络开销（IO），避开海量数据，避开资源争夺。对于这 3 点，我觉得很有道理。所以也想谈一下，CQRS 架构下是如何实现高性能的。

- [Building Scalable Applications Using Event Sourcing and CQRS](https://medium.com/@ikem/event-sourcing-and-cqrs-a-look-at-kafka-e0c1b90d17d8#.bqrq7j3fa)

- [2017-分享一个 CQRS/ES 架构中基于写文件的 EventStore 的设计思路](https://blog.csdn.net/kxinyu/article/details/78140970): EventStore 是在 Event Sourcing（下面简称 ES）模式中，用于存储事件用的。从 DDD 的角度来说，每个聚合根在自己的状态发生变化时都会产生一个或多个领域事件，我们需要把这些事件持久化起来。

- [2019-cqrs-hotel #Project#](https://github.com/luontola/cqrs-hotel): Example application about CQRS and Event Sourcing #NoFrameworks

- [2019-event-sourcing-cqrs-examples #Project#](https://github.com/andreschaffer/event-sourcing-cqrs-examples): Event Sourcing and CQRS in practice.

# COLA

- [COLA #Project#](https://github.com/alibaba/COLA): COLA 是 Clean Object-Oriented and Layered Architecture 的缩写，代表“整洁面向对象分层架构”，也叫“可乐”架构。

- [2017-企业应用架构实践（复杂性应对之道）](https://yq.aliyun.com/articles/285590): 形成了我们自己现在的基于扩展点+元数据+CQRS+DDD 的应用架构。该架构的特点是可扩展性好，很好的贯彻了 OO 思想，有一套完整的规范标准，并采用了 CQRS 和领域建模技术，在很大程度上可以降低应用的复杂度。本文主要阐述了我们的思考过程和架构实现，希望能对在路上的你有所帮助。

# Clean Architecture

- [2021-Clean Architecture Solution Template #Project#](https://github.com/jasontaylordev/CleanArchitecture): Clean Architecture Solution Template for Angular 10 and .NET 5
