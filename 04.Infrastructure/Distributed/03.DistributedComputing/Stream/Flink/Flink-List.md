# Flink Learning & Practices List

# Overview

- [Apache Flink：特性、概念、组件栈、架构及原理分析](http://shiyanjun.cn/archives/1508.html)

- [Flink 原理与实现：架构和拓扑概览](https://yq.aliyun.com/articles/57816?spm=5176.100240.searchblog.15.918ieV)

## ChangeLog

- [2019-修改代码 150 万行！Apache Flink 1.9.0 做了这些重大修改！](https://mp.weixin.qq.com/s/Gj76cO5VGQ76R7d7Kc--0Q): 8 月 22 日，Apache Flink 1.9.0 正式发布。早在今年 1 月，阿里便宣布将内部过去几年打磨的大数据处理引擎 Blink 进行开源并向 Apache Flink 贡献代码。此次版本在结构上有重大变更，修改代码达 150 万行，接下来，我们一起梳理 Flink 1.9.0 中非常值得关注的重要功能与特性。

## Case Study | 案例分析

- [2019-滴滴实时计算发展之路及平台架构实践](https://mp.weixin.qq.com/s/NGeukit_TpwD4_opIZRb-Q): 滴滴的核心业务是一个实时在线服务，因此具有丰富的实时数据和实时计算场景。本文将介绍滴滴实时计算发展之路以及平台架构实践。

- [2019-日处理数据量超 10 亿：友信金服基于 Flink 构建实时用户画像系统的实践](https://mp.weixin.qq.com/s/ptNHzhMu50pAOUMzTxaGfA): 友信金服用户画像项目正是以此为背景成立，旨在实现“数据驱动业务与运营”的集团战略。目前该系统支持日处理数据量超 10 亿，接入上百种合规数据源。

# Resource

## Books

- [2021-Apache Flink SQL Cookbook ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/ververica/flink-sql-cookbook)](https://github.com/ververica/flink-sql-cookbook): The Apache Flink SQL Cookbook is a curated collection of examples, patterns, and use cases of Apache Flink SQL. Many of the recipes are completely self-contained and can be run in Ververica Platform as is.

## Series

- [Madhukara Phatak: 某个大数据咨询师的博客](http://blog.madhukaraphatak.com/)

- [wuchong Jark's Bloh 一系列关于 Flink 的博客](http://wuchong.me/archives/)

- [Flink 系列博客 #Series#](https://mp.weixin.qq.com/s/ok-YwuVbwAVtJz7hUCiZxg): Flink 灵魂两百问，这谁顶得住？

- [2019-Flink Learning #Series#](https://github.com/zhisheng17/flink-learning): 含 Flink 入门、概念、原理、实战、性能调优、源码解析等内容。涉及 Flink Connector、Metrics、Library、DataStream API、Table API & SQL 等内容的学习案例。

- [2020-Flink Tutorial #Series#](https://github.com/confucianzuoyuan/flink-tutorial): 大家好！这是尚硅谷出品的 Flink 教程。包含理论部分和实践部分。深入讲解 了 Flink 的内部原理以及各种 API，包括了最新的 Table API 和 Flink SQL。本教程有尚硅谷大数据组研发。

## Confs

- [Flink Forward China 2018 Slides](https://github.com/flink-china/flink-forward-china-2018)

## Courses

- [2020-Apache Flink 入门 🎥](https://developer.aliyun.com/learning/course/58?spm=a2ctu.24462426.0.0.21a45879PJFgMu): 本课程由阿里云开发者学堂与 Apache Flink 社区共同出品，Apache Flink PMC 及 Committer 精心打磨的 Flink 零基础入门教程。课程内容先从基础理论入手，全盘解析 Apache Flink 底层架构、核心功能模块、社区生态，帮您建立对 Flink 应用场景与功能实现的系统认知。同时，还有 Apache Flink 技术专家手把手进行实操演示，8 天课程，助您完成从理论到实操的跨越，轻松收获 Flink 生产环境开发技能。

# Tutorial

- [从 0 到 1 学习 Flink #Series#](https://mp.weixin.qq.com/s/WrDwd1Ca1jMch6ERCpb_FA): Flink 是一种流式计算框架，我自己整理了些 Flink 的学习资料，目前已经全部放到微信公众号了。

- [2018-Apache Flink Training](https://training.da-platform.com/): This training teaches how to implement scalable data analysis programs with Apache Flink 1.6.0.

- [2019-基于 Flink 实现的商品实时推荐系统](https://mp.weixin.qq.com/s/pF8mr4AeUwWWpGEAKmJW2w): 近期我在 GitHub 观察到一个不错的 Flink 项目，然后也和作者交流了下，于是在这里做一个分享。
  - [flink-recommandSystem-demo](https://github.com/will-che/flink-recommandSystem-demo)

# Internals | 内部原理

- [2016-Flink 原理与实现：理解 Flink 中的计算资源](http://wuchong.me/blog/2016/05/09/flink-internals-understanding-execution-resources/)

- [2018-Flink 原理与实现：内存管理](https://yq.aliyun.com/articles/57815): 本文将会讨论 Flink 是如何解决上面的问题的，主要内容包括内存管理、定制的序列化工具、缓存友好的数据结构和算法、堆外内存、JIT 编译优化等。
