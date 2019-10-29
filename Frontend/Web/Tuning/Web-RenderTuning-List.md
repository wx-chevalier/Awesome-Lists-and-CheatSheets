[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wx-chevalier/Awesome-Lists)

# Web Render Tuning List

- [2019-Rendering on the Web](https://developers.google.com/web/updates/2019/02/rendering-on-the-web): The differences between these approaches help illustrate the trade-offs of rendering on the web through the lens of performance.

# Rendering Mechanism | 渲染机制

- [2017-Pulling Back The Curtains on Your Stylesheets](https://medium.freecodecamp.org/its-not-dark-magic-pulling-back-the-curtains-from-your-stylesheets-c8d677fa21b2): My talk (and this post) will focus on the why by taking a deep dive into browser internals to see how our styles are parsed and rendered.

- [浏览器的工作原理：新式网络浏览器幕后揭秘](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/)

- [浅析渲染引擎与前端优化](http://jdc.jd.com/archives/2806)

- [浏览器工作原理](https://segmentfault.com/a/1190000004934730)

- [从输入 URL 到页面加载完成的过程中都发生了什么事情？](http://fex.baidu.com/blog/2014/05/what-happen/)

- [CSDN-开发者应该知道的有关于网页渲染的事](http://www.csdn.net/article/2015-06-12/2824946)

- [JS 一定要放在 Body 的最底部么？聊聊浏览器的渲染机制](http://delai.me/code/js-and-performance/)

- [how-browsers-work](http://taligarsiel.com/Projects/howbrowserswork1.htm)

- [the-rendering-process-of-a-web-page](https://medium.com/@gneutzling/the-rendering-process-of-a-web-page-78e05a6749dc#.zdp2moezo)

- [应该知道的前端性能二三事：Reflow 和 Repaint](http://www.tuicool.com/articles/UvYBfy)

- [2018-How browser rendering works — behind the scenes](https://parg.co/d3A): The purpose of this article is to explain, in very simple terms, the steps your browser takes to convert HTML, CSS and JavaScript into a working website you can interact with.

# Scripting | 脚本解析与执行

- [2019-The cost of JavaScript in 2019](https://v8.dev/blog/cost-of-javascript-2019#json): In 2019, the dominant costs of processing scripts are now download and CPU execution time. User interaction can be delayed if the browser’s main thread is busy executing JavaScript, so optimizing bottlenecks with script execution time and network can be impactful.

- [Planning for Performance](https://www.youtube.com/watch?v=RWLzUnESylc)

- [Solving the Web Performance Crisis by Nolan Lawson](https://twitter.com/MSEdgeDev/status/819985530775404544)

- [JS Parse and Execution Time](https://timkadlec.com/2014/09/js-parse-and-execution-time/)

- [Measuring Javascript Parse and Load](http://carlos.bueno.org/2010/02/measuring-javascript-parse-and-load.html)

- [Unpacking the Black Box: Benchmarking JS Parsing and Execution on Mobile Devices](https://www.safaribooksonline.com/library/view/velocity-conference-new/9781491900406/part78.html)

- [slides](https://speakerdeck.com/desp/unpacking-the-black-box-benchmarking-js-parsing-and-execution-on-mobile-devices))

- [When everything’s important, nothing is!](https://aerotwist.com/blog/when-everything-is-important-nothing-is/)

- [The truth about traditional JavaScript benchmarks](http://benediktmeurer.de/2016/12/16/the-truth-about-traditional-javascript-benchmarks/)

- [Do Browsers Parse JavaScript On Every Page Load](http://stackoverflow.com/questions/1096907/do-browsers-parse-javascript-on-every-page-load/)

- [optimize-js](https://github.com/nolanlawson/optimize-js)

- [lazy-parsing-in-javascript-engines](https://ariya.io/2012/07/lazy-parsing-in-javascript-engines)

- [Turn off negate_iife by default as it hurts V8 performance.](https://github.com/mishoo/UglifyJS2/issues/886)

- [Optimization killers](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers): This document will contain advice to avoid writing code that will perform significantly worse than expected. Specifically those patterns that cause V8 (relevant to Node.JS, Opera, Chromium...) to refuse to optimize the affected function.

- [2017-Optimizing dynamic JavaScript with inline caches](https://parg.co/b4a): This is an overview of an optimization technique I've been using in JSIL for a while, where you create and update polymorphic inline caches in your JavaScript code at runtime so that it can stay fast while adapting to unexpected changes.。( https://parg.co/b4a )

- [2017-Improved JavaScript performance, WebAssembly, and Shared Memory in Microsoft Edge](https://parg.co/bfk)

- [2012:writing-fast-memory-efficient-javascript](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)

- [2016:efficient-javascript](https://medium.com/@xilefmai/efficient-javascript-14a11651d563#.i6494k3bl)

- [2014-Refactoring your JavaScript code with Grasp](http://www.graspjs.com/blog/2014/01/07/refactoring-javascript-with-grasp): Grasp 这个小小的 JavaScript 的命令行重构工具让我们所有人印象深刻。它为抽象语法树提供了丰富的选择器和操作，比摆弄 sed 和 grep 要先进多了。这给我们正在进行的将 JavaScript 做为一等编程语言的运动添加了一个有用的新工具。

- [2016-Butternut #Project# ](https://github.com/Rich-Harris/butternut): The fast, future-friendly minifier.

- [2017-Prepack #Project# ](https://prepack.io/): Prepack is a tool that optimizes JavaScript source code: Computations that can be done at compile-time instead of run-time get eliminated. Prepack replaces the global code of a JavaScript bundle with equivalent code that is a simple sequence of assignments. This gets rid of most intermediate computations and object allocations.

# Layout & Rendering: 界面布局与渲染策略

- [高性能 JavaScript 重排与重绘](http://www.cnblogs.com/zichi/p/4720000.html)

- [improving-your-css-with-parker](http://csswizardry.com/2016/06/improving-your-css-with-parker/)

- [避免大规模、复杂的布局](https://developers.google.com/web/fundamentals/performance/rendering/?hl=zh-cn)

- [一篇文章说清浏览器解析和 CSS(GPU )动画优化](https://segmentfault.com/a/1190000008015671)

- [What forces layout / reflow](https://gist.github.com/paulirish/5d52fb081b3570c81e3a): All of the below properties or methods, when requested/called in JavaScript, will trigger the browser to synchronously calculate the style and layout\*.

# Interaction & Animation | 交互与动画

# CSS

- [2017-高性能动态 CSS 样式](https://parg.co/btW)：本文是对 [JSS](http://cssinjs.org/) 新近提供的[函数式值的介绍](http://cssinjs.org/json-api?v=v7.1.1#function-values)，其与 React 内联样式以及其他 CSS 解决方案相比有数倍的性能提升。在 Web 开发中动态设置样式往往会触发页面的重渲染，而本文则是介绍了如何使用 CSSOM 的 API 来在元素渲染之前即完成样式的设置。

- [fake-it-til-you-make-it-css](https://kyusuf.com/post/fake-it-til-you-make-it-css)

- [You-Dont-Need-Javascript](https://github.com/NamPNQ/You-Dont-Need-Javascript):一些纯粹的基于 CSS 的有趣的小实验

- [CSS Protips:一些关于 CSS 的小建议](https://github.com/AllThingsSmitty/css-protips)
