# JavaScript Async List | JavaScript 异步编程资料索引

- [2016-JavaScript 之异步编程简述](http://blog.codingplayboy.com/2016/01/20/js_async_intro/)

- [2017-JavaScript 异步编程](http://blog.codingplayboy.com/2017/04/25/js_async/)

- [The Evolution of Asynchronous JavaScript](https://blog.risingstack.com/asynchronous-javascript/)

- [最后谈一次 JavaScript 异步编程](https://zhuanlan.zhihu.com/p/24444262)

- [introduction-to-asynchronous-javascript](http://tutorials.pluralsight.com/front-end-javascript/introduction-to-asynchronous-javascript)

- [Node.js Flow (part 1) - Callback Hell vs. Async vs. Highland](http://blog.vullum.io/javascript-flow-callback-hell-vs-async-vs-highland/)

# Event Loop

- [2014-阮一峰-JavaScript 运行机制详解：再谈 Event Loop](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)

- [2015-Tasks, microtasks, queues and schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)

- [2016-理解事件循环](https://github.com/ccforward/cc/issues/47)

- [2017-Vue 源码详解之 nextTick：MutationObserver 只是浮云，microtask 才是核心！](https://segmentfault.com/a/1190000008589736):

- [2016-setImmediate.js ![code](https://martrix-usa.oss-accelerate.aliyuncs.com/logo/code.svg) ](https://github.com/YuzuJS/setImmediate): setImmediate.js is a highly cross-browser implementation of the setImmediate and clearImmediate APIs, proposed by Microsoft to the Web Performance Working Group.

- [Asynchronous Adventures in JavaScript: Understanding the Event Loop](https://medium.com/@BenDiuguid/asynchronous-adventures-in-javascript-understanding-the-event-loop-fc6f968d5f72#.6td5rwy71)

- [What is the JavaScript Event Loop?](http://altitudelabs.com/blog/what-is-the-javascript-event-loop/)

- [2017-Understanding Javascript Function Executions — Call Stack, Event Loop, Tasks & more ](https://medium.com/@gaurav.pandvia/understanding-javascript-function-executions-tasks-event-loop-call-stack-more-part-1-5683dea1f5ec?source=linkShare-fe48c4221a4c-1503534847)

- [浏览器和 Node 中 Event Loop 其实是不相同的。](https://zhuanlan.zhihu.com/p/54882306): 本文我们将会介绍 JS 实现异步的原理，并且了解了在浏览器和 Node 中 Event Loop 其实是不相同的。

## Node.js EventLoop

- [The Node.js Event Loop, Timers, and process.nextTick()](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)

- [2016-Understanding the Node.js Event Loop](https://blog.risingstack.com/node-js-at-scale-understanding-node-js-event-loop/): This article helps you to understand how the Node.js event loop works, and how you can leverage it to build fast applications. We’ll also discuss the most common problems you might encounter, and the solutions for them.

- [2016-The Node.js Event Loop, Timers, and process.nextTick()](https://parg.co/b1l): The event loop is what allows Node.js to perform non-blocking IO operations — despite the fact that JavaScript is single-threaded — by offloading operations to the system kernel whenever possible.

- [2017-How does Node.js manage timers internally](https://asafdav2.github.io/2017/node-js-timers/)

- [2017-setImmediate() vs nextTick() vs setTimeout(fn,0) – in depth explanation](http://voidcanvas.com/setimmediate-vs-nexttick-vs-settimeout/): And going through official documents of Node may not really be feasible for non-advanced developers. Hence I decided to come up with this article.

# Callback

- [Callback Hell](http://callbackhell.com/)

- [Don't release Zalgo!](https://oren.github.io/blog/zalgo.html)

# Promise

- [2017-How to make the fastest Promise library](https://parg.co/bhz): I have developed Aigle which is a fast Promise library. It is inspired byBluebird. The library is not only a benchmark exercise but a production-ready library that implements the Promise A+ standard, and does so faster than Bluebird.

- [2017-理解 Promise 简单实现的背后原理](http://bupt-hjm.github.io/2017/03/23/study-promise/)

- [2017-A quick guide to JavaScript Promises](https://dev.to/dkundel/a-quick-guide-to-javascript-promises): When you are writing JavaScript, callbacks are one of the most confusing concepts. Promises are the new approach to improve working with async code.

- [2017-ES6 Promises: Patterns and Anti-Patterns](https://parg.co/UYb): Here I’ll lay out a few basic patterns I’ve learned while working with Promises, as well as some gotchas.

- [剖析 Promise 内部结构](https://github.com/xieranmaya/blog/issues/3): 一步一步实现一个完整的、能通过所有 Test case 的 Promise 类。

- [写一个符合 Promises/A+ 规范并可配合 ES7 async/await 使用的 Promise](https://zhuanlan.zhihu.com/p/23312442)

- [Master the JavaScript Interview: What is a Promise?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-promise-27fc71e77261#.yeuxdynfz)

- [2018-Promises are not neutral enough](https://staltz.com/promises-are-not-neutral-enough.html): Promises in JavaScript create problems which affect the entire ecosystem. In this blog post I’ll explain some of those problems.

# Generator

- [2017-Asyncing Feeling about JavaScript Generators](https://www.bignerdranch.com/blog/asyncing-feeling-about-javascript-generators/)

- [2017-The Hidden Power of ES6 Generators: Observable Async Flow Control](https://parg.co/Uhl): In that article, I intentionally sidestepped another major use-case for generators. Arguably, the primary use case: Asynchronous flow control.

# async/await

- [2014-es7-async-functions](https://jakearchibald.com/2014/es7-async-functions/)

- [2017-Await and Async Explained with Diagrams and Examples](http://nikgrozev.com/2017/10/01/async-await/)

- [2017-Even with async/await, raw promises are still key to writing optimal concurrent javascript](https://medium.com/@bluepnume/even-with-async-await-you-probably-still-need-promises-9b259854c161#.w1k2udirb)

- [2017-The 80/20 Guide to Async/Await in Node.js](http://6me.us/jIIzOs)

- [2017-ES7 Async/Await pitfalls](https://medium.com/@matansokolovsky/es7-async-await-pitfalls-d24331388a70#.xkeyncsca)

- [2017-Await and Async Explained with Diagrams and Examples](http://nikgrozev.com/2017/10/01/async-await/#composite-promises)

- [2017-How JavaScript works: Event loop and the rise of Async programming + 5 ways to better coding with async/await](https://parg.co/UGj)

- [2017-Bounce ![code](https://martrix-usa.oss-accelerate.aliyuncs.com/logo/code.svg)](https://github.com/hapijs/bounce): Selective error catching and rewrite rules. [Learning to Throw Again](https://medium.com/@eranhammer/learning-to-throw-again-79b498504d28), [Catching without Awaiting](https://medium.com/@eranhammer/catching-without-awaiting-b2cb7df45790).

- [2017-JavaScript ES 2017: Learn Async/Await by Example](https://parg.co/U6L): Async/Await explained through a clear example.

- [Async Await BIBLE: Sequential, Parallel, Nest, Dynamic and Error Handling in Javascript](http://6me.us/ZMNvVy)

- [asyncawait](https://github.com/yortus/asyncawait#1-introduction)

- [simplifying-asynchronous-coding-es7-async-functions](http://www.sitepoint.com/simplifying-asynchronous-coding-es7-async-functions/)

- [Taming the asynchronous beast with ES7](http://pouchdb.com/2015/03/05/taming-the-async-beast-with-es7.html)

- [Mastering Async Await in Node.js](https://blog.risingstack.com/mastering-async-await-in-nodejs/): In this article, you will learn how you can simplify your callback or Promise based Node.js application with async functions (async/await).

- [2018-Faster async functions and promises](https://v8.dev/blog/fast-async): This article explores how we optimized async functions and promises in V8 (and to some extent in other JavaScript engines as well), and describes how we improved the debugging experience for async code.

# Reactive Programming

- [2017-How to build a reactive engine in JavaScript.](https://parg.co/bhR)
