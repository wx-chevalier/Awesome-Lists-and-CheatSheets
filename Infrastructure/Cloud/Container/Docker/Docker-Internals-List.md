# Docker Internals List | Docker 内部原理资料索引

# Overview

- [2018-Docker 底层技术](https://www.jianshu.com/p/7a1ce51a0eba): Docker 容器技术已经发展了好些年，在很多项目都有应用，线上运行也很稳定。整理了部分 Docker 的学习笔记以及新版本特性，对 Docker 感兴趣的同学可以看看，之前整理过的 Linux namespace 可以见之前的博文。

- [深入 Docker：容器和镜像](http://segmentfault.com/a/1190000002766882)

- [Docker 核心技术与实现原理](https://draveness.me/docker): 作为在生产环境中广泛应用的产品，Docker 有着非常成熟的社区以及大量的使用者，代码库中的内容也变得非常庞大。

# cgroup

- [2017-Docker 容器基础技术：linux cgroup 简介](http://cizixs.com/2017/08/25/linux-cgroup): Linux cgroups 的全称是 Linux Control Groups，它是 Linux 内核的特性，主要作用是限制、记录和隔离进程组（process groups）使用的物理资源（cpu、memory、IO 等）。

# Network

- [2017-理解 Docker 容器网络之 Linux Network Namespace](https://blog.csdn.net/xuguokun1986/article/details/54411394): 在本文中我们将尝试理解 Linux Network Namespace 及相关 Linux 内核网络设备的概念，并手工模拟 Docker 容器网络模型的部分实现，包括单机容器网络中的容器与主机连通、容器。

- [2019-浅聊几种主流 Docker 网络的实现原理](https://mp.weixin.qq.com/s/Jdxct8qHrBUtkUq-hnxSRw): 本文接下来将详细介绍目前主流容器网络的实现原理。

# Storage

- [2015-Deep dive into Docker storage drivers](https://jpetazzo.github.io/assets/2015-03-03-not-so-deep-dive-into-docker-storage-drivers.html)

- [2015-深入分析 Docker 镜像原理](https://www.csdn.net/article/2015-08-21/2825511): 分享内容包含两个部分：1.Docker 镜像的基本知识；2.Dockerfile、Docker 镜像与 Docker 容器的关系。

- [2018-What's in a Docker image?](https://cameronlonsdale.com/2018/11/26/whats-in-a-docker-image/): Not only do I want to give you the answer, but I want to show you how I got there.

# DIY

- [2015-Tiny Docker in Docker #Project#](https://github.com/rancher/docker-from-scratch): Docker-in-Docker image based off of the empty image scratch. Only the bare minimum required files are included to make Docker run. This image weighs in around 25MB expanded.

- [2015-Docker 基础技术 #Series#](https://coolshell.cn/articles/17010.html): 我会用几篇文章来把这些技术给大家做个介绍，希望通过这些文章大家可以自己打造一个山寨版的 docker。

- [2016-Docker Internals](http://docker-saigon.github.io/post/Docker-Internals/): A Deep Dive Into Docker For Engineers Interested In The Gritty Details.

- [2017-rubber-docker #Project#](https://github.com/Fewbytes/rubber-docker): A workshop on Linux containers: Rebuild Docker from Scratch

- [2018-手把手教你写 Docker](https://parg.co/UvM): 模拟 Docker 实现一个简单的容器不到 200 行代码(包括空行、注释、异常处理)。
