[![返回目录](https://user-images.githubusercontent.com/5803001/38079637-ff0abcf0-3371-11e8-9b76-ad651620afc7.jpg)](https://github.com/wx-chevalier/Awesome-Lists)

# DOM 事件处理资料索引

- [移动 Web 之触摸和指针事件详解](http://www.infoq.com/cn/articles/touch-pointer-event)

- [阮一峰 JavaScript 标准参考教材之 DOM 中的事件](http://javascript.ruanyifeng.com/dom/event.html#toc43)

- [前端进阶之路：点击事件绑定](https://github.com/cssmagic/blog/issues/48)

- [如何让 H5 体验接近 APP：(一)触摸反馈](https://segmentfault.com/a/1190000006864910)

# Event Handle

## Event Delegation

- [JavaScript 事件冒泡与事件捕获](http://www.cnblogs.com/zichi/p/4713038.html)

- [How JavaScript Event Delegation Works](http://davidwalsh.name/event-delegate)

- [Event Delegation versus Event Handling](http://icant.co.uk/sandbox/eventdelegation/)

- [jQuery.delegate](http://api.jquery.com/delegate/) is event delegation + selector specification

- [jQuery.on](http://api.jquery.com/on/#direct-and-delegated-events) uses event delegation when passed a selector as the 2nd parameter

- [Event delegation without a JavaScript library](http://web.archive.org/web/20090420170842/http://usabletype.com/weblog/event-delegation-without-javascript-library/)

- [Closures vs Event delegation](http://lists.evolt.org/archive/Week-of-Mon-20090209/127339.html): takes a look at the pros of _not_ converting code to use event delegation

- Interesting approach PPK uncovered for [delegating the `focus` and `blur` events](http://www.quirksmode.org/blog/archives/2008/04/delegating_the.html) (which do *not*bubble)

# Event Type

## Touch Event

- [Introduction to Touch events in JavaScript](http://www.javascriptkit.com/javatutors/touchevents.shtml)

## DnD | 拖拽事件

- [2015-dragula](https://github.com/bevacqua/dragula): Drag and drop so simple it hurts

- [Rethinking drag and drop Taking something basic and making it beautiful](https://medium.com/@alexandereardon/rethinking-drag-and-drop-d9f5770b4e6b)

- [2010-Native HTML5 Drag and Drop](https://www.html5rocks.com/en/tutorials/dnd/basics/): Drag and drop (DnD) is a first class citizen in HTML5! The spec defines an event-based mechanism, JavaScript API, and additional markup for declaring that just about any type of element be draggable on a page.

- [超小 Web 手势库 AlloyFinger 原理](http://www.cnblogs.com/iamzhanglei/p/6053235.html)

# Scroll & Visibility: 滚动事件与可见性

- [Complexities of an Infinite Scroller](https://developers.google.com/web/updates/2016/07/infinite-scroller)

- [react-springy-parallax](https://github.com/drcmda/react-springy-parallax): A springy, composable parallax-scroller for React.

- [react-waypoint](https://github.com/brigade/react-waypoint): A React component to execute a function whenever you scroll to an element. Works in all containers that can scroll, including the window.

- [Lucifier129: pull-element](https://github.com/Lucifier129/pull-element): Lightweight, high-performance and smooth pull element effect that support all directions

- [移动 Web 滚动性能优化: Passive event listeners](https://zhuanlan.zhihu.com/p/24555031)

- [iScroll #Project#](http://iscrolljs.com/#whos):高性能的多平台 JS 滚动条

- [React-iScroll #Project#](https://github.com/schovi/react-iscroll)

- [jquery.nicescroll](https://github.com/inuyaksa/jquery.nicescroll):基于 jQuery 的滚动插件

## Parallaxing

- [2016-Performant Parallaxing](https://developers.google.com/web/updates/2016/12/performant-parallaxing): In this article we’ll discuss a solution that is both performant and, just as importantly, works cross-browser

## ScrollSpy | 滚动监听

- [React Visibility Sensor #Project#](https://github.com/joshwnj/react-visibility-sensor): Sensor component for React that notifies you when it goes in or out of the window viewport.

- [Build a Custom JavaScript Scrollspy Navigation](https://scotch.io/tutorials/build-a-custom-javascript-scrollspy-navigation)

- [InView](https://github.com/camwiegert/in-view): 自动判断某个元素是否在 ViewPort 内

# Observer

## IntersectionObserver

- [2017-IntersectionObserver’s Coming into View](https://developers.google.com/web/updates/2016/04/intersectionobserver): Making this visibility test more efficient is what IntersectionObserver was designed for.

- [2018-Now You See Me: How To Defer, Lazy-Load And Act With IntersectionObserver](https://parg.co/Uiu): In this article, we are going to go out of the scroll darkness and talk about the modern way of lazy-loading resources.

## MutationObserver

- [How JavaScript works: tracking changes in the DOM using MutationObserver](https://parg.co/UzY)
