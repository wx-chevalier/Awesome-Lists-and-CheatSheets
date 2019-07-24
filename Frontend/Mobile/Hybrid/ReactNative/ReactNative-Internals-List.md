[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wx-chevalier/Awesome-Lists)

# React Native Internals List

* [2016-React Native 运行原理解析](http://blog.csdn.net/xiangzhihong8/article/details/52623852)：Facebook 于 2015 年 9 月 15 日推出 react native for Android 版本， 加上 2014 年底已经开源的 IOS 版本，至此 RN (react-native)真正成为跨平台的客户端框架。本篇主要是从分析代码入手，探讨一下 RN 在安卓平台上是如何构建一套 JS 的运行框架。

* [2016-从 iOS 视角解密 React Native 中的线程](http://mp.weixin.qq.com/s/5a83ubJtdg9oJP0lHXeRNA):  在 iOS 开发中，一谈到线程管理，肯定离不开 GCD(Grand Central Dispatch)与 NSOperation/NSOperationQueue 技术选型上的争论。但是 RN 在线程管理是如何选用 GCD 和 NSOperation 的？带着此问题，一起从组件中的线程、JSBundle 加载中的线程以及图片组件中的线程三个方面，逐步看看其中的线程管理细节。

* [2017-React Native Events in Gory Details: What Happens on the Way to Listeners](https://parg.co/UCD): Where we learn about the React native bridge, and realize that React’s central event handling system often gets bypassed…

- [2017-20 分钟理解 React Native For Android 原理](http://6me.us/nNgd): 公司内几个 APP 已经接入并上线了多个 RN 模块，后续规划的定制化需求及性能优化需要我们对 RN 底层原理有更深入的理解。下面通过研读源代码来分析和总结下 Android 中的 RN 实现原理。

- [2018-An In-depth Look Inside React Native](https://parg.co/UD6): Discover how React Native functions internally, and what it does for you without you knowing it.
