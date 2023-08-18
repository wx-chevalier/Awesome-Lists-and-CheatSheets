# CPP Concurrent Programming List

- [2016-Pthreads 入门教程](https://hanbingyan.github.io/2016/03/07/pthread_on_linux/#section): Pthreads 是 IEEE（电子和电气工程师协会）委员会开发的一组线程接口，负责指定便携式操作系统接口（POSIX）. Pthreads 中的 P 表示 POSIX，实际上，Pthreads 有时候也代表 POSIX 线程.

- [2020~《Cpp-Concurrency-in-Action》-2ed](https://github.com/downdemo/Cpp-Concurrency-in-Action-2ed): C++11 引入了 Boost 线程库作为标准线程库，作者 Anthony Williams 为介绍其特性，于 2012 年出版了 C++ Concurrency in Action 一书，并顺应 C++17 于 2019 年 2 月出版了第二版。C++ Concurrency in Action 2ed 前五章介绍了线程支持库的基本用法，后六章从实践角度介绍了并发编程的设计思想，相比第一版多介绍了一些 C++17 特性，如 std::scoped_lock、std::shared_mutex，并多出一章（第十章）介绍 C++17 标准库并行算法，此外个人会在相应处补充 C++20 相关特性，如 std::jthread、std::counting_semaphore、std::barrier、std::latch 等。阅读本书前可参考 Andrew S. Tanenbaum 的 Modern Operating Systems，预备操作系统的基础知识（进程与线程、死锁、内存管理、文件系统、I/O 等）。此为个人笔记，仅供参考，更详细内容见原书。

- [2023~C++ Coroutines Part 1: co_yield, co_return and a Prime Sieve](https://nigeltao.github.io/blog/2023/cpp-coro-part-1-yield-return-prime-sieve.html): My two blog posts don’t aim to be comprehensive but instead to give a quick tour of the three fundamental mechanisms (the new-in-C++20 coroutine-related operators): co_yield, co_return and co_await. Both blog posts walk through a complete, simple program, somewhat like literate programming.
