# React Internals List | React 内部原理解析

- [2017-React Internals](http://www.mattgreer.org/articles/react-internals-part-one-basic-rendering/): In this five part series, we will “recreate” React from the ground up, learning how it works along the way. Once we’ve finished, you should have a good grasp of how React works, and when and why it calls the various lifecycle methods of a component.

- [2019-React as a UI Runtime](https://overreacted.io/react-as-a-ui-runtime/): This is a deep dive — THIS IS NOT a beginner-friendly post. In this post, I’m describing most of the React programming model from first principles. I don’t explain how to use it — just how it works.

- [React 源码剖析系列 － 解密 setState](https://zhuanlan.zhihu.com/p/20328570?refer=purerender)

- [为什么 setState 没有立即执行](http://www.jianshu.com/p/2d50a413e74a)

- [拆解 setState[一][一源看世界][之 React]](http://www.jianshu.com/p/47f24add2b5e)

# Virtual DOM

- [2013-Performance Calendar: React’s diff algorithm](http://calendar.perfplanet.com/2013/diff/)

- [2017-react diff 原理](https://cloud.tencent.com/community/article/654179001489391651?fromSource=gwzcw.114428.114428.114428)：React diff 作为 Virtual DOM 的加速器，其算法上的改进优化是 React 整个界面渲染的基础，以及性能提高的保障，同时也是 React 源码中最神秘、最不可思议的部分，本文将剖析 React diff 的不可思议之处。

- [React 源码剖析系列，不可思议的 react diff](https://zhuanlan.zhihu.com/p/20346379?refer=purerender)

- [React 源码剖析系列 － 解密 setState](https://zhuanlan.zhihu.com/p/20328570?refer=purerender)

- [深入浅出 React(四)：虚拟 DOM Diff 算法解析](http://www.infoq.com/cn/articles/react-dom-diff)

- [ReactJS | Learning Virtual DOM and React Diff Algorithm](http://www.oyecode.com/2015/09/reactjs-learning-virtual-dom-and-react.html)

- [So-You-Want-To-Be-A-Functional-Programmer](http://62f7d6c2.fromwiz.com/share/s/1yZZr21Yv4w42GorJm0oBXEi3AKTQa3rcARz2nKoQ71RpX_Z)

- [React’s diff algorithm](http://calendar.perfplanet.com/2013/diff/)

- [virtual-dom](https://github.com/Matt-Esch/virtual-dom)

- [The Secrets of React’s virtual DOM](http://fluentconf.com/fluent2014/public/schedule/detail/32395)

- [Why is React’s concept of virtual DOM said to be moreperformant than dirty model checking?](http://stackoverflow.com/questions/21109361/why-is-reacts-concept-of-virtual-dom-said-to-be-more-performant-than-dirty-mode)

# Component System | 组件系统

- [The React and React Native Event System Explained: A Harmonious Coexistence](https://parg.co/UDq): You’re using it. You’re liking it. But did you know what React’s event handler is doing under the hood?

# Stack Reconciler

- [2017-RFClarification: why is `setState` asynchronous?](https://parg.co/Uid)

- [Dive into setState() method in React](https://gist.github.com/ajhsu/e259392f06aa8e3bf5c9)

- [Dive into React codebase: Handling state changes](http://reactkungfu.com/2016/03/dive-into-react-codebase-handling-state-changes/)

- [2017-react-reconciler-demo ![code](https://shorturl.at/dlxyK) ](https://github.com/lukebelliveau/react-reconciler-demo): A simple implementation of React's stack reconciler. This is much different from the real implementation, but demonstrates the concepts.

- [ON THE ASYNC NATURE OF `SETSTATE` IN REACT](http://thereignn.ghost.io/on-the-async-nature-of-setstate-in-react/)

# Fiber

- [2017-React Fiber resources 🗃️](https://github.com/koba04/react-fiber-resources): This is for resources for React Fiber.

- [2017-A look inside React Fiber - how work will get done.](http://makersden.io/blog/look-inside-fiber/): This post will go outside-in - starting from calling the render function in client JS and changing state of a component, down to describing the steps taken by Fiber to do all the work.

- [2017-React Fiber Architecture](https://github.com/acdlite/react-fiber-architecture): A description of React's new core algorithm, React Fiber.

- [2017-React 的新引擎 — React Fiber 是什么？](https://parg.co/bgb)：稍有经验的前端工程师会知道，页面的 DOM 改变，就会导致页面重新计算 DOM，进行重绘或者重排，DOM 结构复杂或者频繁操作 DOM 通常是性能瓶颈产生的原因。而网站从最开始比较简单，开始变的越来越复杂，用户交互也会越来越多，怎么去减轻 DOM 操作带来的性能损耗就变得重要起来。

- [2017-React Fiber 是什么](https://zhuanlan.zhihu.com/p/26027085)：React Fiber 这个大改变 Facebook 已经折腾两年多了，刚刚结束不久的 React Conf 2017 会议上，Facebook 终于确认，React Fiber 会搭上 React 下一个大版本 v16 的顺风车发布。

- [2017-React 新引擎 React Fiber 究竟要解决什么问题？](https://parg.co/btw): Facebook 正在以流行的 JavaScript 框架 React 为基础开发一个全新的架构。这个名为 React Fiber 的全新设计改变了检测变更的方法和时机，借此可改进浏览器端和其他渲染设备的响应速度。这一 全新架构 最初已于 2016 年 7 月公开发布，其中蕴含着过去多年来 Facebook 不断改进的工作成果。该架构可向后兼容，彻底重写了 React 的协调(Reconciliation )算法。该过程可用于确定出现变更的具体时间，并将变更传递给渲染器。

- [2017-React Conf: A Cartoon Intro to Fiber](https://www.youtube.com/watch?v=ZCuYPiUIONs)

- [react-fiber-architecture](https://github.com/acdlite/react-fiber-architecture)

- [Didact Fiber: Incremental reconciliation](https://parg.co/UW5): In this post we are going to rewrite most of the code from the didact series to follow React 16 new architecture.

## Async Rendering

- [2018-Beyond React 16: Time Slicing and Suspense API](https://auth0.com/blog/time-slice-suspense-react16/): Learn what's coming to ReactJS. Get a sneak peek of the powerful features that will grace ReactJS soon.

- [2018-React suspense and server rendering](https://blogg.svt.se/svti/react-suspense-server-rendering/): The recently revealed React suspense functionality has the potential to solve a lot of the current pain points in server rendering.

- [2018-Understanding React “Suspense”](https://medium.com/@baphemot/understanding-react-suspense-1c73b4b0b1e6): In short: the new feature allows you to defer rendering part of your application tree until some condition is met (for example data from an endpoint or a resource is loaded).

- [2018-A Walkthrough of _that_ React Suspense Demo](https://dev.to/swyx/a-walkthrough-of-that-react-suspense-demo--4j6a):I'm a recent bootcamp grad. You're not reading the divinings of some thought leader here. I'm just some guy learning in public.
