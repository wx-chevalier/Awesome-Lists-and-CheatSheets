# System List

本文是对于服务端应用程序开发与系统架构领域中高可用系统搭建相关资料进行整理，更多的其他相关优秀资料可以参考笔者的 [AwesomeList](http://6me.us/qvPQ) 系列，其他的还包括[追求技术之上的进阶阅读学习索引](https://zhuanlan.zhihu.com/p/25642783)、[机器学习、深度学习与自然语言处理领域推荐的书籍列表](https://zhuanlan.zhihu.com/p/25612011)等等。随着公司业务的发展与终端用户的增加，保证系统的高可用性也日渐成为团队考虑的重要因素。

- [Event sourcing vs CRUD](https://parg.co/U1V): In many cases event sourcing is combined with domain-driven design (DDD) and the design pattern CQRS.

- [如何在云平台构建大规模分布式系统](http://www.infoq.com/cn/articles/build-a-large-scale-distributed-system)

- [LinkedIn 架构这十年](http://colobu.com/2015/07/24/brief-history-scaling-linkedin/)

- [构建能够每秒处理 3 百万请求的高性能 Web 集群系列文章](http://blog.jobbole.com/87509/)

- [根据 PV 计算带宽及根据 PV 算并发](http://www.tuicool.com/articles/aqi6Znr)

- [C1000K-Servers #Project#](https://github.com/smallnest/C1000K-Servers): High performance websocket servers implemented by Spray-can, Netty, undertow, jetty, Vert.x, Grizzly, node.js and Go. It supports 1,200,000 active websocket connections.

# Overview

- [2014-Software Architecture #Series#](https://cubox.pro/c/yS7SUx): Software architecture and software design are two aspects of the same topic. Both are about how software is structured in order to perform its tasks. The term "software architecture" typically refers to the bigger structures of a software system, whereas "software design" typically refers to the smaller structures.

## Case Study

- [2018-小团队的微服务之路](https://mp.weixin.qq.com/s/_EpgKGKukSZ50Labb9vfag): 公司的背景是提供 SaaS 服务，对于大客户也会有定制开发以及私有化部署。经过 2 年不到的时间，技术架构经历了从单体到微服务再到容器化的过程。

- [2019-Operating a Large, Distributed System in a Reliable Way: Practices I Learned](https://blog.pragmaticengineer.com/operating-a-high-scale-distributed-system/#slos-slas-reporting-on-them): This post is the collection of the practices I've found useful to reliably operate a large system at Uber, while working here.

# Resource

## Book

- [2016-架构师特刊-微服务与 DevOps 技术内参 #Book#](http://q.infoqstatic.com/ppt/Microservice&DevOps.pdf)

- [2016-Production Ready Microservices #Book#](https://parg.co/U6C): Susan Fowler presents a set of microservice standards in depth, drawing from her experience standardizing over a thousand microservices at Uber. You’ll learn how to design microservices that are stable, reliable, scalable, fault tolerant, performant, monitored, documented, and prepared for any catastrophe.

- [2017-Microservice Patterns #Book#](https://microservices.io/patterns/index.html): A pattern language for microservices

- [2017-The System Design Primer #Book#](https://github.com/donnemartin/system-design-primer): Learn how to design large scale systems. Prep for the system design interview.

## Collection

- [2018-从 Spring Cloud 开始，聊聊微服务架构实践之路](http://mp.weixin.qq.com/s/DZQU4s9YNx4fXsfwu5whIg): 平台的技术架构也完成了从传统的单体应用到微服务化的演进。

- [2017-The System Design Primer #Collection#](https://github.com/donnemartin/system-design-primer): Learn how to design large-scale systems. Prep for the system design interview. Includes Anki flashcards.

- [互联网公司经典技术架构 #Collection#](https://github.com/davideuler/architecture.of.internet-product#): 互联网公司技术架构，微信/淘宝/腾讯/阿里/美团点评/百度/微博/Google/Facebook/Amazon/eBay 的架构。

- [2018-Awesome Scalability, Availability, and Stability Back-end Design Patterns #Collection#](https://github.com/binhnguyennus/awesome-scalability): A curated list of selected readings to illustrate Scalability, Availability, and Stability Design Patterns in Back-end Development.

- [2018-The Architecture of Open Source Applications #Collection#](https://cubox.pro/c/V0ffbT): Our goal is to change that. In these two books, the authors of four dozen open source applications explain how their software is structured, and why. What are each program's major components? How do they interact? And what did their builders learn during their development? In answering these questions, the contributors to these books provide unique insights into how they think.

- [2020-Clone Wars #Collection#](https://github.com/GorvGoyl/Clone-Wars): 70+ open-source clones of popular sites like Airbnb, Amazon, Instagram, Netflix, Tiktok, Spotify, Whatsapp, Youtube etc. See source code, demo links, tech stack, github stars.

- [2020-Awesome CTO #Collection#](https://github.com/kuchin/awesome-cto): A curated and opinionated list of resources for Chief Technology Officers and VP R&D, with the emphasis on startups and hyper-growth companies.

## Video

## Series

- [2017-Re：从 0 开始的微服务架构 #Series#](http://www.infoq.com/cn/minibooks/microservice--from-zero): 系列文章就是将以上过程给大家做个分享，不深究概念，不深入细节，只希望能够对微服务架构能够有一个相对全面的认识，从而能够帮助大家成功落地微服务架构。
