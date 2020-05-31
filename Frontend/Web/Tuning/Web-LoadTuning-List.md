# Web Performance Optimization for Page Loading

- [A Comprehensive Guide to Font Loading Strategies](https://www.zachleat.com/web/comprehensive-webfonts/#abstain)

- [前端渲染加速之 - Big Pipe](http://tech.dianwoda.com/2016/10/26/big-pipe-web-page-rendering-acceleration/)

- [Preload, Prefetch And Priorities in Chrome](https://parg.co/bhM): Today we’ll dive into insights from Chrome’s networking stack to provide clarity on how web loading primitives (like <link rel=“preload”> & <link rel=“prefetch”>) work behind the scenes so you can be more effective with them.

- [2017- 多 “ 维 ” 优化：前端高并发策略的更深层思考](https://parg.co/bIv)：一项指标的变好，总少不了相应优化策略的实施。优化并不是简单的一蹴而就，而是个不断迭代与推翻的过程。更深层的优化方案，往往是在某种思维策略之下，对问题场景和基本策略优缺的深刻理解后做出的当下最优的权衡结果。本文笔者从前端高并发优化这一具体点出发，逐步向大家阐述笔者在优化的 “ 术 ” 之上思维层面的一些思考。希望能给各位带来共鸣和感悟。

- [The Best Request Is No Request, Revisited](https://alistapart.com/article/the-best-request-is-no-request-revisited)

- [How Modern Web Browsers Accelerate Performance: The Networking Layer](https://parg.co/UtY): In this post, we’ll try to analyze what techniques modern browsers employ to automatically boost performance.

# HTTP

## Compression: 压缩

## HTTP/2 Push | HTTP/2 推送

- [2018-Use streaming JSON to speed up your website](https://instantdomainsearch.com/articles/streaming-json-jsons/): JSON streaming—or JSONS—is a simple technique we use to decrease search latency for users, particularly anyone on a slow connection.

# CDN

- [2016-从直播 CDN 的原理说起，谈如何解决延时和连麦的老难题？](https://parg.co/UtK)

- [完结篇：史上最全的 CDN 内容分发网络实战技巧](http://mp.weixin.qq.com/s/a9rxbe8Zj8TZGhTVQPBzyQ)

- [JARE](http://www.jare.io/)

- [jare-instant-free-cdn](http://www.yegor256.com/2016/03/30/jare-instant-free-cdn.html)

## Edge Compiting

- [2020-边缘加载](https://mp.weixin.qq.com/s/8Nig2vYMUmtcEw0A7jt1yA): 淘宝是如何缩短首屏时间、降低服务器压力的？边缘计算告诉你答案！

# Cache | 缓存优化

# Prefetch | 预抓取

- [2018-Preload, prefetch and other <link> tags](https://3perf.com/blog/link-rels/): Prefetch a CSS file, prerender a full page, or resolve a domain ahead of time – and you won’t have to wait for it when it’s actually needed! Sounds cool.

# Critical Path | 关键渲染路径

## Critical CSS | 关键 CSS

- [critical](https://github.com/addyosmani/critical):Extract & Inline Critical-path CSS in HTML pages

- [critical-path-css-tools](https://github.com/addyosmani/critical-path-css-tools):Tools to help prioritize above-the-fold CSS

- [2017-Remove Unused CSS Rules](https://parg.co/bDk): Removing unused styles can help make the situation more manageable.

- [UnCSS #Project# ](https://github.com/giakki/uncss): UnCSS is a tool that removes unused CSS from your stylesheets. It works across multiple files and supports Javascript-injected CSS.

- [2017-Critical CSS and Webpack: Automatically Minimize Render-Blocking CSS](https://parg.co/bwo)

- [2017-Critical CSS and Webpack: Automatically Minimize Render-Blocking CSS](https://vuejsdevelopers.com/2017/07/24/critical-css-webpack/): Isolating critical CSS is something that can be done programmatically, and in this article I’ll show you how to delegate it to your Webpack pipeline.

- [2018-purgecss #Project#](https://github.com/FullHuman/purgecss): Purgecss analyzes your content and your css files. Then it matches the selectors used in your files with the one in your content files. It removes unused selectors from your css, resulting in smaller css files.

## Lazy Loading | 懒加载

- [2017-Lozad.js #Project# ](https://github.com/ApoorvSaxena/lozad.js): Highly performant, light ~0.5kb and configurable lazy loader in pure JS with no dependencies for images, iframes and more, using IntersectionObserver API

- [2017-How to use SVG as a Placeholder, and Other Image Loading Techniques](https://parg.co/UEY)

## Code Spliting | 代码分割

- [Bundle Buddy #Project#](https://github.com/samccone/bundle-buddy): Bundle Buddy is a tool to help you find source code duplication across your javascript chunks/splits. This enables you to fine tune code splitting parameters to reduce bundle invalidation rates as well as improve repeat page load performance \o/.

- [2018-Web Performance Optimization with Webpack by Addy Osmani](https://parg.co/UXN): Taking advantage of its features for optimizing modern code, code-splitting scripts into critical and non-critical pieces and stripping out unused code.

- [腾讯社交网络图片带宽优化技术演进之路](https://parg.co/Ua4): 为进一步降低运营带宽成本，减小用户访问流量及提升页面加载速度，社交网络 CDN 运维紧跟行业图片优化趋势，创新引入 WebP、SharpP、自适应分辨率、Guetzli 等图像压缩技术到现网，经过三年多的多部门联合攻关，已逐渐形成一套覆盖全图片类型(JPEG、JPG、PNG、WebP、GIF)多场景的图片压缩运营体系，适用于各类型终端，每年节约外网带宽几百 G。

# Image Optimization: 图片优化

- [2017-Essential Image Optimization](https://images.guide/): In 2017, image optimization should be automated. It's easy to forget, best practices change, and content that doesn't go through a build pipeline can easily slip.

- [2017-An Introduction to Progressive Image Rendering](https://parg.co/bLp): In this article, we’ll look at how you can save your users bandwidth and time by loading and rendering well-optimized images lazily and progressively.

- [2017-Reducing Image File Size at Etsy](https://parg.co/bvn): Serving images is a critical part of Etsy’s infrastructure.

- [Save time by transforming images in the command line](http://6me.us/WYOP1)

- [2017-Network based image loading using the Network Information API in Service Worker](https://parg.co/U5N): Recently, Chromium improved their implementation of navigator.connection by adding three new attributes: effectiveType, downlink and rtt.

- [SuperTinyIcons #Project#](https://github.com/edent/SuperTinyIcons):Under 1KB each! Super Tiny Icons are miniscule SVG versions of your favourite website and app logos

## JPEG

- [reducing-jpg-file-size](https://medium.com/@duhroach/reducing-jpg-file-size-e5b27df3257c#.jdegycys9)

- [reducing-png-file-size](https://medium.com/@duhroach/reducing-png-file-size-8473480d0476#.pxfmpayr1)

## WebP

- [使用 webP 减少图片的大小](http://www.tuicool.com/articles/euAJv2Z)

- [探究 WebP 一些事儿](https://aotu.io/notes/2016/06/23/explore-something-of-webp/)

- [Front End Optimization – 9 Tips to Improve Web Performance](https://www.keycdn.com/blog/front-end-optimization/)

- [Optimising the front end for the browser](https://hackernoon.com/optimising-the-front-end-for-the-browser-f2f51a29c572?source=reading_list---------1-1---------)

- [渲染性能](https://github.com/sundway/blog/issues/2)

- [Web App 性能优化之亮剑](http://insights.thoughtworkers.org/web-apps-performance-optimization/)

- [web-performance-secrets-from-the-bbc](https://medium.com/net-magazine/web-performance-secrets-from-the-bbc-d4b01f869752#.hwhq6jcbn)

- [2017-Developer's Guide to E-Commerce Sites Speed Optimization](https://parg.co/U6q): You need to optimize your e-commerce website for speed at a time when search engines themselves rank faster websites above slower ones. At that same time, audience's attention span is getting shorter by the day.

# Font

# 响应式图片

- [Image Compression for Web Developers](http://www.html5rocks.com/en/tutorials/speed/img-compression/)

- [responsive-images-client-hints](https://davidwalsh.name/responsive-images-client-hints)

- [quick-guide-responsive-images](http://slicejack.com/quick-guide-responsive-images/)

- [responsive-images-done-right-guide-picture-srcset](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/)

- [Picturefill #Project#](https://github.com/scottjehl/picturefill)

- [2017-Fundamentals of Responsive Images](https://www.lullabot.com/articles/fundamentals-of-responsive-images): In this article, I’ll be explaining some of the key concepts for responsive images, as well as providing an overview of a few different responsive image tactics.
