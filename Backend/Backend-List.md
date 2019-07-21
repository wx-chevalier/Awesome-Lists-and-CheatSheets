# Backend List

本文是对于服务端应用程序开发与系统架构领域中高可用系统搭建相关资料进行整理，更多的其他相关优秀资料可以参考笔者的 [AwesomeList](http://6me.us/qvPQ) 系列，其他的还包括[追求技术之上的进阶阅读学习索引](https://zhuanlan.zhihu.com/p/25642783) 、 [机器学习、深度学习与自然语言处理领域推荐的书籍列表](https://zhuanlan.zhihu.com/p/25612011)等等。随着公司业务的发展与终端用户的增加，保证系统的高可用性也日渐成为团队考虑的重要因素。

- [Event sourcing vs CRUD](https://parg.co/U1V): In many cases event sourcing is combined with domain-driven design (DDD) and the design pattern CQRS.

- [如何在云平台构建大规模分布式系统](http://www.infoq.com/cn/articles/build-a-large-scale-distributed-system)

- [LinkedIn 架构这十年](http://colobu.com/2015/07/24/brief-history-scaling-linkedin/)

- [构建能够每秒处理 3 百万请求的高性能 Web 集群系列文章](http://blog.jobbole.com/87509/)

- [根据 PV 计算带宽及根据 PV 算并发](http://www.tuicool.com/articles/aqi6Znr)

- [C1000K-Servers #Project#](https://github.com/smallnest/C1000K-Servers): High performance websocket servers implemented by Spray-can, Netty, undertow, jetty, Vert.x, Grizzly, node.js and Go. It supports 1,200,000 active websocket connections.

# Overview

## Case Study

- [2018-小团队的微服务之路](https://mp.weixin.qq.com/s/_EpgKGKukSZ50Labb9vfag): 公司的背景是提供 SaaS 服务，对于大客户也会有定制开发以及私有化部署。经过 2 年不到的时间，技术架构经历了从单体到微服务再到容器化的过程。

- [2019-Operating a Large, Distributed System in a Reliable Way: Practices I Learned](https://blog.pragmaticengineer.com/operating-a-high-scale-distributed-system/#slos-slas-reporting-on-them): This post is the collection of the practices I've found useful to reliably operate a large system at Uber, while working here.