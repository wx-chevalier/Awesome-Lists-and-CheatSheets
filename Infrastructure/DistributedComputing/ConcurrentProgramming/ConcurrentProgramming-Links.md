[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wxyyxc1992/Awesome-Links)

# Concurrent Learning & Practices Links

# Overview

* [2015-Amdahl's Law](http://tutorials.jenkov.com/java-concurrency/amdahls-law.html)

* [2016-Concurrency and Parallelism: Understanding I/O](https://blog.risingstack.com/concurrency-and-parallelism-understanding-i-o/)

- [2017-Go 语言并发机制初探](https://yq.aliyun.com/articles/72365)：Go 语言一个很大的优势就是可以方便地编写并发程序。Go 语言内置了 goroutine 机制，使用 goroutine 可以快速地开发并发程序，Go 语言的并发机制有很多值得探讨的，比如 Go 语言和 Scala 并发实现的不同，Golang CSP 和 Actor 模型的对比等，了解并发机制的这些实现，可以帮助我们更好的进行并发程序的开发，实现性能的最优化。

- [2017-工作线程数究竟要设置为多少](https://mp.weixin.qq.com/s/BRpngTEFHjzpGv8tkdqmPQ)：Web  Server 通常有个配置，最大工作线程数，后端服务一般也有个配置，工作线程池的线程数量，这个线程数的配置不同的业务架构师有不同的经验值，有些业务设置为 CPU 核数的 2 倍，有些业务设置为 CPU 核数的 8 倍，有些业务设置为 CPU 核数的 32 倍。“工作线程数”的设置依据是什么，到底设置为多少能够最大化 CPU 性能，是本文要讨论的问题。

* [夏俊：深入网站服务端技术(一)——网站并发的问题](http://www.csdn.net/article/2015-03-16/2824221)

- [抛开语言和技术栈不谈，我们应该如何选择线程模型？ ](http://mp.weixin.qq.com/s?__biz=MzA5Nzc4OTA1Mw==&mid=2659598379&idx=1&sn=39d432e1d2f2c07254157e621bc50f01&chksm=8be99539bc9e1c2f892fcc89089c939d70361d1ba1fb584ce69ab68240eb35e6846f3c14bd6b&mpshare=1&scene=1&srcid=1028Z0atSJuHV9dRSZdjogqo#rd)

- [2018-Why goroutines are not lightweight threads?](https://codeburst.io/why-goroutines-are-not-lightweight-threads-7c460c1f155f): Concurrency has existed since long ago in the form of Threads which are used in almost all the applications these days.

# Concurrent IO

* [2017-epoll 浅析以及 nio 中的 Selector](http://www.importnew.com/24794.html)

# Asynchronous Pattern

* [CS168-Introduction to Asynchronous Programming](http://cs.brown.edu/courses/cs168/s12/handouts/async.pdf)
