# Web Architecture List

- [2018-Designing very large (JavaScript) applications](https://medium.com/@cramforce/designing-very-large-javascript-applications-6e013a3291a3): Besides not being open source, I think there is a lot to learn from it and it is worth sharing the things we learned along the way.

- [2017-The MVC Design Pattern in Vanilla JavaScript](https://www.sitepoint.com/mvc-design-pattern-javascript/): The MVC pattern is a design pattern that can stand on its own. The question is, how far can this take us?

- [2020~The Web’s Next Transition](https://www.epicweb.dev/the-webs-next-transition): As the web has evolved, so too has the architecture for the development of these applications. There are many core architectures for building applications for the web these days. The most popular architecture employed by web developers today is the Single Page App (SPA), but we are transitioning to a new and improved architecture for building web applications.

## Case Study

- [2017-重构 Airbnb 前端架构](https://parg.co/bkA)：本文是近日 Airbnb 开发团队在思索重构代码库中 JavaScript 部分的经验总结；本文主要着眼于产品驱动开发以及技术沉淀、从传统的 Rails 架构中积攒的经验以及新的技术栈的某些特性。本文首先介绍了从 Rails 迁移过程中的一些经验，譬如将原本完全的服务端渲染界面所需要的数据切分为了 API 与 Non-API 两大类，并且使用 Hypernova 来进行 React 服务端渲染。然后介绍了如何在应用前端通过引入懒加载与异步加载等方式提升前端性能与用户体验。

# Large-scale Applications

- [2019~How to build a plugin system on the web and also sleep well at night](https://www.figma.com/blog/how-we-built-the-figma-plugin-system/): Since we published this blog post, we decided to change our sandbox implementation to an alternative approach: compiling a JavaScript VM written in C to WebAssembly. As you'll see in the blog post below, it was one of several ideas we originally weighed.
