# Service Gateway List

# Overview

- [谈 API 网关的背景、架构以及落地方案](http://www.infoq.com/cn/news/2016/07/API-background-architecture-floo)

- [一个简单可参考的 API 网关架构设计](https://parg.co/8KN): 网关一词较早出现在网络设备里面，比如两个相互独立的局域网段之间通过路由器或者桥接设备进行通信，这中间的路由或者桥接设备我们称之为网关。

- [2018~MicroService Proxy Gateway Solutions](https://gist.github.com/StevenACoffman/acf1133da6c5ff5226c0f6eb8fbd8132): Kong, Traefik, Caddy, Linkerd, Fabio, Vulcand, and Netflix Zuul seem to be the most common in microservice proxy/gateway solutions. Kubernetes Ingress is often a simple Ngnix, which is difficult to separate the popularity from other things.

# Rate Limiting

- [API 返回结果设计经验与总结](http://tutuge.me/2016/05/02/design-json-api-respoense/)

- [API 调用次数限制实现](https://zhuanlan.zhihu.com/p/20872901)

# Long Connection

- [2019~Golang 实现单机百万长连接服务，美图的三年优化经验](https://mp.weixin.qq.com/s/xavjsa4NzRiVRxyMhifCDg): 本文将从多个角度介绍长连接服务在内存优化路上的探索，首先会先通过介绍当前服务的架构模型，Go 语言的内存管理，让大家清晰地了解我们内存优化的方向和关注的重要数据。
