# Docker Configuration List

# System

- [2018~使用 docker 对容器资源进行限制](http://cizixs.com/2017/08/04/docker-resources-limit): 这篇文章就介绍如何使用 docker 来限制 CPU、内存和 IO，以及对应的 cgroups 文件。

# Docker Storage

- [2016~Docker : Storage Patterns for Persistence](https://parg.co/Ur8): We’ll go over several variants when it comes down to data persistence.

- [2017~Managing Persistence for Docker Containers](https://thenewstack.io/methods-dealing-container-storage/)

- [copying-data-between-docker-containers](https://medium.com/@gchudnov/copying-data-between-docker-containers-26890935da3f)

- [docker-indepth-volumes](http://container42.com/2014/11/03/docker-indepth-volumes/)

- [深入理解 Docker Volume](http://dockone.io/article/128)

# Network

- [Docker 网络部分执行流分析(Libnetwork 源码解读)](http://dockone.io/article/1255)

- [Docker Networking: Reborn](http://www.container42.com/2015/10/30/docker-networking-reborn/)

- [2018~Demystifying Docker overlay networking](http://blog.nigelpoulton.com/demystifying-docker-overlay-networking/): We’ll explain the theory behind how it works.

# Dockerfile

- [2018~An Exhaustive Guide to Writing Dockerfiles for Node.js Web Apps](https://parg.co/UyX): This post is filled with examples ranging from a simple Dockerfile to multistage production builds for Node.js web apps.

- [高效编写 Dockerfile 的几条准则](https://www.jianshu.com/p/a9d08ba3d979?from=groupmessage&isappinstalled=0): 写 Dockerfile 也像写代码一样，一份精心设计、Clean Code 的 Dockerfile 能在提高可读性的同时也大大提升 Docker 的使用效率。

# Registry

- [private-docker-registry-ssl](https://github.com/fzuleta/private-docker-registry-ssl): Private Docker registry protected with Let's Encrypt SSL

# Application

- [2017~Create lean Node.js image with Docker multi-stage build](https://codefresh.io/blog/node_docker_multistage/)

- [3 tricks for mastering Docker with Python](https://hackernoon.com/3-tricks-for-mastering-docker-with-python-99876412348d?source=reading_list---------6-1---------)

# Engineering Practices

## Security

- [Docker Security Best Practices](https://www.sqreen.io/resources/docker-security-best-practices): This Docker Security Cheat Sheet will walk you through five actions to protect your Docker containers and infrastructure. Improve your Docker security today.

- [Docker Security CheatSheet](https://parg.co/d6b): The following tips should help you to secure a container based system.

- [2019~Docker 容器安全的“终极武器” AIM](https://mp.weixin.qq.com/s/i9lMWgST6ZdRGxau5hGt9g): 我们需要关注 Docker 中的安全问题吗？这个得具体分析。Docker 拥有相当强大的安全保障能力，因此如果大家只使用官方 Docker 镜像而且不需要进行机器间通信，就完全没必要为安全而担心。

## Optimization

- [2017~Tips to Reduce Docker Image Sizes](https://parg.co/beS): Docker images can easily get to 2–3GB. Here’s some tips that can help reduce their sizes.

- [Dockerfile 最佳实践](http://dockone.io/article/132)

- [Dockerfile 优化浅谈](http://dockone.io/article/255)

- [记一次 docker 问题定位](https://parg.co/lIW): 性能测试发现业务进程运行在容器中比业务进程运行在宿主机上吞吐量下降了 100 倍，这让周一显得更加阴暗。
