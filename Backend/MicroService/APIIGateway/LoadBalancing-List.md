# Load Balancing List | 负载均衡

# Overview

- [Nginx/LVS/HAProxy 负载均衡软件的优缺点详解](http://os.51cto.com/art/201407/446441.htm)

- [Google 是如何做负载均衡的？](https://zhuanlan.zhihu.com/p/23826170)

- [分布式系统中负载均衡算法在高可用场景下的分析](http://tech.youzan.com/load-balancing-algorithm/)

- [多种负载均衡算法及其 Java 代码实现](http://www.duzhi.me/article/864.html)

- [负载均衡的那些算法们 ](http://mp.weixin.qq.com/s?__biz=MzA3MDExNzcyNA==&mid=2650392075&idx=1&sn=fca2ebeca258e15f78a43c44bbb6153d&scene=0#wechat_redirect)

# LVS

- [Linux 服务器集群系统](http://www.linuxvirtualserver.org/zh/lvs1.html)

- [LVS+Keepalived 构建高可用负载均衡](http://os.51cto.com/art/201202/317441.htm)

- [Ali-LVS](https://github.com/alibaba/LVS)

- [章文嵩(正明)博士和他背后的负载均衡 (LOAD BANLANCER) 帝国](https://yq.aliyun.com/articles/52752)

# Nginx

- [Nginx 负载均衡系列](http://blog.csdn.net/zhangskd/article/details/50208527)

# Tengine

- [2019-QPS 比 Nginx 提升 60%，阿里 Tengine 负载均衡算法揭秘](https://mp.weixin.qq.com/s/3KZ99d94yqRDxEByn7nGWg): 阿里自研 Tengine 通过实现新的负载均衡算法 Virtual Node Smooth Weighted Round-Robin（VNSWRR）解决了 SWRR 算法在阿里业务场景下的缺陷，而且 QPS 处理能力相对于 Nginx 官方的 SWRR 算法也提升了 60% 左右。

# HAProxy

- [How we fine-tuned HAProxy to achieve 2,000,000 concurrent SSL connections](https://medium.freecodecamp.com/how-we-fine-tuned-haproxy-to-achieve-2-000-000-concurrent-ssl-connections-d017e61a4d27)
