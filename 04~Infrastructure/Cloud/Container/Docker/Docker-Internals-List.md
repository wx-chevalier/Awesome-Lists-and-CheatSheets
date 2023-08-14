# Docker Internals List | Docker 内部原理资料索引

# Overview

- [2018-Docker 底层技术](https://www.jianshu.com/p/7a1ce51a0eba): Docker 容器技术已经发展了好些年，在很多项目都有应用，线上运行也很稳定。整理了部分 Docker 的学习笔记以及新版本特性，对 Docker 感兴趣的同学可以看看，之前整理过的 Linux namespace 可以见之前的博文。

- [深入 Docker：容器和镜像](http://segmentfault.com/a/1190000002766882)

- [Docker 核心技术与实现原理](https://draveness.me/docker): 作为在生产环境中广泛应用的产品，Docker 有着非常成熟的社区以及大量的使用者，代码库中的内容也变得非常庞大。

- [2021~万字长文：彻底搞懂容器镜像构建](https://zhuanlan.zhihu.com/p/357107501): 我将在这篇文章中深入 Docker 的源码，与你聊聊镜像构建的原理。

# cgroup

- [2017-Docker 容器基础技术：linux cgroup 简介](http://cizixs.com/2017/08/25/linux-cgroup): Linux cgroups 的全称是 Linux Control Groups，它是 Linux 内核的特性，主要作用是限制、记录和隔离进程组（process groups）使用的物理资源（cpu、memory、IO 等）。

# 网络

- [2017-理解 Docker 容器网络之 Linux Network Namespace](https://blog.csdn.net/xuguokun1986/article/details/54411394): 在本文中我们将尝试理解 Linux Network Namespace 及相关 Linux 内核网络设备的概念，并手工模拟 Docker 容器网络模型的部分实现，包括单机容器网络中的容器与主机连通、容器。

- [2019~浅聊几种主流 Docker 网络的实现原理](https://mp.weixin.qq.com/s/Jdxct8qHrBUtkUq-hnxSRw): 本文接下来将详细介绍目前主流容器网络的实现原理。

- [2020~Container networking is simple](https://iximiuz.com/en/posts/container-networking-is-simple/): Luckily, we've been looking under the hood of the containerization technology for quite some time already and even managed to uncover that containers are just isolated and restricted Linux processes, that images aren't really needed to run containers, and on the contrary - to build an image we need to run some containers.

# 存储

- [2015-Deep dive into Docker storage drivers](https://jpetazzo.github.io/assets/2015-03-03-not-so-deep-dive-into-docker-storage-drivers.html)

- [2015-深入分析 Docker 镜像原理](https://www.csdn.net/article/2015-08-21/2825511): 分享内容包含两个部分：1.Docker 镜像的基本知识；2.Dockerfile、Docker 镜像与 Docker 容器的关系。

- [2018-What's in a Docker image?](https://cameronlonsdale.com/2018/11/26/whats-in-a-docker-image/): Not only do I want to give you the answer, but I want to show you how I got there.
