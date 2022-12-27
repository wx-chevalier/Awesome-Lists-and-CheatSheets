# Webpack Learning & Practices List

- [前端缓存策略与基于 Webpack 的静态资源版本管理](https://zhuanlan.zhihu.com/p/24954527)

- [大公司里怎样开发和部署前端代码](https://github.com/fouber/blog/issues/6)。

- [2017-Webpack HMR 原理解析](https://zhuanlan.zhihu.com/p/30669007): Hot Module Replacement（以下简称 HMR）是 webpack 发展至今引入的最令人兴奋的特性之一。

# Resource | 资源

## Book | 书籍

- [SurviveJS Webpack 📚](https://survivejs.com/webpack/): SurviveJS - Webpack is meant for beginner to intermediate users of webpack.

- [Practical Module Federation 📚](https://ngte.cowtransfer.com/s/77b881e3669847): Module Federation is an advanced use topic for the Webpack bundler starting with version 5.

## Tutorial | 教程

- [2016-Getting Started with Webpack 2](https://blog.madewithenvy.com/getting-started-with-webpack-2-ed2b86c68783#.3ksiast1f): At its simplest, webpack is a module bundler for your JavaScript. However, since its release it’s evolved into a manager of all your front-end code.

- [2017-Intro To Webpack](https://medium.com/@kimberleycook/intro-to-webpack-1d035a47028d?source=linkShare-fe48c4221a4c-1482154145): Webpack is a very complex tool, and most people do not need to know how every part of it works.

- [2017-How to setup Webpack +2.0 from scratch in 2017 #Series#](https://medium.com/@wesharehoodies/simple-beginner-guide-for-webpack-2-0-from-scratch-part-v-495dba627718)

- [2017-Webpack: A Detailed Introduction](https://www.smashingmagazine.com/2017/02/a-detailed-introduction-to-webpack/): JavaScript module bundling has been around for a while. RequireJS had its first commits in 2009, then Browserify made its debut, and since then several other bundlers have spawned across the Internet. Among that group, webpack has jumped out as one of the best. If you’re not familiar with it, I hope this article will get you started with this powerful tool.

- [WEBPACK - THE GOOD PARTS](https://presentations.survivejs.com/webpack-the-good-parts/#/00): What is Webpack, Developing, Building, Assets, Bundle/code Splitting, Analysis, Optimizing.

- [2018-Webpack Basics](https://dev.to/kayis/webpack-basics): Many people seem to like Webpack and use it for their everyday web bundling process.

# Configuration: 基础配置

## Modularity: 模块化

- [2017-Brief introduction to scope hoisting in Webpack](https://parg.co/beE): On its third major release, Webpack introduced a new feature: scope hoisting. Many developers are already exposing data showing great positive impacts on the initial execution time of their bundles.

## Build Performance: 构建性能优化

- [2016-Optimizing Webpack build times and improving caching with DLL bundles](https://robertknight.github.io/posts/webpack-dll-plugins/)

- [Keep webpack Fast: A Field Guide for Better Build Performance](https://parg.co/UkI): This post is a field guide offering up what we learned on our path towards a faster build.

- [HappyPack ![code](https://shorturl.at/dlxyK)](https://github.com/amireh/happypack): HappyPack makes webpack builds faster by allowing you to transform multiple files in parallel.

- [AutoDllPlugin ![code](https://shorturl.at/dlxyK)](https://parg.co/Uka): Webpack's DllPlugin without the boilerplate.

- [HardSourceWebpackPlugin ![code](https://shorturl.at/dlxyK)](https://parg.co/Uk1): HardSourceWebpackPlugin is a plugin for webpack to provide an intermediate caching step for modules.

- [parallel-webpack ![code](https://shorturl.at/dlxyK)](https://parg.co/UkW): Builds multi-config webpack projects in parallel.

# Production | 发布到生产环境

- [2017-Reducing CSS bundle size 70% by cutting the class names and using scope isolation](https://parg.co/b19)

- [2017-webpack for real tasks: bundling front-end and adding compilation #Series#](https://iamakulov.com/notes/all/webpack-for-real-tasks-part-1/): Bundling front-end and adding compilation ,Decreasing front-end size and improving caching, Speeding up build and improving the development workflow

- [基于 Webpack 搭建前端工程解决方案探索](http://www.infoq.com/cn/articles/frontend-engineering-webpack)

- [基于 Webpack 的前端资源构建方案](http://lifei.github.io/2015/12/20/webpack/#___8)

- [Web Performance Optimization with Webpack by Addy Osmani](https://parg.co/UXN): Taking advantage of its features for optimizing modern code, code-splitting scripts into critical and non-critical pieces and stripping out unused code.

## Code Split | 代码分割

- [2017-Vendor and code splitting in webpack 2](https://medium.com/@adamrackis/vendor-and-code-splitting-in-webpack-2-6376358f1923#.4ma6usgf0)

- [2017-webpack bits: Getting the most out of the CommonsChunkPlugin()](https://parg.co/bQb):

- [2017-How to use Webpack’s new “magic comment” feature with React Universal Component + SSR](https://parg.co/b9A): Webpack 2.4.0, which came out a few weeks ago, launched with a very interesting new feature: “magic comments.” In combination with dynamic imports, “magic comments” greatly simplify code-splitting + server-side rendering.

- [2018-RIP CommonsChunkPlugin](https://parg.co/Ukz): webpack 4 removes the CommonsChunkPlugin in favor of two new options (optimization.splitChunks and optimization.runtimeChunk). Here is how it works.

# OpenSource

- [2018-size-plugin ![code](https://shorturl.at/dlxyK)](https://github.com/GoogleChromeLabs/size-plugin): Prints the gzipped sizes of your webpack assets and the changes since the last build.

## 监控

- [Webpack Dashboard ![code](https://shorturl.at/dlxyK)](https://github.com/FormidableLabs/webpack-dashboard): A CLI dashboard for webpack dev server. 如果是 Windows 下的开发者可以优先使用 [electron-webpack-dashboard](https://github.com/FormidableLabs/electron-webpack-dashboard)

- [Webpack Monitor ![code](https://shorturl.at/dlxyK)](https://github.com/webpackmonitor/webpackmonitor): A tool for monitoring webpack optimization metrics through the development process

- [JARVIS ![code](https://shorturl.at/dlxyK)](https://github.com/zouhir/jarvis): J.A.R.V.I.S. (Just A Rather Very Intelligent System) will put in your browser all the relevant information you need from your webpack build whether in dev or in prod.

- [Webpack Bundle Analyzer ![code](https://shorturl.at/dlxyK) ](https://github.com/th0r/webpack-bundle-analyzer): Webpack plugin and CLI utility that represents bundle content as convenient interactive zoomable treemap.

## 应用优化

- [preload-webpack-plugin](https://github.com/googlechrome/preload-webpack-plugin): A Webpack plugin for wiring up link `<rel='preload'>` (and prefetch) - supports async chunks

# Internals

- [2017-Webpack HMR 原理解析](https://zhuanlan.zhihu.com/p/30669007/)

- [2019-Webpack 是怎样运行的?](https://mp.weixin.qq.com/s/uc4fVViv4u86TTX2XsMgFA): 下面我们来通过一个简单的项目来看一下 Webpack 是怎样运行的。
