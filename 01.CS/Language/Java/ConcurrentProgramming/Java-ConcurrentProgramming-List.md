# Java Concurrent Programming List

# Overview

- [2014-Java 并发导论](http://ifeve.com/concurrency-paper/)：由于之前工作中的疏忽，在使用 Java 多线程并发的时候出了问题，遂决心全面学习并发相关知识。写作本文的意图只是希望在写作过程中把想不清楚或是一时无法掌握的地方反复揣摩记录下来。

- [JVM 并发编程模型览](http://www.qingjingjie.com/blogs/23)

- [2015-Java Concurrency/Multithreading Tutorial](http://tutorials.jenkov.com/java-concurrency/index.html): The trail will primarily be concerned with multithreading in Java, but some of the problems occurring in multithreading are similar to problems occurring in multitasking and in distributed systems.

- [Java 并发的四种风味：Thread、Executor、ForkJoin 和 Actor](http://www.open-open.com/lib/view/open1421202894171.html)

- [java8-concurrency-tutorial](http://winterbe.com/posts/2015/04/07/java8-concurrency-tutorial-thread-executor-examples/)

- [java-util-concurrent](http://tutorials.jenkov.com/java-util-concurrent/index.html)

- [Threading in Java](https://medium.com/@behzodbekqodirov/threading-java-541bd986647d#.lmwvdmeje)

- [2017-面试小结之并发篇](http://ginobefunny.com/post/java_concurrent_interview_questions/)：最近面试一些公司，被问到的关于 Java 并发编程的问题，以及自己总结的回答。

- [2017-所有对象都自动含有单一的锁与一个对象可以被多次加锁的矛盾？](https://parg.co/bO2)

- [2017-Java 线程池的理论与实践](http://www.jianshu.com/p/0478e283cfef)：本文将会包含以下内容：Java 中的 Thread 与操作系统中的线程的关系、线程切换的各种开销、ThreadGroup 存在的意义、使用线程池减少线程开销、Executor 的概念、ThreadPoolExecutor 中的一些具体实现、如何监控线程的健康、参考 ThreadPoolExecutor 来设计适合自己的线程模型。

- [2017-Using the Timer Class to Schedule Tasks](https://dzone.com/articles/using-timer-class-to-schedule-tasks): Setting up simple scheduled tasks within an app is easy with the Timer class. There's a lot of versatility in the class, giving you plenty of customization.

- [Using the Timer Class to Schedule Tasks](https://dzone.com/articles/using-timer-class-to-schedule-tasks)

- [Java Concurrency Patterns and Features ![code](https://ng-tech.icu/assets/code.svg)](https://parg.co/UVC): Concurrency Patterns and features found in Java, through multithreaded programming. Threads, Locks, Atomics and more.

- [2017-Java Concurrency / Multithreading Basics](https://www.callicoder.com/java-concurrency-multithreading-basics/): Concurrency is the ability to do more than one thing at the same time.

# Resource

## Collection

- [2019-threadandjuc ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/qiurunze123/threadandjuc)](https://github.com/qiurunze123/threadandjuc): ⭐⭐⭐⭐ 高并发-高可靠-高性能 three-high-import 导入系统-高并发多线程进阶

- [2019-CL0610/Java-concurrency ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/CL0610/Java-concurrency)](https://github.com/CL0610/Java-concurrency):
  整个系列文章为 Java 并发专题，一是自己的兴趣，二是，这部分在实际理解上很有难度，另外在面试过程中也是经常被问到。所以在学习过程中，记录了 Java 并发相关的基础知识，一是自己对知识能够建立体系，同时也希望有幸能够对其他人有用。

## Series

- [死磕 Java 并发系列 #Series#](http://cmsblogs.com/?author=1)：[J.U.C 之 AQS：CLH 同步队列](http://cmsblogs.com/?p=2188)、[J.U.C 之 AQS：AQS 简介](http://cmsblogs.com/?p=2174)、[Java 内存模型之总结](http://cmsblogs.com/?p=2167)、[Java 内存模型之从 JMM 角度分析 DCL](http://cmsblogs.com/?p=2161)、[Java 内存模型之分析 volatile](http://cmsblogs.com/?p=2148)、[死磕 Java 系列博客](http://cmsblogs.com/?p=2122)、[Java 内存模型之重排序](http://cmsblogs.com/?p=2116)、[ Java 内存模型之 happens-before](http://cmsblogs.com/?p=2102)

- [2021-RedSpider Concurrent #Series#](https://github.com/RedSpider1/concurrent): 这是 RedSpider 社区成员原创与维护的 Java 多线程系列文章。

# Concurrency Primitives | 并发单元

- [2017-深度解析 Java 线程池的异常处理机制](https://github.com/aCoder2013/blog/issues/3): 线程池提交的任务如果没有 catch 异常，那么会抛到哪里去？

- [2017-从 0 到 1 学习 Java 线程池 #Series#](http://6me.us/TOE3)：该系列文章总共三篇，介绍了 Java 线程池的使用以及原理，并且最后会实现一个基本的线程池。

# Async Patterns | 异步模式

# Concurrency Control | 并发控制

## Variables | 变量

- [2017-An Introduction to Atomic Variables in Java](http://www.baeldung.com/java-atomic-variables)

- [深入理解 Java 之 ThreadLocal 工作原理](http://allenwu.itscoder.com/threadlocal-source): 简单理解“Thread”即线程，“Local”即本地。连续起来理解就是 每个线程本地独有的。

# Coroutine

- [2017-Project Loom: Fibers and Continuations for the Java Virtual Machine](http://cr.openjdk.java.net/~rpressler/loom/Loom-Proposal.html)

- [2017-Java CompletableFuture Tutorial with Examples](https://www.callicoder.com/java-8-completablefuture-tutorial/): In this post I’ll give you a detailed explanation of CompletableFuture and all its methods using simple examples.
