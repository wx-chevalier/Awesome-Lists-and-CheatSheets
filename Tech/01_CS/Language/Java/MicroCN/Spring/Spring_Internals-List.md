# Spring Internals List

# OpenSource

- [2017~tiny-spring ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/code4craft/tiny-spring)](https://github.com/code4craft/tiny-spring): tiny-spring 是为了学习 Spring 的而开发的，可以认为是一个 Spring 的精简版。Spring 的代码很多，层次复杂，阅读起来费劲。我尝试从使用功能的角度出发，参考 Spring 的实现，一步一步构建，最终完成一个精简版的 Spring。有人把程序员与画家做比较，画家有门基本功叫临摹，tiny-spring 可以算是一个程序的临摹版本-从自己的需求出发，进行程序设计，同时对著名项目进行参考。

- [2017~基于 Netty 的 Spring Boot 内置 Servlet 容器的实现 #Series#](https://parg.co/SCE): Spring Boot 有 Tomcat、Jetty 和 undertow 三种内置 Servlet 容器，默认使用 Tomcat。一般来说已经够用了，但当 Spring Boot 用于高并发微服务的时候，可能并不够用，而且 tomcat 的资源占用在这种情况下说不上轻量化了。于是萌生了自己实现一个 Spring Boot 的 Netty Servlet 容器的想法。

- [2018~徒手撸框架，实现 IoC ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/diaozxin007/xilidou-framework): Spring 作为 J2ee 开发事实上的标准，是每个 Java 开发人员都需要了解的框架。但是 Spring 的 IoC 和 Aop 的特性，对于初级的 Java 开发人员来说还是比较难于理解的。所以我就想写一系列的文章给大家讲解这些特性。从而能够进一步深入了解 Spring 框架。

- [2021~mini-spring ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/DerekYRC/mini-spring)](https://github.com/DerekYRC/mini-spring): mini-spring 是简化版的 spring 框架，能帮助你快速熟悉 spring 源码和掌握 spring 的核心原理。抽取了 spring 的核心逻辑，代码极度简化，保留 spring 的核心功能，如 IoC 和 AOP、资源加载器、事件监听器、类型转换、容器扩展点、bean 生命周期和作用域、应用上下文等核心功能。
