# JVM Memory Management List

# Overview

- [《成神之路-基础篇》JVM——Java 内存相关(已完结)](http://www.hollischuang.com/archives/1003)

# Memory Allocation

- [认识 JVM(上)——对象分配&回收算法](http://www.importnew.com/18242.html)

- [垃圾收集器与内存分配策略——在线文字版](http://book.51cto.com/art/201107/278857.htm)

- [2016-Java 内存管理初探](https://halfstackdeveloper.github.io/2016/12/30/java%E5%86%85%E5%AD%98%E7%AE%A1%E7%90%86%E5%88%9D%E6%8E%A2/)

# Garbage Collection

- [2018-Java Garbage Collection handbook #Series#](https://plumbr.eu/java-garbage-collection-handbook): The Java Virtual Machine is a wonderful construct in many ways. Perhaps the most amazing part of it is the Garbage Collection process that automatically takes care of memory management. However – as with all automated solutions, it’s good to understand how they work, even if you don’t plan to manually tune them.

- [成为 JavaGC 专家(1)—深入浅出 Java 垃圾回收机制](http://www.importnew.com/1993.html)

- [JVM 垃圾回收器工作原理及使用实例介绍](www.ibm.com/developerworks/cn/java/j-lo-JVMGarbageCollection/index.html)

- [Java 中, 为什么一个对象的实例方法在执行完成之前其对象可以被 GC 回收?](https://www.zhihu.com/question/51244545/answer/126055789)

- [【笔记】Java 虚拟机(一)-GC](https://darkness463.github.io/2017/03/30/Java-VM-GC/)

## Garbage Collector

- [2019-Do It Yourself (OpenJDK) Garbage Collector](https://shipilev.net/jvm/diy-gc/): Adding garbage collection to our non-garbage collector: wait, what?

## CMS

- [2013-并发垃圾收集器（CMS）为什么没有采用标记整理-算法来实现，而是采用的标记-清除算法？](http://hllvm.group.iteye.com/group/topic/38223#post-248757)

## G1

- [Case for Defaulting to G1 Garbage Collector in Java 9](https://www.infoq.com/articles/Make-G1-Default-Garbage-Collector-in-Java-9#anch128313)

## ZGC

- [2018-Java 程序员的荣光，听 R 大论 JDK11 的 ZGC](https://mp.weixin.qq.com/s/KUCs_BJUNfMMCO1T3_WAjw?from=groupmessage&isappinstalled=0): ZGC 的成绩是，无论你开了多大的堆内存(1288G？2T？)，硬是能保证低于 10 毫秒的 JVM 停顿。

# Memory Leak | 内存泄漏

- [2017-How Memory Leaks Happen in a Java Application](https://stackify.com/memory-leaks-java/): In this article, we’re going to describe the most common memory leaks, understand their causes, and look at a few techniques to detect/avoid them.

- [2017-How Memory Leaks Happen in a Java Application](https://stackify.com/memory-leaks-java?utm_source=mybridge&utm_medium=ios&utm_campaign=read_more): In this article, we’re going to describe the most common memory leaks, understand their causes, and look at a few techniques to detect/avoid them.

- [The Introduction of Java Memory Leaks](http://www.programcreek.com/2013/10/the-introduction-of-memory-leak-what-why-and-how/): One of the most significant advantages of Java is its memory management. You simply create objects and Java Garbage Collector takes care of allocating and freeing memory. However, the situation is not as simple as that, because memory leaks frequently occur in Java applications.

- [Creating a memory leak with Java](https://stackoverflow.com/questions/6470651/creating-a-memory-leak-with-java)

- [2017-Troubleshooting Memory Issues in Java Applications](https://parg.co/bsr): Troubleshooting memory problems can be tricky but the right approach and proper set of tools can simplify the process substantially.
