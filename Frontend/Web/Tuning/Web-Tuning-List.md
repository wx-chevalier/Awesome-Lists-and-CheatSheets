[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wx-chevalier/Awesome-Lists)

# Web Performance List

前端优化的根本目的是为了有一个更好地用户体验的同时尽可能减少后端负载压力。即保证更少的加载时间、更快的首屏渲染、更流畅的用户交互。

# Overview | 概述

- [2017-Production Web Apps Performance Study Q4/16 - Q1/17](https://github.com/GoogleChrome/discovery/issues/1)

- [2017-Frontend Performance Check-list For Production](https://parg.co/bLP): In this article I will share with you my chick-list that I use to optimize my web pages after development. So feel free to leave a comment if you think I miss something.

* [2017-The State of the Web](https://medium.com/@fox/talk-the-state-of-the-web-3e12f8e413b3): A guide to impactful performance improvements.

- [400% 飞跃：Web 页面加载速度优化实战](https://parg.co/Utq)

- [移动端 HTML5 页面开发备忘录](http://zerosoul.github.io/2016/11/15/h5-memo/)

- [钉钉的 H5 性能优化方案](http://mp.weixin.qq.com/s/r-D4S94XOo22PQM_wZlrig)

- [解耦 ---Hybrid H5 跨平台性思考 ](http://mp.weixin.qq.com/s?__biz=MzA3NTYzODYzMg==&mid=2653577297&idx=3&sn=96c9ec407e937132595c29b0584cdd5c&scene=4#wechat_redirect)

- [Mobile JavaScript Apps: The Problem with the Mobile Web](http://thefullstack.xyz/category/the-mobile-web/)

- [Speed Matters: Designing for Mobile Performance](https://parg.co/bDR)

* [2017-Tracking CPU with Long Tasks API](https://calendar.perfplanet.com/2017/tracking-cpu-with-long-tasks-api/): the old bottleneck for web performance used to be the network. But the new bottleneck for web performance is the CPU, and particularly the main thread.

- [2018-Front-End Performance Checklist](https://github.com/thedaviddias/Front-End-Performance-Checklist): The only Front-End Performance Checklist that runs faster than the others

- [Front-End Checklist](https://github.com/thedaviddias/Front-End-Checklist#performance-1): The Front-End Checklist is an exhaustive list of all elements you need to have / to test before launching your site / HTML page to production.

## Case Study | 案例分析

- [美团境外业务性能优化实践](https://zhuanlan.zhihu.com/p/33179166): 本文根据第 16 期美团点评技术线上沙龙 OnLine 演讲内容整理而成。

- [2018-蚂蚁金服如何把前端性能监控做到极致?](https://mp.weixin.qq.com/s/pqFhhb5u6w7gmUutilH5xQ): 将分享如何通过 Performance 相关的 API 准确的采集用户性能数据，并如何通过大数据计算加工最终产出用户性能分析产品，以及如何通过性能数据纵向衡量产品性能、发现性能瓶颈。

- [2017- 美团点评收银台前端可用性保障实践](https://parg.co/ba2)：本文主要讨论的是前端可用性相关话题，以在美团点评移动端网页收银台的实践为例，讲解收银台前端是如何保障可用性的。

## Resource

- [小胡子哥的性能专栏](https://github.com/barretlee√/performance-column/issues)

# Benchmark | 性能评测与监控

- [SiteSpeed](https://www.sitespeed.io/): itespeed.io is a set of Open Source tools that helps make your web pages faster.

* [stacks-cli #Project#](https://github.com/WeiChiaChang/stacks-cli): Check website stack from the terminal.

* [WebPagetest #Project#](https://github.com/WPO-Foundation/webpagetest)

## Page Metric | 页面评测

- [Leveraging the Performance Metrics that Most Affect User Experience](https://parg.co/b96): But as you try to answer the question: how fast is my app?, you'll realize that fast is a vague term. What exactly do we mean when we say fast? In what context? And fast for whom?

- [2014-FEX-7 天打造前端性能监控系统](http://6me.us/3EO4ch)

- [2015- 使用 HMTL5 API 监控前端性能](http://www.infoq.com/cn/articles/html5-performance-api-monitoring): 用户计时 API 可以在网页应用中测量两个预定义标记之间的性能。开发者仅仅需要分别定义测量的开始和结束标记。

- [前端性能 —— 监控起步](http://www.07net01.com/2016/09/1653517.html)

- [2018-使用 RAIL 模型评估性能](https://developers.google.com/web/fundamentals/performance/rail?hl=zh-cn): RAIL 是一种以用户为中心的性能模型。每个网络应用均具有与其生命周期有关的四个不同方面，且这些方面以不同的方式影响着性能。

## API Metric | 接口性能评测

- [Locust](https://locust.io/): Define user behaviour with Python code, and swarm your system with millions of simultaneous users.

- [wrk](https://github.com/wg/wrk): wrk is a modern HTTP benchmarking tool capable of generating significant load when run on a single multi-core CPU.

- [Apache JMeter](https://jmeter.apache.org/): The Apache JMeter™ application is open source software, a 100% pure Java application designed to load test functional behavior and measure performance.

## Code Coverage | 代码覆盖率

- [Using the Chrome devtools new code coverage feature](https://blog.logrocket.com/using-the-chrome-devtools-new-code-coverage-feature-ca96c3dddcaf): This is an exciting feature that is useful both when working with JavaScript and CSS, so I thought I’d do a quick demo and explore how it can be helpful.
