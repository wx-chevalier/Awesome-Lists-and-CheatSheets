# RPC

# Showcase

- [2020~guide-rpc-framework ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/Snailclimb/guide-rpc-framework)](https://github.com/Snailclimb/guide-rpc-framework): A custom RPC framework implemented by Netty+Kyro+Zookeeper.（一款基于 Netty+Kyro+Zookeeper 实现的自定义 RPC 框架-附详细实现过程和相关教程。）

- [2020~My-RPC-Framework ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/CN-GuoZiyang/My-RPC-Framework)](https://github.com/CN-GuoZiyang/My-RPC-Framework): My-RPC-Framework 是一款基于 Nacos 实现的 RPC 框架。网络传输实现了基于 Java 原生 Socket 与 Netty 版本，并且实现了多种序列化与负载均衡算法。

- [2020~MyRPCFromZero ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/he2121/MyRPCFromZero)](https://github.com/he2121/MyRPCFromZero): 从零开始，手写一个 RPC，跟随着这篇文档以及数个迭代版本的代码，由简陋到逐渐完备，让所有人都能看懂并且写出一个 RPC 框架。

## RPC Protocol

- [Hessian]()

- [Protobuf]()

- [2021~Kryo ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/EsotericSoftware/kryo)](https://github.com/EsotericSoftware/kryo): Kryo is a fast and efficient binary object graph serialization framework for Java. The goals of the project are high speed, low size, and an easy to use API. The project is useful any time objects need to be persisted, whether to a file, database, or over the network.

# RPC Frameworks

- [brpc ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/brpc/brpc): Most common RPC framework used throughout Baidu, with 600,000+ instances and 500+ kinds of services, called "baidu-rpc" inside Baidu.

- [gRPC ![code](https://ng-tech.icu/assets/code.svg)](https://grpc.io/docs/guides/): gRPC is a modern, open source, high-performance remote procedure call (RPC) framework that can run anywhere. It enables client and server applications to communicate transparently, and makes it easier to build connected systems.

- [rpcx ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/smallnest/rpcx): Faster multil-language bidirectional RPC framework in Go, like alibaba Dubbo and weibo Motan in Java, but with more features, Scale easily.

- [Dubbo ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/apache/incubator-dubbo): Apache Dubbo (incubating) is a high-performance, java based, open source RPC framework.

- [OCTO ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/Meituan-Dianping/octo-rpc): 微服务通信框架及治理平台 OCTO 作为美团基础架构设施的重要组成部分，目前已广泛应用于公司技术线，稳定承载上万应用、日均支撑千亿级的调用。

- [2018-Tars ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/TarsCloud/Tars): Tars is a high-performance RPC framework based on name service and Tars protocol, also integrated administration platform, and implemented hosting-service via flexible schedule.

- [2018-ServiceComb ![code](https://ng-tech.icu/assets/code.svg)](http://servicecomb.apache.org/cn/): 开箱即用、高性能、兼容流行生态、支持多语言的一站式开源微服务解决方案。

- [Zebra ![code](https://ng-tech.icu/assets/code.svg)](https://gitee.com/gszebra/zebra): Zebra 是国信证券的微服务框架，是国信证券在微服务架构和 CNCF 上的实践，让有相同目标方向的尽量少走弯路。

- [2022~trpc ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/trpc/trpc)](https://github.com/trpc/trpc): tRPC allows you to easily build & consume fully typesafe APIs without schemas or code generation.

### Dubbo

- [dubbogo ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/AlexStocks/dubbogo): a golang micro-service framework compatible with alibaba dubbo.

- [dubbo2.js ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/dubbo/dubbo2.js)：Node.js native dubbo client on hessian.

## Data Formatter

- [gron ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/tomnomnom/gron): gron transforms JSON into discrete assignments to make it easier to grep for what you want and see the absolute 'path' to it.

## Distributed Tracing | 分布式追踪

- [Zipkin ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/openzipkin/zipkin): Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in microservice architectures. It manages both the collection and lookup of this data. Zipkin’s design is based on the Google Dapper paper.

- [Pinpoint ![code](https://ng-tech.icu/assets/code.svg)](http://naver.github.io/pinpoint/): Pinpoint is an APM (Application Performance Management) tool for large-scale distributed systems written in Java / PHP.

# Service Coordination

## Configuration

- [Apollo ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/ctripcorp/apollo): Apollo(阿波罗)是携程框架部门研发的分布式配置中心，能够集中化管理应用不同环境、不同集群的配置，配置修改后能够实时推送到应用端，并且具备规范的权限、流程治理等特性，适用于微服务配置管理场景。

- [Hawk ![code](https://ng-tech.icu/assets/code.svg)](https://parg.co/Uv4): Hawk 基于 ETCD 打造，主要解决把开发人员从复杂的业务流程和烦琐的配置中解脱出来，让开发人员只关注自己的业务代码，把运维、配置这些剥离出去。同时降低服务部署、发布过程中的风险。

- [2018-Nacos ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/alibaba/nacos): an easy-to-use dynamic service discovery, configuration and service management platform for building cloud native applications(更易于构建云原生应用的动态服务发现、配置管理和服务管理平台)
