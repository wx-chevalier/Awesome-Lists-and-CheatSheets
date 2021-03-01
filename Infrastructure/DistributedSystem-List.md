# Distributed System List

# Overview

- [漫谈分布式系统、拜占庭将军问题与区块链](https://mp.weixin.qq.com/s/tngWdvoev8SQiyKt1gy5vw): 今天本文就借这个机会，跟大家一起讨论一下分布式系统的核心问题和概念。最后，我们将尽量沿着逻辑上前后一贯的思路，讨论一下区块链技术。

- [走向分布式，分布式系列入门教程](http://dcaoyuan.github.io/papers/pdfs/Scalability.pdf)

- [浅析分布式系统](http://wetest.qq.com/lab/view/203.html?from=content_toutiao): 来自腾讯 Wadehan 关于服务器端系统技术的基础概念探索

- [分布式系统互斥性与幂等性问题的分析与解决 ](http://blog.csdn.net/zdy0_2004/article/details/52760404)

- [An introduction to distributed systems](https://github.com/aphyr/distsys-class): 一个基本的分布式系统简介

# Resource

## Book

- [2012-Concurrent Programming for Scalable Web Architectures #Book#](http://berb.github.io/diploma-thesis/): We examine the relations between concurrency, scalability and distributed systems and dare an outlook on the near future.

- [2012-The Art of Multiprocessor Programming, Revised Reprint](https://www.safaribooksonline.com/library/view/the-art-of/9780123973375/): The Art of Multiprocessor Programming is an authoritative guide to multicore programming. It introduces a higher level set of software development skills than that needed for efficient single-core programming. This book provides comprehensive coverage of the new principles, algorithms, and tools necessary for effective multiprocessor programming.

- [2011-Özsu-Principles of Distributed Database Systems-3rd Edition #Book#](http://www.springer.com/us/book/9781441988331): The first part discusses the fundamental principles of distributed data management and includes distribution design, data integration, distributed query processing and optimization, distributed transaction management, and replication. The second part focuses on more advanced topics and includes discussion of parallel database systems, distributed object management, peer-to-peer data management, web data management, data stream systems, and cloud computing.

- [2017-Designing Data Intensive Applications #Book#](https://dataintensive.net/): This book will help you navigate the diverse and fast-changing landscape of technologies for storing and processing data. [DDIA 中文翻译](https://github.com/Vonng/ddia)。

- [2018-Programming Models for Distributed Computation #Book#](https://github.com/heathermiller/dist-prog-book): This is a book about the programming constructs we use to build distributed systems. These range from the small, RPC, futures, actors, to the large; systems built up of these components like MapReduce and Spark. We explore issues and concerns central to distributed systems like consistency, availability, and fault tolerance, from the lens of the programming models and frameworks that the programmer uses to build these systems.

## Blog

- [the morning paper #Blog#](https://blog.acolyer.org): A random walk through Computer Science research, by Adrian Colyer.

## Collection

- [The Twelve-Factor App #Collection#](http://12factor.net/zh_cn/): To raise awareness of some systemic problems we’ve seen in modern application development, to provide a shared vocabulary for discussing those problems, and to offer a set of broad conceptual solutions to those problems with accompanying terminology.

- [awesome-shell #Collection#](https://github.com/alebcay/awesome-shell): A curated list of awesome command-line frameworks, toolkits, guides and gizmos. Inspired by awesome-php.

- [Cloud Native Landscape #Collection#](https://github.com/cncf/landscape): Static Cloud Native Landscapes and Interactive Landscape that filters and sorts hundreds of cloud native projects and products, and shows details including GitHub stars, funding or market cap, first and last commits, contributor counts, headquarters location, and recent tweets.

- [2019-分布式系统领域经典论文翻译集 #Collection#](https://zhuanlan.zhihu.com/p/91434149)

- [2019-A Distributed Systems Reading List #Collection#](https://dancres.github.io/Pages/): I often argue that the toughest thing about distributed systems is changing the way you think. The below is a collection of material I've found useful for motivating these changes.

## Course

- [2018-6.824: Distributed Systems](http://nil.csail.mit.edu/6.824/2018/index.html): It will present abstractions and implementation techniques for engineering distributed systems.

- [2018-MIT-6.824 #Course#](http://nil.csail.mit.edu/6.824/2018/schedule.html): Distributed Systems Engineering, What is a distributed system?, etc.

- [PingCAP Talent Plan #Course#](https://github.com/pingcap/talent-plan): This is a series of training courses about writing distributed systems in Go and Rust. It is maintained by PingCAP for training and/or evaluating students, new employees, and new contributors to TiDB and TiKV.

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

## Series

- [2020-Patterns of Distributed Systems #Series#](https://martinfowler.com/articles/patterns-of-distributed-systems/): This article recognizes and develops these solutions as patterns, with which we can build up an understanding of how to better understand, communicate and teach distributed system design.

# Consistency & CAP

- [2011-Consistency, Availability, and Convergence #Paper#](https://apps.cs.utexas.edu/tech_reports/reports/tr/TR-2036.pdf): We examine the limits of consistency in fault-tolerant distributed storage systems.

- [大话分布式系统理论基础](http://mp.weixin.qq.com/s/p4PEZPjxJyYXKpkCCdShbw)

- [不懂点 CAP 理论，你好意思说你是做分布式的吗？](https://parg.co/ULa): CAP 理论，被戏称为[帽子理论]。CAP 理论由 Eric Brewer 在 ACM 研讨会上提出，而后 CAP 被奉为分布式领域的重要理论。

- [2016-2016 年，分布式数据库的那些事儿都在这里！](https://parg.co/b1g)

- [2016-腾讯金融级分布式数据库 TDSQL 的前世今生](http://blog.csdn.net/test_soy/article/details/53259136): TDSQL(Tencent Distributed MySQL，腾讯分布式 MySQL)是由腾讯技术工程事业群计费平台部针对金融联机交易场景开发的高一致性数据库集群产品。

## Eventually Consistency

- [Base: 一种 Acid 的替代方案-中文翻译](http://article.yeeyan.org/view/167444/125572)

- [2020-Limitations of Highly-Available Eventually-Consistent Data Stores #Paper#](https://www.cs.tau.ac.il/~mad/publications/podc2015-replds.pdf): Modern replicated data stores aim to provide high availability, by immediately responding to client requests, often by implementing objects that expose concurrency.
