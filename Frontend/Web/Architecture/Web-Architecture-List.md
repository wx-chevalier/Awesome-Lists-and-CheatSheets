# Web Architecture List

- [2018-Designing very large (JavaScript) applications](https://medium.com/@cramforce/designing-very-large-javascript-applications-6e013a3291a3): Besides not being open source, I think there is a lot to learn from it and it is worth sharing the things we learned along the way.

- [2017-The MVC Design Pattern in Vanilla JavaScript](https://www.sitepoint.com/mvc-design-pattern-javascript/): The MVC pattern is a design pattern that can stand on its own. The question is, how far can this take us?

## Case Study

- [2017-重构 Airbnb 前端架构](https://parg.co/bkA)：本文是近日 Airbnb 开发团队在思索重构代码库中 JavaScript 部分的经验总结；本文主要着眼于产品驱动开发以及技术沉淀、从传统的 Rails 架构中积攒的经验以及新的技术栈的某些特性。本文首先介绍了从 Rails 迁移过程中的一些经验，譬如将原本完全的服务端渲染界面所需要的数据切分为了 API 与 Non-API 两大类，并且使用 Hypernova 来进行 React 服务端渲染。然后介绍了如何在应用前端通过引入懒加载与异步加载等方式提升前端性能与用户体验。

# Micro Frontend | 微前端

- [2017-Micro frontends—a microservice approach to front-end web development](https://parg.co/bI7)

- Phodal 系列文章：[实施微前端的六种方式（上）：三种借助路由微服务化前端应用](https://www.phodal.com/blog/implement-microfrontend-apply-route-change/), [实施微前端的六种方式（下）：更好的三种实现方式](https://parg.co/o3W), [前端微服务化方案对比：路由懒加载 vs 子应用模式](https://parg.co/o3g)

- [2019-大前端时代下的微前端架构：实现增量升级、代码解耦、独立部署](https://mp.weixin.qq.com/s/DVkrV_KKE9KaGSeUSenc6w): 本文将介绍前端领域最近的一项变革：单体前端架构正在过渡到许多较小、较易管理的前端架构。

- [2019-Micro Frontends](https://martinfowler.com/articles/micro-frontends.html): In this article we'll describe a recent trend of breaking up frontend monoliths into many smaller, more manageable pieces, and how this architecture can increase the effectiveness and efficiency of teams working on frontend code.

## 基于 iFrame 的微前端方案

- [基于 iframe 的全新微前端方案](https://mp.weixin.qq.com/s/6ioo7xXngaOaWBaqcNFalg): iframe是一个天然的微前端方案，但受限于跨域的严格限制而无法很好的应用，本文介绍一种基于 iframe 的全新微前端方案，继承iframe的优点，补足 iframe 的缺点，让 iframe 焕发新生。

# Large-scale Applications

- [2019-How to build a plugin system on the web and also sleep well at night](https://www.figma.com/blog/how-we-built-the-figma-plugin-system/): Since we published this blog post, we decided to change our sandbox implementation to an alternative approach: compiling a JavaScript VM written in C to WebAssembly. As you'll see in the blog post below, it was one of several ideas we originally weighed.
