[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wxyyxc1992/Awesome-Links)

# Node.js Syntax Links

* [Node.js 如何解析 Form 上传？](https://mp.weixin.qq.com/s/pJ6yVvcuFWROmuFU1ULXeQ): 作者前段时间遇到了一个需要手动解析 Form 表单上传的机会，也借此为各位解析一下 Node.js 解析 Form 上传的实现细节。

# Core Modules: 核心模块

* [2017-Mastering the Node.js Core Modules - The File System & fs Module](https://blog.risingstack.com/mastering-the-nodejs-core-modules-file-system-fs-module/): In this article, we'll take a look at the File System core module, File Streams and some fs module alternatives.

## Event Loop

* [2016-Understanding the Node.js Event Loop](https://blog.risingstack.com/node-js-at-scale-understanding-node-js-event-loop/): This article helps you to understand how the Node.js event loop works, and how you can leverage it to build fast applications. We’ll also discuss the most common problems you might encounter, and the solutions for them.

* [2016-The Node.js Event Loop, Timers, and process.nextTick()](https://parg.co/b1l): The event loop is what allows Node.js to perform non-blocking I/O operations — despite the fact that JavaScript is single-threaded — by offloading operations to the system kernel whenever possible.

## Modularity: 模块机制

* [2011- 深入 Node.js 的模块机制](http://www.infoq.com/cn/articles/nodejs-module-mechanism)

- [2017-Requiring modules in Node.js: Everything you need to know](https://parg.co/bQl)

## Stream | 流

* [2015-stream-handbook](https://github.com/substack/stream-handbook): This document covers the basics of how to write node.js programs with streams.

* [2017-Node.js Streams: Everything you need to know](https://parg.co/bJN): Node.js streams have a reputation for being hard to work with, and even harder to understand. Well I’ve got good news for you — that’s no longer the case. Over the years, developers created lots of packages out there with the sole purpose of making working with streams easier. But in this article, I’m going to focus on the native Node.js stream API.

- [2017-深入理解 Node Stream 内部机制](http://www.barretlee.com/blog/2017/06/06/dive-to-nodejs-at-stream-module/)：相信很多人对 Node 的 Stream 已经不陌生了，不论是请求流、响应流、文件流还是 socket 流，这些流的底层都是使用 stream 模块封装的，甚至我们平时用的最多的 console.log 打印日志也使用了它，不信你打开 Node runtime 的源码。

* [2017-A Brief History of Node Streams #Series#](http://6me.us/cC9Jcm): This post takes a look at what streams are and do, while providing some examples along the way.

- [2017-Do you want a better understanding of Buffer in Node.js? Check this out.](https://medium.freecodecamp.org/do-you-want-a-better-understanding-of-buffer-in-node-js-check-this-out-2e29de2968e8)

- [2017-Video stream with Node.js and HTML5](https://medium.com/@daspinola/video-stream-with-node-js-and-html5-320b3191a6b6): The “challenge” was to make a route sending a .mp4 file to a page and make the video available to be seen.

- [2017-Something about Buffer](https://hackernoon.com/nodejs-javasript-react-buffer-understand-tutorial-example-easy-step-create-read-utf8-ce37866ddd8c): In node.js a buffer is a container for raw bytes.

# Command Line

* 命令行辅助参数解析：[yargs #Project# ](https://github.com/yargs/yargs)、[Inquirer.js #Project# ](https://github.com/SBoudrias/Inquirer.js)

* [pkg #Project# ](https://github.com/zeit/pkg): Package your Node.js project into an executable.

* [2017-Creating a project generator with Node](https://parg.co/byo): In this post, I’ll walk you through how to create a simple project generator built with NodeJS that can be installed globally on your computer and used to create a starter project wherever you want, whenever you want.

- [ora #Project#](https://github.com/sindresorhus/ora): Elegant terminal spinner

- [Backpressuring in Streams](https://nodejs.org/en/docs/guides/backpressuring-in-streams/): The purpose of this guide is to further detail what backpressure is, and how exactly streams address this in Node.js' source code.

# Storage

## MySQL

## ORM

## Redis

* [node_redis #Project#](https://github.com/NodeRedis/node_redis): This is a complete and feature rich Redis client for node.js. It supports all Redis commands and focuses on high performance.

* [ioredis #Project#](https://github.com/luin/ioredis): A robust, performance-focused and full-featured Redis client for Node and io.js.

* [Radredis #Project#](https://github.com/bustle/radredis): Radredis is a node data adapter for redis. It is not a full ORM but a simple opinionated interface for storing application data in redis.

# 权限认证

* [Node Hero - Node.js Authentication using Passport.js](https://parg.co/UqY)

# HTTP/2

* [2017-How to create a zero dependency HTTP/2 static file server with Node.js (with examples)](https://parg.co/UKq)
