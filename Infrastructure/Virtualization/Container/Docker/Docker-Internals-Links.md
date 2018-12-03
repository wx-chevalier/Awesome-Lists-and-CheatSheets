[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wxyyxc1992/Awesome-Links)

# Docker Internals Links | Docker 内部原理资料索引

- [2015-Docker 基础技术 #Series#](https://coolshell.cn/articles/17010.html): 我会用几篇文章来把这些技术给大家做个介绍，希望通过这些文章大家可以自己打造一个山寨版的 docker。

- [2015-Tiny Docker in Docker #Project#](https://github.com/rancher/docker-from-scratch): Docker-in-Docker image based off of the empty image scratch. Only the bare minimum required files are included to make Docker run. This image weighs in around 25MB expanded.

- [2016-Docker Internals](http://docker-saigon.github.io/post/Docker-Internals/): A Deep Dive Into Docker For Engineers Interested In The Gritty Details.

* [2017-rubber-docker #Project#](https://github.com/Fewbytes/rubber-docker): A workshop on Linux containers: Rebuild Docker from Scratch

- [2018-手把手教你写 Docker](https://parg.co/UvM): 模拟 Docker 实现一个简单的容器不到 200 行代码(包括空行、注释、异常处理)。

- [记一次 docker 问题定位](https://parg.co/lIW): 性能测试发现业务进程运行在容器中比业务进程运行在宿主机上吞吐量下降了 100 倍，这让周一显得更加阴暗。

- [2018-Docker 底层技术](https://www.jianshu.com/p/7a1ce51a0eba): Docker 容器技术已经发展了好些年，在很多项目都有应用，线上运行也很稳定。整理了部分 Docker 的学习笔记以及新版本特性，对 Docker 感兴趣的同学可以看看，之前整理过的 Linux namespace 可以见之前的博文。

* [深入 Docker：容器和镜像](http://segmentfault.com/a/1190000002766882)

# cgroup

- [2017-docker 容器基础技术：linux cgroup 简介](http://cizixs.com/2017/08/25/linux-cgroup): Linux cgroups 的全称是 Linux Control Groups，它是 Linux 内核的特性，主要作用是限制、记录和隔离进程组（process groups）使用的物理资源（cpu、memory、IO 等）。

# Network

- [2017-理解 Docker 容器网络之 Linux Network Namespace](https://blog.csdn.net/xuguokun1986/article/details/54411394): 在本文中我们将尝试理解 Linux Network Namespace 及相关 Linux 内核网络设备的概念，并手工模拟 Docker 容器网络模型的部分实现，包括单机容器网络中的容器与主机连通、容器。

# Storage

- [2015-深入分析Docker镜像原理](https://www.csdn.net/article/2015-08-21/2825511): 分享内容包含两个部分：1.Docker镜像的基本知识；2.Dockerfile、Docker镜像与Docker容器的关系。

- [2018-What's in a Docker image?](https://cameronlonsdale.com/2018/11/26/whats-in-a-docker-image/): Not only do I want to give you the answer, but I want to show you how I got there.
