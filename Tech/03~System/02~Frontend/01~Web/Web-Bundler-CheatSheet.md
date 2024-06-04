题注：[Web Bundler CheatSheet](https://parg.co/YO2) 属于 [Awesome-CheatSheet](https://github.com/wx-chevalier/Awesome-CheatSheets) 系列，盘点数个常用的开发打包工具清单。欢迎加入阿里南京前端团队，欢迎关注[阿里南京技术专刊](https://zhuanlan.zhihu.com/ali-nanjing)了解更多讯息。

# Web Bundler CheatSheet | Web 构建与打包工具盘点

工欲善其事，必先利其器，当我们准备开始某个 Web 相关的项目时，合适的脚手架会让我们事半功倍。在 [2016~我的前端之路：工具化与工程化](https://parg.co/YOg)一文中，我们讨论了工具化与工程化相关的内容，其中重要的章节就是关于所谓的打包工具。Grunt、Glup 属于 Task Runner，即任务执行器；实际上，npm package.json 中定义的脚本也可以看做 Task Runner，而 Rollup，Parcel 以及 Webpack 则是属于 Bundler，即打包工具。

![webpack](https://user-images.githubusercontent.com/5803001/39966649-02e751a6-56e2-11e8-8af1-bbbd47aa7dbb.png)

尺有所短，寸有所长，不同的构建工具有其不同的适用场景。Webpack 是非常优秀的构建与打包工具，但是其提供了基础且复杂的功能支持，使得并不适用于全部的场景。Parcel 这样的零配置打包工具适合于应用型的原型项目构建，而 Rollup 或者 Microbundle 适合于库的打包，Backpack 则能够帮我们快速构建 Node.js 项目。笔者在本文中列举讨论的仅是日常工作中会使用的工具，更多的 [Browserify](https://github.com/browserify/browserify)、[Fusebox](https://github.com/fuse-box/fuse-box) 等等构建工具查看 [Web 构建与打包工具资料索引](https://parg.co/Uss)或者[现代 Web 开发实战/进阶篇](https://github.com/wx-chevalier/Web-Notes)。

# NPM & Yarn

```sh
yarn config set registry https://registry.npm.taobao.org -g
yarn config set disturl https://npm.taobao.org/dist -g
yarn config set electron_mirror https://npm.taobao.org/mirrors/electron/ -g
yarn config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/ -g
yarn config set phantomjs_cdnurl https://npm.taobao.org/mirrors/phantomjs/ -g
yarn config set chromedriver_cdnurl https://cdn.npm.taobao.org/dist/chromedriver -g
yarn config set operadriver_cdnurl https://cdn.npm.taobao.org/dist/operadriver -g
yarn config set fse_binary_host_mirror https://npm.taobao.org/mirrors/fsevents -g
```

# Parcel

Parcel 是著名的零配置的应用打包工具，在 [TensorFlowJS](https://github.com/wx-chevalier/AIDL-Workbench) 或者 [gh-craft](https://github.com/wx-chevalier/xCompass/blob/master/x-home/gh-craft/README.md) 等算法实验/游戏场景构建中，都能够快速地搭建应用。

```sh
# 安装 Parcel
$ npm install -g parcel-bundler

# 启动开发服务器
$ parcel index.html

# 执行线上编译
$ parcel build index.js

# 指定编译路径
$ parcel build index.js -d build/output
```

Parcel 会为我们自动地下载安装依赖，并且内置了 ES、SCSS 等常见的处理器。在 [fe-boilerplate](https://github.com/wx-chevalier/fe-boilerplates/) 中提供了 [React](https://github.com/wx-chevalier/fe-boilerplates/blob/master/react/parcel), [React & TypeScript](https://github.com/wx-chevalier/fe-boilerplates/blob/master/react/parcel-ts), [Vue.js](https://github.com/wx-chevalier/fe-boilerplates/blob/master/vue/parcel) 等 Parcel 常见的示例，这里以 React 为例，首先定义组件与渲染：

```js
// index.js
import React from "react";
import ReactDOM from "react-dom";
import logo from "../public/logo.svg";
import "./index.css";

const App = () => (
  <div className="App">
    <img className="App-Logo" src={logo} alt="React Logo" />
    <h1 className="App-Title">Hello Parcel x React</h1>
  </div>
);

ReactDOM.render(<App />, document.getElementById("root"));

// Hot Module Replacement
if (module.hot) {
  module.hot.accept();
}
```

然后定义入口的 index.html 文件：

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Parcel React Example</title>
  </head>

  <body>
    <div id="root"></div>
    <script src="./index.js"></script>
  </body>
</html>
```

然后使用 `parcel index.html` 运行开发服务器即可。Parcel 中同样也是支持异步加载的，假设我们将部分代码定义在 someModule.js 文件中，然后在用户真实需要时再进行加载：

```js
// someModule.js
console.log("someModule.js loaded");
module.exports = {
  render: function (element) {
    element.innerHTML = "You clicked a button";
  },
};
```

在入口文件中使用 import 进行异步加载：

```js
console.log("index.js loaded");
window.onload = function () {
  document.querySelector("#bt").addEventListener("click", function (evt) {
    console.log("Button Clicked");
    import("./someModule").then(function (page) {
      page.render(document.querySelector(".holder"));
    });
  });
};
```

最后值得一提的是，Parcel 内建支持 WebAssembly 与 Rust，通过简单的 import 导入，即可以使用 WASM 模块：

```js
// synchronous import
import { add } from "./add.wasm";
console.log(add(2, 3));

// asynchronous import
const { add } = await import("./add.wasm");
console.log(add(2, 3));

// synchronous import
import { add } from "./add.rs";
console.log(add(2, 3));

// asynchronous import
const { add } = await import("./add.rs");
console.log(add(2, 3));
```

这里 add.rs 是使用 Rust 编写的简单加法计算函数：

```rs
#[no_mangle]
pub fn add(a: i32, b: i32) -> i32 {
  return a + b
}
```

# Rollup + Microbundle

Rollup 是较为为纯粹的模块打包工具，其相较于 Parcel 与 Webpack 等，更适合于构建 Library，譬如 React、Vue.js、Angular、D3、Moment、Redux 等一系列优秀的库都是采用 Rollup 进行构建。。Rollup 能够将按照 ESM(ES2015 Module)规范编写的源码构建输出为 IIFE、AMD、CommonJS、UMD、ESM 等多种格式，并且其较早地支持 Tree Shaking，Scope Hoisting 等优化特性，保证模块的简洁与高效。这里我们使用的 Rollup 示例配置项目存放在了 [fe-boilerplate/rollup](https://github.com/wx-chevalier/fe-boilerplates/tree/master/bundler/rollup)。最简单的 rollup.config.js 文件配置如下：

```js
export default {
  // 指定模块入口
  entry: "src/scripts/main.js",
  // 指定包体文件名
  dest: "build/js/main.min.js",
  // 指定文件格式
  format: "iife",
  // 指定 SourceMap 格式
  sourceMap: "inline",
};
```

如果我们只是对简单的 `sayHello` 函数进行打包，那么输出的文件中也只是会简单地连接与调用，并且清除未真实使用的模块：

```js
(function() {
  'use strict';
  ...
  function sayHelloTo(name) {
    ...
  }
  ...
  const result1 = sayHelloTo('Jason');
  ...
})();
//# sourceMappingURL=data:application/json;charset=utf-8;base64,...
```

Rollup 同样具有丰富的插件系统，在 [fe-boilerplate/rollup](https://github.com/wx-chevalier/fe-boilerplates/tree/master/bundler/rollup) 中我们也引入了常见的别名、ESLint、环境变量定义、包体压缩与分析等插件。这里我们以最常用的 Babel 与 TypeScript 为例，如果我们需要在项目中引入 Babel，则同样在根目录配置 `.babelrc` 文件，然后引入 rollup-plugin-babel 插件即可：

```js
import { rollup } from 'rollup';
import babel from 'rollup-plugin-babel';

rollup({
  entry: 'main.js',
  plugins: [
    babel({
      exclude: 'node_modules/**'
    })
  ]
}).then(...)
```

对于 TypeScript 则是引入 rollup-plugin-typescript 插件：

```js
import typescript from "rollup-plugin-typescript";

export default {
  entry: "./main.ts",

  plugins: [typescript()],
};
```

[Microbundle](https://github.com/developit/microbundle) 则是 Developit 基于 Rollup 封装的零配置的轻量级打包工具，其目前已经内建支持 TypeScript 与 Flow，不需要额外的配置；笔者在 [js-swissgear/x-fetch](https://github.com/wx-chevalier/js-swissgear) 项目的打包中也使用了该工具。

```json
{
  "scripts": {
    "build": "microbundle",
    "dev": "microbundle watch"
  }
}
```

- index.js 是 CommonJS 模块，是 Node.js 内置的模块类型，使用类似于 `require('MyModule')` 语法导入
- index.m.js 是 ECMAScript 模块，使用类似于 `import MyModule from 'my-module'` 语法导入
- index.umd.js 是 UMD 模块
- index.d.ts 是 TypeScript 的类型声明文件

# Webpack

作为著名的打包工具，Webpack 允许我们指定项目的入口地址，然后自动将用到的资源，经由 Loader 与 Plugin 的转换，打包到包体文件中。Webpack 相关的项目模板可以参考：[fe-boilerplate/react-webpack](https://github.com/wx-chevalier/fe-boilerplates/blob/master/react/webpack), [fe-boilerplate/react-webpack-ts](https://github.com/wx-chevalier/fe-boilerplates/blob/master/react/webpack-ts), [fe-boilerplate/vue-webpack](https://github.com/wx-chevalier/fe-boilerplates/blob/master/vue/webpack) 等。

![538c4af0d21e375d6d252d38cbb8a993](https://user-images.githubusercontent.com/5803001/39744493-0e21c33a-52d7-11e8-8295-1f8deb389565.png)

Webpack 目前也支持零配置运行

```sh
$ npm install webpack webpack-cli webpack-dev-server --save-dev
```

```json
"scripts": {
  "start": "webpack-dev-server --mode development",
  "build": "webpack --mode production"
},
```

## 基础配置

```js
const config = {
  // 定义入口
  entry: {
    app: path.join(__dirname, "app"),
  },
  // 定义包体文件
  output: {
    // 输出目录
    path: path.join(__dirname, "build"),

    // 输出文件名
    filename: "[name].js",
    // 使用 hash 作为文件名
    // filename: "[name].[chunkhash].js",
  },
  // 定义如何处理
  module: {
    rules: [
      {
        test: /\.js$/,
        use: "babel-loader",
        exclude: /node_modules/,
      },
    ],
  },
  // 添加额外插件操作
  plugins: [new webpack.DefinePlugin()],
};
```

Webpack 同样支持添加多个配置：

```js
module.exports = [{
  entry: './app.js',
  output: ...,
  ...
}, {
  entry: './app.js',
  output: ...,
  ...
}]
```

我们代码中的 require 与 import 解析规范，则由 resolve 模块负责，其包含了扩展、别名、模块等部分：

```js
const config = {
  resolve: {
    alias: {
      /*...*/
    },
    extensions: [
      /*...*/
    ],
    modules: [
      /*...*/
    ],
  },
};
```

## 资源加载

```js
const config = {
  module: {
    rules: [
      {
        // **Conditions**
        test: /\.js$/, // Match files
        enforce: "pre", // "post" too

        // **Restrictions**
        include: path.join(__dirname, "app"),
        exclude: (path) => path.match(/node_modules/),

        // **Actions**
        use: "babel-loader",
      },
    ],
  },
};
```

```js
// Process foo.png through url-loader and other matches
import "url-loader!./foo.png";

// Override possible higher level match completely
import "!!url-loader!./bar.png";
```

babel-loader 或者 awesome-typescript-loader 来处理 JavaScript 或者 TypeScript 文件

```js
/******/ (function(modules) { // webpackBootstrap
...
/* 0 */
/***/ (function(module, __webpack_exports__, __webpack_require__) {

"use strict";
__webpack_require__.r(__webpack_exports__);
/* harmony default export */ __webpack_exports__["default"] = ((text = "Hello world") => {
  const element = document.createElement("div");

  element.innerHTML = text;

  return element;
});

/***/ })
/******/ ]);
```

`use: ["style-loader", "css-loader"]` css-loader 会自动地解析 @import 与 url()，而 style-loader 则会将 CSS 注入到 DOM 中，并且实现 HMR 的特性，而对于 SASS、LESS 等 CSS 预处理器，也有专门的 sass-loader 或者 less-loader 来处理；在生产环境下，我们也常常会将 CSS 抽取到独立的样式文件中，此时就可以使用 mini-css-extract-plugin (MCEP) 等工具。同样，我们可以使用 url-loader/file-loader 来处理图片等资源文件，

## 代码分割

代码分割是[提升 Web 性能表现](https://parg.co/lwm)的重要分割，我们常做的代码分割也分为公共代码提取与按需加载等方式。公共代码提取即是将第三方渲染模块或者库与应用本身的逻辑代码分割，或者将应用中多个模块间的公共代码提取出来，划分到独立的 Chunk 中，以方便客户端进行缓存等操作。

![cc11f7e53c579fff28de1b3ed5b9f53a](https://user-images.githubusercontent.com/5803001/39862950-c8ba51c0-5477-11e8-892c-a2b6ec619e2d.png)

### SplitChunksPlugin

不同于 Webpack 3 中需要依赖 CommonChunksPlugin 进行配置，Webpack 4 引入了 [SplitChunksPlugin](https://webpack.js.org/plugins/split-chunks-plugin/#optimization-runtimechunk)，并为我们提供了开箱即用的代码优化特性，Webpack 会根据以下情况自动进行代码分割操作：

- 新的块是在多个模块间共享，或者来自于 node_modules 目录；
- 新的块在压缩之前的大小应该超过 30KB；
- 页面所需并发加载的块数量应该小于或者等于 5；
- 初始页面加载的块数量应该小于或者等于 3；

SplitChunksPlugin 的默认配置如下：

```js
splitChunks: {
    // 通用配置
    chunks: "async",
    minSize: 30000,
    minChunks: 1,
    maxAsyncRequests: 5,
    maxInitialRequests: 3,
    automaticNameDelimiter: '~',
    name: true,

    // 自定义配置，会覆写通用配置
    cacheGroups: {
        vendors: {
            test: /[\\/]node_modules[\\/]/,
            priority: -10
        },

    // 默认的切割规则
    default: {
            minChunks: 2,
            priority: -20,
            reuseExistingChunk: true
        }
    }
}
```

当两个 chunk 包含了相同代码时，会生成 `chunka~index~chunkb` 等类似的代码，值得一提的是，这里的 chunks 选项有 `initial`, `async` 与 `all` 三个配置，上述配置即是分别针对初始 chunks、按需加载的 chunks 与全部的 chunks 进行优化；如果将 vendors 的 chunks 设置为 `initial`，那么它将忽略通过动态导入的模块包包含的第三方库代码。而 priority 则用于指定某个自定义的 Cache Group 捕获代码的优先级，其默认值为 0。在 [common-chunk-and-vendor-chunk](https://parg.co/YoE) 例子中，我们即针对入口进行优化，提取出入口公共的 vendor 模块与业务模块：

```js
{
splitChunks: {
			cacheGroups: {
				commons: {
					chunks: "initial",
					minChunks: 2,
					maxInitialRequests: 5, // The default limit is too small to showcase the effect
					minSize: 0 // This is example is too small to create commons chunks
				},
				vendor: {
					test: /node_modules/,
					chunks: "initial",
					name: "vendor",
					priority: 10,
					enforce: true
				}
			}
		}
}
```

Webpack 的 optimization 还包含了 runtimeChunk 属性，当该属性值被设置为 true 时，即会为每个 Entry 添加仅包含运行时信息的 Chunk；当该属性值被设置为 single 时，即为所有的 Entry 创建公用的包含运行时的 Chunk。

### import

我们也可以在代码中使用 import 语句，动态地进行块划分，实现代码的按需加载：

![c4e91fafb1a08e7733ac2688222eb65a](https://user-images.githubusercontent.com/5803001/39863036-0aaf92d4-5478-11e8-929c-9f07e8dca3b8.png)

```js
// Webpack 3 之后支持显式指定 Chunk 名
import(/* webpackChunkName: "optional-name" */ "./module")
  .then((module) => {
    /* ... */
  })
  .catch((error) => {
    /* ... */
  });
```

```js
webpackJsonp([0], {
  KMic: function(a, b, c) {
    ...
  },
  co9Y: function(a, b, c) {
    ...
  },
});
```

如果是使用 React 进行项目开发，推荐使用 [react-loadable](https://www.npmjs.com/package/react-loadable) 进行组件的按需加载，他能够优雅地处理组件加载、服务端渲染等场景。Webpack 还内建支持基于 ES6 Module 规范的 Tree Shaking 优化，即仅从导入文件中提取出所需要的代码。

更多关于 Webpack 的使用技巧可以参阅 [Webpack CheatSheet](https://parg.co/Yuq) 或者[现代 Web 全栈开发与工程架构/Webpack](https://github.com/wx-chevalier/Web-Notes) 章节。

# Backpack

Backpack 是面向 Node.js 的极简构建系统，受 create-react-app, Next.js 以及 Nodemon 的影响，能够以零配置的方式创建 Node.js 项目。Backpack 为我们处理了文件监控、热加载、转换、打包等工作，默认支持 ECMAScript 最新的 async/await, 对象扩展、类属性等语法。我们可以使用 npm 安装依赖：

```sh
$ npm i backpack-core --save
```

然后在 package.json 中配置运行脚本：

```json
{
  "scripts": {
    "dev": "backpack",
    "build": "backpack build"
  }
}
```

在 [Backend-Boilerplate/node](https://github.com/wx-chevalier/Backend-Boilerplate) 中可以查看 Backpack 的典型应用，我们也可以覆盖默认的 Webpack 配置：

```js
// backpack.config.js
module.exports = {
  webpack: (config, options, webpack) => {
    // Perform customizations to config
    // Important: return the modified config
    return config;
  },
};
```

或者添加 Babel 插件：

```json
{
  "presets": ["backpack-core/babel", "stage-0"]
}
```

# Module Loader | 模块加载器

## SystemJS

Configurable module loader enabling backwards compatibility workflows for ES modules in browsers.

```html
<script type="systemjs-packagemap">
  {
    "packages": {
      "lodash": "https://unpkg.com/lodash@4.17.10/lodash.js"
    }
  }
</script>
<!-- Alternatively:
<script type="systemjs-packagemap" src="path/to/map.json">
-->
<!-- SystemJS must be loaded after the package map -->
<script src="system.js"></script>
<script>
  System.import("/js/main.js");
</script>
```

To load ES modules directly in older browsers with SystemJS we can install and use the Babel plugin:

```html
<script src="system.js"></script>
<script src="extras/transform.js"></script>
<script src="plugin-babel/dist/babel-transform.js"></script>
<script>
  // main and all its dependencies will now run through transform before loading
  System.import("/js/main.js");
</script>
```

```js
import moment from "moment";

export function test() {
  const m1 = moment().format("LLL");
  const m2 = moment().fromNow();
  return `The moment is ${m1}, which was ${m2}`;
}
```

```js
const SystemJS = require("systemjs");

SystemJS.config({
  map: {
    traceur: "node_modules/traceur/bin/traceur.js",
    moment: "node_modules/moment/src",
  },
  packages: {
    moment: {
      main: "moment.js",
    },
  },
});

SystemJS.import("./test.js")
  .then(function (test) {
    var t = test.test();
    console.log(t);
  })
  .catch(function (e) {
    console.error(e);
  });
```

## RequireJS
