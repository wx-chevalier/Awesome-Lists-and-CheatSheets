[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wxyyxc1992/Awesome-Lists)

# Web Performance Optimization for Page Loading

* [A Comprehensive Guide to Font Loading Strategies](https://www.zachleat.com/web/comprehensive-webfonts/#abstain)

* [前端渲染加速之 - Big Pipe](http://tech.dianwoda.com/2016/10/26/big-pipe-web-page-rendering-acceleration/)

* [Preload, Prefetch And Priorities in Chrome](https://parg.co/bhM): Today we’ll dive into insights from Chrome’s networking stack to provide clarity on how web loading primitives (like <link rel=“preload”> & <link rel=“prefetch”>) work behind the scenes so you can be more effective with them.

* [2017- 多 “ 维 ” 优化 —— 前端高并发策略的更深层思考](https://parg.co/bIv)：一项指标的变好，总少不了相应优化策略的实施。优化并不是简单的一蹴而就，而是个不断迭代与推翻的过程。更深层的优化方案，往往是在某种思维策略之下，对问题场景和基本策略优缺的深刻理解后做出的当下最优的权衡结果。本文笔者从前端高并发优化这一具体点出发，逐步向大家阐述笔者在优化的 “ 术 ” 之上思维层面的一些思考。希望能给各位带来共鸣和感悟。

* [The Best Request Is No Request, Revisited](https://alistapart.com/article/the-best-request-is-no-request-revisited)

- [How Modern Web Browsers Accelerate Performance: The Networking Layer](https://parg.co/UtY): In this post, we’ll try to analyze what techniques modern browsers employ to automatically boost performance.

# HTTP

## Compression: 压缩

## HTTP/2 Push | HTTP/2 推送

* [2018-Use streaming JSON to speed up your website](https://instantdomainsearch.com/articles/streaming-json-jsons/): JSON streaming—or JSONS—is a simple technique we use to decrease search latency for users, particularly anyone on a slow connection.

## CDN

* [2016-从直播 CDN 的原理说起，谈如何解决延时和连麦的老难题？](https://parg.co/UtK)

* [完结篇：史上最全的 CDN 内容分发网络实战技巧](http://mp.weixin.qq.com/s/a9rxbe8Zj8TZGhTVQPBzyQ)

- [JARE](http://www.jare.io/)

* [jare-instant-free-cdn](http://www.yegor256.com/2016/03/30/jare-instant-free-cdn.html)

# Cache | 缓存优化

# Prefetch | 预抓取

- [2018-Preload, prefetch and other <link> tags](https://3perf.com/blog/link-rels/): Prefetch a CSS file, prerender a full page, or resolve a domain ahead of time – and you won’t have to wait for it when it’s actually needed! Sounds cool.

# Critical Path | 关键渲染路径

## Critical CSS | 关键 CSS

* [critical](https://github.com/addyosmani/critical):Extract & Inline Critical-path CSS in HTML pages

* [critical-path-css-tools](https://github.com/addyosmani/critical-path-css-tools):Tools to help prioritize above-the-fold CSS

* [2017-Remove Unused CSS Rules](https://parg.co/bDk): Removing unused styles can help make the situation more manageable.

* [UnCSS #Project# ](https://github.com/giakki/uncss): UnCSS is a tool that removes unused CSS from your stylesheets. It works across multiple files and supports Javascript-injected CSS.

- [2017-Critical CSS and Webpack: Automatically Minimize Render-Blocking CSS](https://parg.co/bwo)

- [2017-Critical CSS and Webpack: Automatically Minimize Render-Blocking CSS](https://vuejsdevelopers.com/2017/07/24/critical-css-webpack/): Isolating critical CSS is something that can be done programmatically, and in this article I’ll show you how to delegate it to your Webpack pipeline.

- [2018-purgecss #Project#](https://github.com/FullHuman/purgecss): Purgecss analyzes your content and your css files. Then it matches the selectors used in your files with the one in your content files. It removes unused selectors from your css, resulting in smaller css files.

## Lazy Loading | 懒加载

* [2017-Lozad.js #Project# ](https://github.com/ApoorvSaxena/lozad.js): Highly performant, light ~0.5kb and configurable lazy loader in pure JS with no dependencies for images, iframes and more, using IntersectionObserver API

- [2017-How to use SVG as a Placeholder, and Other Image Loading Techniques](https://parg.co/UEY)

## Code Spliting | 代码分割

* [Bundle Buddy #Project#](https://github.com/samccone/bundle-buddy): Bundle Buddy is a tool to help you find source code duplication across your javascript chunks/splits. This enables you to fine tune code splitting parameters to reduce bundle invalidation rates as well as improve repeat page load performance \o/.
