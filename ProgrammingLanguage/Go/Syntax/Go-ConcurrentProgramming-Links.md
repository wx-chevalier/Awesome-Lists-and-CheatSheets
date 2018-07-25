# Concurrent Programming | 并发编程

- [2017-Visualizing Concurrency in Go · divan's blog](http://divan.github.io/posts/go_concurrency_visualize/): One of the strongest sides of Go programming language is a built-in concurrency based on Tony Hoare’s CSP paper. Go is designed with concurrency in mind and allows us to build complex concurrent pipelines. But have you ever wondered - how various concurrency patterns look like?

- [2018-Go Channel 应用模式](http://colobu.com/2018/03/26/channel-patterns): 除了正常的在 goroutine 之间安全地传递共享数据， Channel 还可以玩出很多的花样(模式)， 本文列举了一些 channel 的应用模式。

## Memory Model

- [The Go Memory Model](https://golang.org/ref/mem): The Go memory model specifies the conditions under which reads of a variable in one goroutine can be guaranteed to observe values produced by writes to the same variable in a different goroutine.
