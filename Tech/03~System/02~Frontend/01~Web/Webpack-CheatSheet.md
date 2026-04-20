# Webpack CheatSheet | Webpack 基础与实践清单

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

# 基础配置

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

# 开发环境

题注：本文是 [Webpack CheatSheet | Webpack 基础与实践清单](https://github.com/wx-chevalier/Awesome-CheatSheets/blob/master/Web/DevOps/Bundler/Webpack-CheatSheet.md)的一部分，项目代码可以参考 [fe-boilerplate | 多技术栈前端项目模板](https://github.com/wx-chevalier/fe-boilerplates)。

## 路径解析

随着需求的迭代与功能的完善，我们的项目也会愈发庞大而复杂，目录层级结构也会不断深化；以 [React 实践清单](https://parg.co/YWj)中讨论的 React 项目组织方式为例，我们常会分为 components, containers, services, apis, ducks, store, i18n 等等目录，如果全部以相对路径方式引入，可能会变成这个样子：

```js
import React from "react";
import { connect } from "react-redux";

import { someConstant } from "./../../config/constants";
import MyComponent from "./../../../components/MyComponent";
import { myActionCreator } from "./../../../ducks/someReducer";
```

毫无疑问，这样繁多的引用不可避免地会导致代码之间耦合度的增加，使得更难以重构或者优化。在适当地模块划分的基础上，我们希望在跨模块引用时，能够以绝对路径的方式，譬如：

```js
import React from "react";
import { connect } from "react-redux";
import { someConstant } from "Config/constants";
import MyComponent from "Components/MyComponent";
import { myActionCreator } from "Ducks/someReducer";
```

当然，我们并不提倡过度地使用绝对路径引入，对于相对关系固定的组件，还是应该优先使用相对路径方式引入。

### Webpack

如前文介绍，Webpack 允许我们使用 `resolve.alias` 来自定义路径解析：

```js
module.resolve = {
  alias: {
    Config: path.resolve(__dirname, "..", "src", "config"),
    Components: path.resolve(__dirname, "..", "src", "components"),
    Ducks: path.resolve(__dirname, "..", "src", "ducks"),
    Shared: path.resolve(__dirname, "..", "src", "shared"),
    App: path.join(__dirname, "..", "src"),
  },
};
```

### VSCode

开发工具的支持是不可避免地因素，值得高兴的是 VSCode 允许我们在 `jsconfig.json` 中配置解析规则，[Auto-Import](https://github.com/soates/Auto-Import) 这样的自动导入工具同样能识别这些规则：

```js
{
  "compilerOptions": {
    "target": "es2017",
    "allowSyntheticDefaultImports": false,
    "baseUrl": "./",
    "paths": {
      "Config/*": ["src/config/*"],
      "Components/*": ["src/components/*"],
      "Ducks/*": ["src/ducks/*"],
      "Shared/*": ["src/shared/*"],
      "App/*": ["src/*"]
    }
  },
  "exclude": ["node_modules", "dist"]
}
```

### ESLint

ESLint 同样是前端开发不可或缺的部分，我们可以使用 [eslint-import-resolver-webpack](https://www.npmjs.com/package/eslint-import-resolver-webpack) 来扩展 eslint-import 的模块解析，使用 npm 安装该模块之后进行如下配置：

```yaml
---
settings:
  import/resolver: webpack # take all defaults
```

或者指定文件名：

```yaml
---
settings:
  import/resolver:
    webpack:
      config: "webpack.dev.config.js"
      config-index: 1 # optional, take the config at index 1
```

对于未使用 Webpack 的项目，则可以考虑使用 [eslint-import-resolver-alias](https://www.npmjs.com/package/eslint-import-resolver-alias):

```js
// .eslintrc.js
module.exports = {
  settings: {
    "import/resolver": {
      alias: {
        map: [
          ["babel-polyfill", "babel-polyfill/dist/polyfill.min.js"],
          ["helper", "./utils/helper"],
          ["material-ui/DatePicker", "../custom/DatePicker"],
          ["material-ui", "material-ui-ie10"],
        ],
        extensions: [".ts", ".js", ".jsx", ".json"],
      },
    },
  },
};
```

### Jest

我们可以在 package.json 中的 jest 配置项中添加 moduleNameMapper 属性：

```json
"jest": {
  "moduleNameMapper": {
    "^Config(.*)$": "<rootDir>/src/config$1",
    "^Components(.*)$": "<rootDir>/src/components$1",
    "^Ducks(.*)$": "<rootDir>/src/ducks$1",
    "^Shared(.*)$": "<rootDir>/src/shared$1",
    "^App(.*)$": "<rootDir>/src$1"
}
```

### TypeScript

TypeScript 的配置类似于 VSCode，在 tsconfig.json 的 compilerOptions 选项中添加如下配置：

```json
{
  "baseUrl": ".",
  "paths": {
    "c-apis/*": ["src/apis/*"],
    "c-models/*": ["src/models/*"],
    "c-stores/*": ["src/stores/*"],
    "c-utils/*": ["src/shared/*"]
  }
}
```

## 构建性能优化

# 生产环境

## 压缩与版本控制

## 代码分割

代码分割是[提升 Web 性能表现](https://parg.co/lwm)的重要分割，我们常做的代码分割也分为公共代码提取与按需加载等方式。公共代码提取即是将第三方渲染模块或者库与应用本身的逻辑代码分割，或者将应用中多个模块间的公共代码提取出来，划分到独立的 Chunk 中，以方便客户端进行缓存等操作。

![cc11f7e53c579fff28de1b3ed5b9f53a](https://user-images.githubusercontent.com/5803001/39862950-c8ba51c0-5477-11e8-892c-a2b6ec619e2d.png)

不同于 Webpack 3 中需要依赖 CommonChunksPlugin 进行配置，Webpack 4 引入了 [SplitChunksPlugin](https://webpack.js.org/plugins/split-chunks-plugin/#optimization-runtimechunk)，并为我们提供了开箱即用的代码优化特性，Webpack 会根据以下情况自动进行代码分割操作：

- 新的块是在多个模块间共享，或者来自于 node_modules 目录；
- 新的块在压缩之前的大小应该超过 30KB；
- 页面所需并发加载的块数量应该小于或者等于 5；
- 初始页面加载的块数量应该小于或者等于 3；

SplitChunksPlugin 的默认配置如下：

```js
splitChunks: {
    chunks: "async",
    minSize: 30000,
    minChunks: 1,
    maxAsyncRequests: 5,
    maxInitialRequests: 3,
    automaticNameDelimiter: '~',
    name: true,
    cacheGroups: {
        vendors: {
            test: /[\\/]node_modules[\\/]/,
            priority: -10
        },
    default: {
            minChunks: 2,
            priority: -20,
            reuseExistingChunk: true
        }
    }
}
```

值得一提的是，这里的 chunks 选项有 `initial`, `async` 与 `all` 三个配置，上述配置即是分别针对初始 chunks、按需加载的 chunks 与全部的 chunks 进行优化；如果将 vendors 的 chunks 设置为 `initial`，那么它将忽略通过动态导入的模块包包含的第三方库代码。而 priority 则用于指定某个自定义的 Cache Group 捕获代码的优先级，其默认值为 0。在 [common-chunk-and-vendor-chunk](https://parg.co/YoE) 例子中，我们即针对入口进行优化，提取出入口公共的 vendor 模块与业务模块：

```js
{
	splitChunks: {
		// 禁止默认 splitChunks 行为，防止生成 a~b.js 这样的公用包
		default: false,
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

Webpack 的 optimization 还包含了 runtimeChunk 属性，当该属性值被设置为 true 时，即会为每个 Entry 添加仅包含运行时信息的 Chunk；当该属性值被设置为 single 时，即为所有的 Entry 创建公用的包含运行时的 Chunk。我们也可以在代码中使用 import 语句，动态地进行块划分，实现代码的按需加载：

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
