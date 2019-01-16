[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wxyyxc1992/Awesome-Lists)

# MicorService OpenSource Links | 微服务相关开源框架索引

与编程框架强相关的微服务相关框架应用归纳在本处，其余归纳在 [DevOps OpenSource Links](https://parg.co/A1W)。

# RPC

## RPC Protocol

## RPC Frameworks

- [brpc #Project#](https://github.com/brpc/brpc): Most common RPC framework used throughout Baidu, with 600,000+ instances and 500+ kinds of services, called "baidu-rpc" inside Baidu.

- [gRPC #Project#](https://grpc.io/docs/guides/): gRPC is a modern, open source, high-performance remote procedure call (RPC) framework that can run anywhere. It enables client and server applications to communicate transparently, and makes it easier to build connected systems.

- [Dubbo #Project#](https://github.com/apache/incubator-dubbo): Apache Dubbo (incubating) is a high-performance, java based, open source RPC framework.

## Data Formatter

- [gron #Project#](https://github.com/tomnomnom/gron): gron transforms JSON into discrete assignments to make it easier to grep for what you want and see the absolute 'path' to it.

# Service Gateway

- [2001-HAProxy #Project#](http://www.haproxy.org/): HAProxy is a free, very fast and reliable solution offering high availability, load balancing, and proxying for TCP and HTTP-based applications.

- [2013-Tengine #Project#](https://github.com/alibaba/tengine): A distribution of Nginx with some advanced features.

- [2016-Kong #Project#](https://getkong.org/): The open-source API Gateway and Microservices Management Layer, delivering high performance and reliability.

- [2016-VeryNginx #Project#](https://github.com/alexazhou/VeryNginx): A very powerful and friendly nginx base on lua-nginx-module( openresty ) which provide WAF, Control Panel, and Dashboards.

* [2018-HTTPS Portal #Project#](https://github.com/SteveLTN/https-portal): A fully automated HTTPS server powered by Nginx, Let's Encrypt and Docker.

- [2018-Træfik #Project#](https://github.com/containous/traefik): Træfik (pronounced like traffic) is a modern HTTP reverse proxy and load balancer made to deploy microservices with ease.

## SSO

- [2018-sso #Project#](https://github.com/buzzfeed/sso): Ovingly known as the S.S. Octopus or octoboi — is the authentication and authorization system BuzzFeed developed to provide a secure, single sign-on experience for access to the many internal web apps used by our employees.

## API Automation

- [automatic-api #Project#](https://github.com/dbohdan/automatic-api): The following is a list of tools that automatically expose a REST, GraphQL, or another kind of API for your database.

- [pREST #Project#](https://github.com/prest/prest): Serve a RESTful API from any PostgreSQL database

- [apig #Project#](https://github.com/wantedly/apig): Golang RESTful API Server Generator

## API Management

- [WSO2 #Project#](https://wso2.com/api-management/): WSO2 API Manager is a 100% open source enterprise-class solution that supports API publishing, lifecycle management, application development, access control, rate limiting and analytics in one cleanly integrated system.

- [DOClever #Project#](https://github.com/sx1989827/DOClever): DOClever 是一个商业化开源产品，完全免费。无论你是前端工程师，还是后端工程师，接口永远都是两者交互的桥梁，所以 DOClever 专为中小型团队量身打造，旨在解决接口的管理，测试与数据生成，实现真正的一体化解决方案。

# Service Coordination

## Configuration

- [Apollo #Project#](https://github.com/ctripcorp/apollo): Apollo(阿波罗)是携程框架部门研发的分布式配置中心，能够集中化管理应用不同环境、不同集群的配置，配置修改后能够实时推送到应用端，并且具备规范的权限、流程治理等特性，适用于微服务配置管理场景。

* [Hawk #Project#](https://parg.co/Uv4): Hawk 基于 ETCD 打造，主要解决把开发人员从复杂的业务流程和烦琐的配置中解脱出来，让开发人员只关注自己的业务代码，把运维、配置这些剥离出去。同时降低服务部署、发布过程中的风险。

- [2018-Nacos #Project#](https://github.com/alibaba/nacos): an easy-to-use dynamic service discovery, configuration and service management platform for building cloud native applications(更易于构建云原生应用的动态服务发现、配置管理和服务管理平台)

## Fault Tolerance

- [2015-Hystrix #Project#](https://github.com/Netflix/Hystrix): Hystrix is a latency and fault tolerance library designed to isolate points of access to remote systems, services and 3rd party libraries, stop cascading failure and enable resilience in complex distributed systems where failure is inevitable.

- [Sentinel #Project#](https://github.com/alibaba/Sentinel): A lightweight flow-control library providing high-available protection and monitoring (高可用防护的流量管理框架)

- [2018-Resilience4j #Project#](https://github.com/resilience4j/resilience4j): Resilience4j is a fault tolerance library designed for Java8 and functional programming

## Distributed Transaction | 分布式事务

- [2015-tcc transaction #Project#](https://github.com/changmingxie/tcc-transaction): tcc-transaction 是 TCC 型事务 java 实现。

- [2016-Solar #Project#](https://github.com/prontera/spring-cloud-rest-tcc): 基于 Spring Cloud Netflix 的 TCC 柔性事务和 EDA 事件驱动示例，结合 Spring Cloud Sleuth 进行会话追踪和 Spring Boot Admin 的健康监控，并辅以 Hystrix Dashboard 提供近实时的熔断监控。

- [2017-ByteTCC #Project#](https://github.com/liuyangming/ByteTCC): ByteTCC 是一个兼容 JTA 规范的基于 TCC 机制的分布式事务管理器。

## Distributed Tracing | 分布式追踪

- [Zipkin #Project#](https://github.com/openzipkin/zipkin): Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in microservice architectures. It manages both the collection and lookup of this data. Zipkin’s design is based on the Google Dapper paper.

- [Pinpoint #Project#](http://naver.github.io/pinpoint/): Pinpoint is an APM (Application Performance Management) tool for large-scale distributed systems written in Java / PHP.

# Service Orchestration

- [Istio #Project#](https://istio.io/about/intro.html): Istio is an open platform that provides a uniform way to connect, manage, and secure microservices. Istio supports managing traffic flows between microservices, enforcing access policies, and aggregating telemetry data, all without requiring changes to the microservice code.

- [Service Fabric #Project#](https://github.com/Microsoft/service-fabric): Service Fabric is a distributed systems platform for packaging, deploying, and managing stateless and stateful distributed applications and containers at large scale.

# Service Availability

## Load Balancer

- [glb-director #Project#](https://github.com/github/glb-director): GitHub Load Balancer Director and supporting tooling.
