[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wx-chevalier/Awesome-Lists)

# 分布式系统学习与实践资料索引

# Overview

- [分布式系统本质论](http://www.52cs.org/)

* [In search of a simple consensus algorithm](http://rystsov.info/2017/02/15/simple-consensus.html)

* [漫谈分布式系统、拜占庭将军问题与区块链](https://mp.weixin.qq.com/s/tngWdvoev8SQiyKt1gy5vw): 今天本文就借这个机会，跟大家一起讨论一下分布式系统的核心问题和概念。最后，我们将尽量沿着逻辑上前后一贯的思路，讨论一下区块链技术。

- [走向分布式，分布式系列入门教程](http://dcaoyuan.github.io/papers/pdfs/Scalability.pdf)

- [浅析分布式系统](http://wetest.qq.com/lab/view/203.html?from=content_toutiao): 来自腾讯 Wadehan 关于服务器端系统技术的基础概念探索

* [分布式系统互斥性与幂等性问题的分析与解决 ](http://blog.csdn.net/zdy0_2004/article/details/52760404)

# Resources

## Book

- [2012-Concurrent Programming for Scalable Web Architectures #Book#](http://berb.github.io/diploma-thesis/): We examine the relations between concurrency, scalability and distributed systems and dare an outlook on the near future.

- [2012-The Art of Multiprocessor Programming, Revised Reprint](https://www.safaribooksonline.com/library/view/the-art-of/9780123973375/): The Art of Multiprocessor Programming is an authoritative guide to multicore programming. It introduces a higher level set of software development skills than that needed for efficient single-core programming. This book provides comprehensive coverage of the new principles, algorithms, and tools necessary for effective multiprocessor programming.

- [2011-Özsu-Principles of Distributed Database Systems-3rd Edition #Book#](http://www.springer.com/us/book/9781441988331): The first part discusses the fundamental principles of distributed data management and includes distribution design, data integration, distributed query processing and optimization, distributed transaction management, and replication. The second part focuses on more advanced topics and includes discussion of parallel database systems, distributed object management, peer-to-peer data management, web data management, data stream systems, and cloud computing.

* [2017-Designing Data Intensive Applications #Book#](https://dataintensive.net/): This book will help you navigate the diverse and fast-changing landscape of technologies for storing and processing data.

## Course

- [2018-6.824: Distributed Systems](http://nil.csail.mit.edu/6.824/2018/index.html): It will present abstractions and implementation techniques for engineering distributed systems.

## Paper

- Fallacies of Distributed Computing

- Distributed systems theory for the distributed systems engineer

- FLP Impossibility Result

- An introduction to distributed systems

- Distributed Systems for fun and profit

- Distributed Systems: Principles and Paradigms

- Scalable Web Architecture and Distributed Systems

- Principles of Distributed Systems

- Making reliable distributed systems in the presence of software errors

- Designing Data Intensive Applications

# CAP

- [大话分布式系统理论基础](http://mp.weixin.qq.com/s/p4PEZPjxJyYXKpkCCdShbw)

- [不懂点 CAP 理论，你好意思说你是做分布式的吗？ ](https://parg.co/ULa): CAP 理论，被戏称为[帽子理论]。CAP 理论由 Eric Brewer 在 ACM 研讨会上提出，而后 CAP 被奉为分布式领域的重要理论。

- [Base: 一种 Acid 的替代方案-中文翻译](http://article.yeeyan.org/view/167444/125572)

- [2016-2016 年，分布式数据库的那些事儿都在这里！](https://parg.co/b1g)

- [2016-腾讯金融级分布式数据库 TDSQL 的前世今生](http://blog.csdn.net/test_soy/article/details/53259136): TDSQL(Tencent Distributed MySQL，腾讯分布式 MySQL)是由腾讯技术工程事业群计费平台部针对金融联机交易场景开发的高一致性数据库集群产品。

* [An introduction to distributed systems](https://github.com/aphyr/distsys-class): 一个基本的分布式系统简介

# 分布式 ID

- [分布式 ID 生成系统怎么做？](http://mp.weixin.qq.com/s/vurewakh7jINbmgKWR8rTw): 在分布式系统中，经常需要对大量的数据、消息、http 请求等进行唯一标识，例如：对于分布式系统，服务间相互调用需要唯一标识，调用链路分析的时候需要使用这个唯一标识。

* [五分钟了解分布式 ID 生成方案](http://mp.weixin.qq.com/s?__biz=MzA5ODM0NjA3NA==&mid=2651209088&idx=1&sn=640af6452e8644e65c5c5985eb405358&scene=4#wechat_redirect)

* [2017-Leaf—— 美团点评分布式 ID 生成系统](http://tech.meituan.com/MT_Leaf.html)：在复杂分布式系统中，往往需要对大量的数据和消息进行唯一标识。如在美团点评的金融、支付、餐饮、酒店、猫眼电影等产品的系统中，数据日渐增长，对数据分库分表后需要有一个唯一 ID 来标识一条数据或消息，数据库的自增 ID 显然不能满足需求；特别一点的如订单、骑手、优惠券也都需要有唯一 ID 做标识。此时一个能够生成全局唯一 ID 的系统是非常必要的。。

## Twitter-Snowflake

- [Twitter-Snowflake，64 位自增 ID 算法详解](http://www.lanindex.com/twitter-snowflake%EF%BC%8C64%E4%BD%8D%E8%87%AA%E5%A2%9Eid%E7%AE%97%E6%B3%95%E8%AF%A6%E8%A7%A3/)

- [微信序列号生成器架构设计及演变](http://h2ex.com/1163)
