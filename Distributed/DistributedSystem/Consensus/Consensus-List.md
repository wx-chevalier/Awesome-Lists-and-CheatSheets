# Distributed Consistency

- [分布式事务：不过是在一致性、吞吐量和复杂度之间，做一个选择](www.primeton.com/read.php?id=2258&his=1)

- [分布式一致性论文阅读阶段性小结](http://blog.fnil.net/blog/ac1fa10ff9b2404ed0b91bdfaf76a87d/)

- [2004-Consensus on Transaction Commit](https://lamport.azurewebsites.net/video/consensus-on-transaction-commit.pdf): The distributed transaction commit problem requires reaching agreement on whether a transaction is committed or aborted.

- [2021-The Problem of Distributed Consensus](https://writings.stephenwolfram.com/2021/05/the-problem-of-distributed-consensus/): In the past, it’s been difficult to analyze the more general setup where there is no rigid notion of either space or time. But this is exactly the setup in our new Physics Project, and so there’s now the potential to use its formalism and results (as well as intuition imported from physics) to make further progress.

- [分布式系统的事务处理](http://mp.weixin.qq.com/s?__biz=MzA4NDc2MDQ1Nw==&mid=2650238031&idx=1&sn=d7ba7844f15d587c83906aedd073748a&scene=0#wechat_redirect)

# Consistency & CAP

- [2011-Consistency, Availability, and Convergence #Paper#](https://apps.cs.utexas.edu/tech_reports/reports/tr/TR-2036.pdf): We examine the limits of consistency in fault-tolerant distributed storage systems.

- [大话分布式系统理论基础](http://mp.weixin.qq.com/s/p4PEZPjxJyYXKpkCCdShbw)

- [不懂点 CAP 理论，你好意思说你是做分布式的吗？](https://parg.co/ULa): CAP 理论，被戏称为[帽子理论]。CAP 理论由 Eric Brewer 在 ACM 研讨会上提出，而后 CAP 被奉为分布式领域的重要理论。

- [2016-2016 年，分布式数据库的那些事儿都在这里！](https://parg.co/b1g)

- [2016-腾讯金融级分布式数据库 TDSQL 的前世今生](http://blog.csdn.net/test_soy/article/details/53259136): TDSQL(Tencent Distributed MySQL，腾讯分布式 MySQL)是由腾讯技术工程事业群计费平台部针对金融联机交易场景开发的高一致性数据库集群产品。

## Eventually Consistency

- [Base: 一种 Acid 的替代方案-中文翻译](http://article.yeeyan.org/view/167444/125572)

- [2020-Limitations of Highly-Available Eventually-Consistent Data Stores #Paper#](https://www.cs.tau.ac.il/~mad/publications/podc2015-replds.pdf): Modern replicated data stores aim to provide high availability, by immediately responding to client requests, often by implementing objects that expose concurrency.

# Consensus Algorithms

- [In search of a simple consensus algorithm](http://rystsov.info/2017/02/15/simple-consensus.html)

# OpenSource

- [2021-Stateright ![code](https://shorturl.at/dlxyK)](https://github.com/stateright/stateright): Correctly implementing distributed algorithms such as the Paxos and Raft consensus protocols is notoriously difficult due to inherent nondetermism such as message reordering by network devices. Stateright is a Rust actor library that aims to solve this problem by providing an embedded model checker, a UI for exploring system behavior (demo), and a lightweight actor runtime. It also features a linearizability tester that can be run within the model checker for more exhaustive test coverage than similar solutions such as Jepsen.
