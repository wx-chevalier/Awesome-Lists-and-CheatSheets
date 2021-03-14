# Spring Internals

- [2017-基于 Netty 的 Spring Boot 内置 Servlet 容器的实现 #Series#](https://parg.co/SCE): Spring Boot 有 Tomcat、Jetty 和 undertow 三种内置 Servlet 容器，默认使用 Tomcat。一般来说已经够用了，但当 Spring Boot 用于高并发微服务的时候，可能并不够用，而且 tomcat 的资源占用在这种情况下说不上轻量化了。于是萌生了自己实现一个 Spring Boot 的 Netty Servlet 容器的想法。

# IoC
