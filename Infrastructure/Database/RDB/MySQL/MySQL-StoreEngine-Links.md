[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wxyyxc1992/Awesome-Links)

# MySQL 工程实践与性能优化资料索引

- [2017-MySQL 处理海量数据时的一些优化查询速度方法](http://www.54tianzhisheng.cn/2017/04/29/MySQL-select-good/)

- [2017-How to Optimize MySQL: Indexes, Slow Queries, Configuration](https://parg.co/UrU): In this article, we’ll look at some MySQL optimization tips we’ve covered previously, and combine them with novelties that came out since.

- [2016-Writing a MySQL storage engine from scratch](https://www.codeproject.com/articles/1107279/writing-a-mysql-storage-engine-from-scratch): This article summarizes the things that I learned when I wrote a new MySQL storage engine (“SE”).

- [MySQL 线程池内幕](https://my.oschina.net/andylucc/blog/820624)：在 MySQL 中，线程池指的是用来管理处理 MySQL 客户端连接任务的线程的一种机制，我厂用的 percona 版本已经是集成了线程池，只需要通过如下参数开启即可。

- [MySQL 锁系列(七)之 锁算法详解](https://parg.co/bXN)

- [InnoDB 存储引擎体系架构](https://segmentfault.com/a/1190000004673132)

- [MySQL · InnoDB 文件系统之 IO 系统和内存管理  ](http://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650342507&idx=1&sn=b7beed97485a9eb1b2b5d80c16c02ef7&scene=23&srcid=0417dJlCwbKo1B0hQQrlG2jP#rd)

- [MySQL 如何存储大数据](https://github.com/zhangyachen/zhangyachen.github.io/issues/96)

* [2017-青铜到王者，快速提升你 MySQL 数据库的段位！](http://database.51cto.com/art/201708/550029.htm)

- [2017-MyFlash #Project#](https://github.com/Meituan-Dianping/MyFlash): MyFlash 是由美团点评公司技术工程部开发维护的一个回滚 DML 操作的工具。该工具通过解析 v4 版本的 binlog，完成回滚操作。相对已有的回滚工具，其增加了更多的过滤选项，让回滚更加容易。

# InnoDB

- [MySQL 加锁处理分析](http://hedengcheng.com/?p=771#_Toc374698313)

- [大众点评工程师：从特性说起，漫谈 MySQL 中的事务及其实现](http://dbaplus.cn/news-11-515-1.html)

- [InnoDB 的锁机制](http://owl-pi.com/2016/11/10/innodb-lock-1/)

- [MySQL 排序内部原理探秘](http://geek.csdn.net/news/detail/105891)

- [阿里云栖社区一系列关于 MySQL 的 InnoDB 引擎的讲解](https://yq.aliyun.com/groups/25?spm=5176.blog223.yqblogcon1.3.aZ9XJX)

- [MySQL 中的读写锁详解](http://www.jizhuomi.com/software/594.html)

- [MySQL 事务隔离级别的实现原理](http://www.cnblogs.com/cjsblog/p/8365921.html): MySQL 的众多存储引擎中，只有 InnoDB 支持事务，所有这里说的事务隔离级别指的是 InnoDB 下的事务隔离级别。

# Index | 索引

- [2011-MySQL 索引背后的数据结构及算法原理](http://blog.codinglabs.org/articles/theory-of-mysql-index.html): 为了避免混乱，本文将只关注于 BTree 索引，因为这是平常使用 MySQL 时主要打交道的索引，至于哈希索引和全文索引本文暂不讨论。

- [2017-10 分钟让你明白 MySQL 是如何利用索引的](http://fordba.com/spend-10-min-to-understand-how-mysql-use-index.html?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io): 在 MySQL 中进行 SQL 优化的时候，经常会在一些情况下，对 MySQL 能否利用索引有一些迷惑。

- [2018-B-Tree 索引](http://blueskykong.com/2018/07/28/b-tree-index/): 本文就详细讲解一下 B-Tree 索引的的底层结构，使用原则和特性
