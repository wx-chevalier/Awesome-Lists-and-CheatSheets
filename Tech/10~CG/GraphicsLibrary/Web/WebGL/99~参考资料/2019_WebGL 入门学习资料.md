# WebGL 入门学习资料

作为一名图形爱好者，在学习 WebGL 的起步阶段经历了非常痛苦的过程。2016 年初至今，三年的学习过程中，阅览过各种类型的教程。这里收集了我所学习过的、对初学者比较友好的教程，主要包括了 WebGL、GLSL 和 ThreeJS 相关主题。

在罗列这些教程前，先介绍一下我个人的情况，这样你也能够更好的和自身情况进行对比。我学习的专业是工业设计与软件工程，所以对三维的各种概念和三维美术创作的整个工作流程比较了解、而且能熟练使用多种行业的三维软件。毕业后从事交互设计工作，在工作中学习了 Html、CSS 和 JavaScript。

如果你对三维一无所知，我建议你可以看一下这两本书：[3D 动画与特效制作艺术](https://book.douban.com/subject/4924302/)、[数字绘图的光照与渲染技术](https://book.douban.com/subject/3225198/)，这两本是我看过**最最最优秀**的三维书籍（美术技术方面），不局限于某一三维软件，讲解浅显易懂、面面俱到，看完后你会对三维美术工作流程有一个直观的认识，并且里面也提及了非常多专业术语，对我的帮助特别大。

学习 WebGL 前，你还需要具备一定的前端知识，至少需要知道 HTML 的标签是干什么用的，JavaScript 的变量和基本语法。除了前端知识，一些基本的线性代数概念也需要了解，比如矢量、矩阵。你也可以考虑先学习使用 ThreeJS 这样的 WebGL 框架，然后再过度到 WebGL，这也是一个很好的选择。ThreeJS 的学习门槛非常低，重要的是 ThreeJS 对象名称、属性、方法的可读性很高，正常人能够直观的理解，学习过程中不会有太大挫败感。

带有 的教程是我个人最喜欢的教程，希望这些入门教程也同样对你有帮助。Enjoy~

## WebGL 在线学习资料

- [Mozilla - Getting_started_with_WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Tutorial/Getting_started_with_WebGL)（中/英）

- Learning WebGL （中/英）

  - [English](http://learningwebgl.com/)（dead link as of Nov 2018, backup link [here](https://web.archive.org/web/20180624223943/http://learningwebgl.com/blog/?page_id=1217)，[GitHub DEMO](https://github.com/tparisi/webgl-lessons)）
  - [Chinese](http://www.hiwebgl.com/?p=42)

- [WebGL Fundamentals](https://webglfundamentals.org/)（中/英）

- [WebGL Academy - interactive tutorials](http://www.webglacademy.com/)（英）

- [Learn WebGL](http://learnwebgl.brown37.net/)（英）

#### WebGL 2.0

- [WebGL2 Fundamentals](https://webgl2fundamentals.org/)（中/英）

#### Manual

- Khronos WebGL repository（英）
  - [Official](https://www.khronos.org/webgl/)
  - [GitHub](https://github.com/KhronosGroup/WebGL)
- [Mozilla - WebGL: 2D and 3D graphics for the web ](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API)（中/英）

## GLSL/ESSL 在线学习资料

- [The Book of Shaders](https://thebookofshaders.com/)（中/英） ，讲解浅显易懂，并且提供了很多现成的函数算法和优秀的 GLSL 相关资源。还在连载中，但已经很久没有更新了，这个项目的[GitHub](https://github.com/patriciogonzalezvivo/thebookofshaders)地址。正在学习中~
- [GLSL: An Introduction](http://nehe.gamedev.net/article/glsl_an_introduction/25007/)（英）

#### Shader create tool

- [GLSL community - Shadertoy](https://www.shadertoy.com/)
- [GLSL community - Vertex Shader Art](https://www.vertexshaderart.com/)
- [GLSL community - GLSL sandbox](http://glslsandbox.com/)
- [Shader editor](http://shdr.bkcore.com/)

## ThreeJS 在线学习资料

- [Threejs intro PPT](http://davidscottlyons.com/threejs-intro/)（英）
- [ThreeJS documentation](https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene)（中/英），Manual 章节中的 Getting Started 部分是很好的入门资料
- [Three.js 入门指南](http://www.ituring.com.cn/book/1272)（中） ，浅显易懂的一本小教材，是我学习 WebGL 过程中看的第一本教材，对我帮助非常大。

## 数学在线学习资料

- [Mozilla - Matrix math for the web](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Matrix_math_for_the_web)（中/英）
- [Immersive math](http://immersivemath.com/ila/index.html)（英）

## 中文图书

- [WebGL Programming Guide / WebGL 编程指南](https://book.douban.com/subject/25909351/)（[Download DEMO](https://sites.google.com/site/webglbook/home/downloads)）
- [OpenGL Shading Language / OpenGL 着色语言](https://book.douban.com/subject/1911849/)，这本书是用的 OpenGL 语言，但是因为比较老，所以书中 GLSL 语言貌似现在 WebGL 的 GLSL 都能支持，内置函数命名有些不同，但是能够看明白。正在学习中~
- [Learning Three.js / Three.js 开发指南](https://book.douban.com/subject/27127506/)（[Online DEMO](http://www.smartjava.org/content/all-109-examples-my-book-threejs-threejs-version-r63/)、[GitHub DEMO](https://github.com/josdirksen/learning-threejs)） ，市面上为数不多的 ThreeJS 中文教材，不需要图形学基础就能看懂。
- [Interactive Computer Graphics / 交互式计算机图形学](https://book.douban.com/subject/26916420/)（[Resources](https://www.cs.unm.edu/~angel/BOOK/INTERACTIVE_COMPUTER_GRAPHICS/SEVENTH_EDITION/)） ，这是一本正儿八经、非常全面的高校计算机图形学教科书。难得的是这本教材居然用 JavaScript 和 WebGL 作为讲解计算机图形学的语言，缺点是这本书有点厚、难度也较高，课后习题我基本都不会做。相见恨晚，努力学习中~~~
- [Introduction to Computer Graphics / 计算机图形学导论——实用学习指南（WebGL 版）](https://book.douban.com/subject/30856114/)，这本书没有看过，发现这本教材的时候，我已经不需要学习导论了。但是这种导论、概论类的教材对初学者入门非常有帮助。
- [程序员的数学 3 - 线性代数](https://book.douban.com/subject/26740548/)，遇到线性代数的计算问题可以翻看查阅，正在努力学习中~

## 版本兼容&浏览器兼容

- [OpenGL (ES) APIs Table](http://web.eecs.umich.edu/~sugih/courses/eecs487/common/notes/APITables.xml)（中/英）
- [Caniuse.com](https://caniuse.com/#feat=webgl)
