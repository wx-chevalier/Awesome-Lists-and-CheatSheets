![](https://img.readitlater.com/i/cdn-images-1.medium.com/max/800/1*LBocICeBuP3FSLPMBLA04g/RS/w1408.png?&ssl=1)

# Message Oriented Middleware List | 消息中间件资料索引

# Overview

- [2020-云原生时代消息中间件的演进路线](https://mp.weixin.qq.com/s/b3YGm8uMuOZNRhZdA7egSQ): 本文整理自作者于 2020 年云原生微服务大会上的分享《云原生时代的消息中间件演进》，主要探讨了传统的消息中间件如何持续进化为云原生的消息服务。

# Resource

## Books

- [2017-Understanding Message Brokers》📚](https://learning.oreilly.com/library/view/understanding-message-brokers/9781492049296/): Messaging is one of the more poorly understood areas of IT; most developers and architects have only a passing familiarity with how broker-based messaging technologies work. This practical report not only helps you get up to speed on the essentials of messaging, but also compares two of today’s most popular messaging technologies—Apache ActiveMQ and Apache Kafka.

## Comparison

- [2016-消息队列的流派之争](https://parg.co/faL): 这篇文章的标题很难起，网上一翻全是各种 MQ 的性能比较，很容易让人以为我也是这么“粗俗”的人（o(╯□╰)o）。我这篇文章想要表达的是——它们根本不是一个东西，有毛的性能好比较？

- [2017-消息队列的对比调研](http://www.jianshu.com/p/f056a74d77a4)：我们发现 Redis 的作者出了一个新的消息队列系统 Disque，我做了一点调研来决定我们使用哪种消息队列，主要对比了 Disque、Kafka 和 RocketMQ。

- [2017-Kafka & Redis Streams](https://parg.co/UsQ): Let’s talk about queue design.

## Case Study

- [2015-携程异步消息系统实践](http://blog.qiniu.com/archives/4791): 今天会跟大家分享一下我们在携程，现在应该是正在推广的一个新的消息系统，主要会偏重于讲一些架构和实现方面的内容。目前我在携程大概一年多都在做新的消息系统 Hermes。

- [2016-阿里巴巴分布式消息系统的演进之路](https://parg.co/fai): 阿里中间件给客户提供的是一套企业互联网应用架构整体解决方案，里面有很多组件，比如用来做分布式应用编写的应用平台（EDAS），做可无限扩展的分布式数据库（DRDS）和金融级可靠的消息队列服务（AliMQ）。

- [2019-网易云音乐的消息队列改造之路](https://mp.weixin.qq.com/s/F94YPWQzI2_bb9pdDG4mtA): 本文整理自网易云音乐消息队列负责人林德智在近期 Apache Flink&RocketMQ Meetup 上海站的分享。

- [2019-今日头条在消息服务平台和容灾体系建设方面的实践与思考](https://mp.weixin.qq.com/s/qsLNavqAhYv49r6WTAJy9w): 今日头条的业务背景；为什么选择 RocketMQ；RocketMQ 在头条的落地实践；头条的容灾系统建设。

## Spec

- [2019-Cloud Events](https://github.com/cloudevents/spec): CloudEvents is a specification for describing event data in common formats to provide interoperability across services, platforms and systems.

# System Design

- [2016-消息队列设计精要](https://tech.meituan.com/2016/07/01/mq-design.html): 当你需要使用消息队列时，首先需要考虑它的必要性。可以使用 mq 的场景有很多，最常用的几种，是做业务解耦/最终一致性/广播/错峰流控等。反之，如果需要强一致性，关注业务逻辑的处理结果，则 RPC 显得更为合适。

- [2016-设计消息中间件时我关心什么?(解密电商数据一致性与完整性实现)](https://parg.co/fav): 今天主要给大家分享一下消息队列基础组件的设计。

- [2017-Message Queue 的设计和实现](http://mp.weixin.qq.com/s/AgdayVL0pvcwL0amLouu-Q): 终于过完年了，老王也回归了，这周给大家带来的是 Message Queue（业界喜欢简称为 MQ）的设计和实现。

# OpenSource
