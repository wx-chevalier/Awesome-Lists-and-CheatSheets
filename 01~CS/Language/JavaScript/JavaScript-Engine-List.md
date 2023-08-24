# JavaScript Engine & V8 List

# Overview

- [2017~认识 V8 引擎](https://zhuanlan.zhihu.com/p/27628685)：V8 是如何使得 JavaScript 性能有大幅提升的呢？通过对一些书籍和文章的学习，梳理了 V8 的相关内容，本文将带你认识 V8。

- [2017~Understanding JS Engine with Cartoons](https://parg.co/U3B)

- [2017~Node.js V8 internals: an illustrative primer](https://parg.co/UXh): It’s really interesting to dig some proof of concept technology, it also will help us to write better code.

## News

- [High-performance ES2015 and beyond](http://6me.us/2dRAT4): Over the last couple of months the V8 team focused on bringing the performance of newly added ES2015 and other even more recent JavaScript features on par with their transpiled ES5 counterparts.

## Resource

- [demystifying-js-engines](https://github.com/a0viedo/demystifying-js-engines): 一系列讲解 JavaScript 虚拟机构造的资源整合

- [v8project.blogspot.com 🗃️](http://v8project.blogspot.com/): Official V8 blog

- [Rednaxelafx: 各 JavaScript 引擎的简介，及相关资料 / 博客收集帖](http://hllvm.group.iteye.com/group/topic/37596): 各 JavaScript 引擎的简介，及相关资料 / 博客收集帖

- [v8-perf](https://github.com/thlorenz/v8-perf): Notes and resources related to v8 and thus Node.js performance

- [Rednaxelafx: Implementing a JavaScript Engine](http://www.slideshare.net/RednaxelaFX/implement-js-krystalmok20131110)

# Complier

- [2017~How The Performance Characteristics of V8's Turbofan Will Affect The Way WE Optimize ](https://www.nearform.com/blog/node-js-is-getting-a-new-v8-with-turbofan/):

- [2017~Understanding How the Chrome V8 Engine Translates JavaScript into Machine Code](https://parg.co/Utm): All of our systems consists of microprocessors, the thing that is sitting inside your computer right now and allowing you to read this.

- [2017~Understanding V8’s Bytecode](https://parg.co/bzQ): This article explains V8’s bytecode format — which is actually easy to read once you understand some basic concepts.

# AST

- JavaScript Generator: [ECMAScript code generator on steroids](https://github.com/inikulin/esotope), [ECMAScript code generator](https://github.com/estools/escodegen)

- [2017~Understanding ASTs by Building Your Own Babel Plugin](https://www.sitepoint.com/understanding-asts-building-babel-plugin/)

- [2017~16-BIT VM IN JAVASCRIPT](https://francisstokes.wordpress.com/2017/07/20/16-bit-vm-in-javascript/)

- [前端工程师为什么要学习编译原理？](https://zhuanlan.zhihu.com/p/31096468): 而编译原理，作为一门基础理论学科，除了 JS 语言本身的编译器之外，更成为 Babel、ESLint、Stylus、Flow、Pug、YAML、Vue、React、Marked 等开源前端框架的理论基石之一。了解编译原理能够对所接触的框架有更充分的认识。

## Optimization

- [2017~An Introduction to Speculative Optimization in V8](https://parg.co/Uuv): An impressively low-level article that we hope gives you a good idea about what happens in V8 when it comes to optimization.

## Babel

- [2017~Babel Handbook》📚](https://github.com/thejameskyle/babel-handbook): A guided handbook on how to use Babel and how to create plugins for Babel.

# Memory Management

## Memory Allocation

- [A tour of V8: object representation](http://www.jayconrod.com/posts/52/a-tour-of-v8-object-representation)

- [JavaScript 中使用 object[key] 查找属性的过程是怎样的呢(相对于 Array 查找元素)？](https://www.zhihu.com/question/30848981/answer/51997592)

- [2017~Exposing HomeObject](https://hackernoon.com/exposing-homeobject-e61061cbfe17#.e9vdk64zd)

- [MDN: Memory Management](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management)

- [2017~Fast Properties in V8](https://parg.co/b70): In this blog post we would like to explain how V8 handles JavaScript properties internally.

# Garbage Collection

- [2017~Orinoco: young generation garbage collection](https://parg.co/UpK): V8 partitions its managed heap into generations where objects are initially allocated in the “nursery” of the young generation.

- [2017~Garbage collection in V8, an illustrated guide](https://parg.co/bQG): I would also like to mention that this guide is meant to be beginner friendly, and does not cover every aspect of memory management within V8, and the rest of V8 internals.

- [A crash course in memory management](https://parg.co/b9p): To understand why ArrayBuffer and SharedArrayBuffer were added to JavaScript, you need to understand a bit about memory management.

- [JavaScript Memory Usage](https://roman01la.github.io/js-memory-usage/)

- [Node.js at Scale - Node.js Garbage Collection Explained](https://blog.risingstack.com/node-js-at-scale-node-js-garbage-collection/)

## Memory Leak

- [深入理解 Node.js 中的垃圾回收和内存泄漏的捕获](http://wwsun.github.io/posts/understanding-nodejs-gc.html)

- [2017~How JavaScript works: memory management + how to handle 4 common memory leaks](https://parg.co/bnw)

- [2017~JavaScript 内存泄漏教程](http://www.ruanyifeng.com/blog/2017/04/memory-leak.html)

- [A curious case of memory leak in a node.js app](https://www.future-processing.pl/blog/a-curious-case-of-memory-leak-in-a-node-js-app/)

- [Demystifying v8 and JavaScript Performance](http://thlorenz.com/talks/demystifying-v8/talk.pdf)

- [V8 Docs: Object Class Links](https://v8docs.nodesource.com/node-7.2/db/d85/classv8_1_1_object.html)

- [How does V8 manage the memory of object instances?](http://stackoverflow.com/questions/7413168/how-does-v8-manage-the-memory-of-object-instances)

- [2017~How JavaScript works: inside the V8 engine + 5 tips on how to write optimized code](https://blog.sessionstack.com/how-javascript-works-inside-the-v8-engine-5-tips-on-how-to-write-optimized-code-ac089e62b12e): The first post of the series focused on providing an overview of the engine, the runtime and the call stack. This second post will be diving into the internal parts of Google’s V8 JavaScript engine.
