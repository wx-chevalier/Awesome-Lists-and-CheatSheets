# Go Concurrent Programming List

- [2017-Visualizing Concurrency in Go · divan's blog](http://divan.github.io/posts/go_concurrency_visualize/): One of the strongest sides of Go programming language is a built-in concurrency based on Tony Hoare’s CSP paper. Go is designed with concurrency in mind and allows us to build complex concurrent pipelines. But have you ever wondered - how various concurrency patterns look like?

- [2018-Go Channel 应用模式](http://colobu.com/2018/03/26/channel-patterns): 除了正常的在 goroutine 之间安全地传递共享数据，Channel 还可以玩出很多的花样(模式)，本文列举了一些 channel 的应用模式。

- [2019~LearnConcurrency](https://github.com/golang/go/wiki/LearnConcurrency): This page links to resources for learning about concurrency in Go. The items are presented in order, from beginner material to advanced topics.

# Primitive

- [2018-Goroutine 并发调度模型深度解析&手撸一个协程池](http://blog.taohuawu.club/article/42): 本文将通过 runtime 对 goroutine 的调度分析，帮助大家理解它的机理和发现一些内存和调度的原理和问题，并且基于此提出一种个人的解决方案 — 一个高性能的 Goroutine Pool（协程池）。

# Memory Model

- [The Go Memory Model](https://golang.org/ref/mem): The Go memory model specifies the conditions under which reads of a variable in one goroutine can be guaranteed to observe values produced by writes to the same variable in a different goroutine.
