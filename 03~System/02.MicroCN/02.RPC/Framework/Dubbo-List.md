# Dubbo List

- [2019~Dubbo 实现原理与源码解析系列 #Series#](http://www.iocoder.cn/Dubbo/good-collection/?title)

# Overview

## Case Study

- [2019~聊聊携程升级 Dubbo 的踩坑历程](https://mp.weixin.qq.com/s/zZ5MKNeRly6UXa8nCKpEEQ): 携程从 2017 年 11 月左右开始调研，真正落地是在 2018 年 4 月发布的 CDubbo 0.1.1 版本。在携程内部，我们管他叫 CDubbo，言下之意就是携程版的 Dubbo。考虑到以后升级的问题，CDubbo SDK 是对 Dubbo SDK 的扩展和包装，保留了 Dubbo 所有的扩展和配置能力。

# Kubernetes

- [2019~Dubbo 应用迁移到 Docker 的问题](https://blog.51cto.com/nxlhero/2447505): Dubbo 是阿里开源的一套服务治理与 rpc 框架，服务的提供者通过 zookeeper 把自己的服务发布上去，然后服务调用方通过 zk 获取服务的 ip 和端口，dubbo 客户端通过自己的软负载功能自动选择服务提供者并调用，整个过程牵涉到的三方关系如下图所示。
