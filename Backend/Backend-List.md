# Backend List

本文是对于服务端应用程序开发与系统架构领域中高可用系统搭建相关资料进行整理，更多的其他相关优秀资料可以参考笔者的 [AwesomeList](http://6me.us/qvPQ) 系列，其他的还包括[追求技术之上的进阶阅读学习索引](https://zhuanlan.zhihu.com/p/25642783) 、 [机器学习、深度学习与自然语言处理领域推荐的书籍列表](https://zhuanlan.zhihu.com/p/25612011)等等。随着公司业务的发展与终端用户的增加，保证系统的高可用性也日渐成为团队考虑的重要因素。

- [Event sourcing vs CRUD](https://parg.co/U1V): In many cases event sourcing is combined with domain-driven design (DDD) and the design pattern CQRS.

- [如何在云平台构建大规模分布式系统](http://www.infoq.com/cn/articles/build-a-large-scale-distributed-system)

- [LinkedIn 架构这十年](http://colobu.com/2015/07/24/brief-history-scaling-linkedin/)

- [构建能够每秒处理 3 百万请求的高性能 Web 集群系列文章](http://blog.jobbole.com/87509/)

- [根据 PV 计算带宽及根据 PV 算并发](http://www.tuicool.com/articles/aqi6Znr)

- [C1000K-Servers #Project#](https://github.com/smallnest/C1000K-Servers): High performance websocket servers implemented by Spray-can, Netty, undertow, jetty, Vert.x, Grizzly, node.js and Go. It supports 1,200,000 active websocket connections.

# Overview 

- [2015-Practical Scalability Analysis With The Universal Scalability Law #Book#](https://parg.co/bNA): I wrote this book to help you understand the simple, but profoundly powerful, truths about scalability.

- [2016- 究竟啥才是互联网架构 “ 高可用 ”](http://6me.us/Fz25N7)

- [2017-The System Design Primer](https://github.com/donnemartin/system-design-primer): Learn how to design large scale systems. Prep for the system design interview.

- [2017- 大话程序猿眼里的高并发](https://blog.thankbabe.com/2016/04/01/high-concurrency/)：高并发是指在同一个时间点，有很多用户同时的访问 URL 地址，比如：淘宝的双 11，双 12，就会产生高并发 , 如贴吧的爆吧，就是恶意的高并发请求，也就是 DDOS 攻击，再屌丝点的说法就像玩撸啊撸被 ADC 暴击了一样 , 那伤害你懂得 ( 如果你看懂了，这个说法说明是正在奔向人生巅峰的屌丝。

- [2017- 微信高并发资金交易系统设计方案 —— 百亿红包背后的技术支撑](http://mp.weixin.qq.com/s/suBAJrP6uN2kFgHtGz16mw)：本文将为读者介绍百亿级别红包背后的系统高并发设计方案，包括微信红包的两大业务特点、微信红包系统的技术难点、解决高并发问题通常使用的方案，以及微信红包系统的高并发解决方案。

- [2017- 如何提升 Web 后端性能？我的 4 个实践和总结](http://mp.weixin.qq.com/s/KsXS5f-1-217CY5R88qOHQ)：随着互联网的不断发展，日常生活中越来越多的需求通过网络来实现，从衣食住行到金融教育，从口袋到身份，人们无时无刻不依赖着网络，而且越来越多的人通过网络来完成自己的需求。作为直接面对来自客户请求的 Web 服务端，无疑是要同时承受更多的请求，并为用户提供更好的体验。这个时候 Web 端的性能常常会成为业务发展的瓶颈，提升性能刻不容缓。本文作者在开发过程中总结了一些提升 Web 服务端性能的经验，与大家分享。

- [2017- 去哪儿 - 超时，重试，熔断，限流](http://mp.weixin.qq.com/s/wIQIv4TAHRIqR_X9iSz3Hw)

- [乐视秒杀：每秒十万笔交易的数据架构解读 ](http://www.uml.org.cn/sjjm/201611184.asp)

- [晓明 美团点评技术团队 常见性能优化策略的总结](http://tech.meituan.com/performance_tunning.html)

# Case Study

## 架构衍化

- [2018-小团队的微服务之路](https://mp.weixin.qq.com/s/_EpgKGKukSZ50Labb9vfag): 公司的背景是提供SaaS服务，对于大客户也会有定制开发以及私有化部署。经过2年不到的时间，技术架构经历了从单体到微服务再到容器化的过程。

