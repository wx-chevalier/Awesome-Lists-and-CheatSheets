[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![license: CC BY-NC-SA 4.0](https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-lightgrey.svg)][license-url]

<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/wx-chevalier/Awesome-Lists">
    <img src="https://ngte-website.oss-cn-hangzhou.aliyuncs.com/header-svgs/Awesome-Lists.svg" alt="Logo" style="width: 100vw;height: 400px" />
    <img src="https://assets.ng-tech.icu/item/20230221235618.png" alt="Logo" style="height: 400px" />
  </a>

  <p align="center">
    <a href="https://ng-tech.icu/books/Awesome-Lists"><strong>在线阅读 >> </strong></a>
    <br />
    <br />
    <a href="https://github.com/wx-chevalier/Awesome-Lists">速览手册</a>
    ·
    <a href="https://github.com/wx-chevalier">代码实践</a>
    ·
       <a href="https://github.com/wx-chevalier/Awesome-Lists">参考资料</a>

  </p>
</p>

<!-- ABOUT THE PROJECT -->

# Preface | 前言

Awesome-Lists 是横跨了编程语言与理论、Web 与大前端、服务端开发与基础架构、云计算与大数据、数据科学与人工智能、产品设计等多个领域的，包括了文章、书籍、课程、案例、开源项目等多种类型的**精选**资料索引（在各个系列的文章末尾会附上一些细分领域关联性较强的参考资料列表）。Awesome-Lists 记录了笔者在日常阅读、学习与实践中发掘的优秀的资料，其按照[知识图谱](https://github.com/wx-chevalier/Developer-Zero-To-Mastery)中定义的各个领域的知识体系分门别类地存放；笔者会不断更新其中链接，去芜存菁，去重留一，希望为同仁提供优秀的、有价值的、尽可能精简的资料索引。

梭罗在《瓦尔登湖》中写道：知道自己知道什么，也知道自己不知道什么，这就是真正的知识。知我所知是对于自己能力的正确认识，知我所不知则能为自己未来的路明确些方向。站在巨人的肩膀上窥探大道三千，才能触类旁通，他山之石，可以攻玉。相较于其他很多的 `Awesome-*` 项目，笔者认为 AwesomeList 更为纯粹，其中收录的文章链接都是笔者阅读、筛选之后，按照 [IT 技术图谱与知识架构](https://github.com/wx-chevalier/Developer-Zero-To-Mastery)归档留存。在碎片化学习的同时，也能够建立系统化的知识。

![awesome coder](https://user-images.githubusercontent.com/5803001/43364904-59f5bda6-9356-11e8-9ab3-ae073d08bb9e.png)

# Nav | 导航

## Convention | 约定

本系列文章目录层次如下：

- {Something}-List.md - 该文件包含或者分割为以下内容：

  - Overview

    - Ecosystem
    - Learning Path & Roadmap & Guideline
    - CheatSheet

  - Resource
    - Book
    - Collection
    - Course
    - Series
    - Site
    - Tutorial

- {Something}-OpenSource-List.md

  - Showcase
  - Dev Tools
  - Framework
  - ...

- @Deprecated {Something}-Syntax-List.md - 该文件包含或者分割为以下内容：

  - Variable & Expression
  - Control flow & Error Handler
  - Function & Functional Programming
  - Class & Object
  - MetaProgramming

- @Deprecated {Something}-DataStructure-List.md - 该文件包含或者分割为以下内容：

  - Basic Type
  - Indexed Collection
  - Keyed Collection

- @Deprecated {Something}-Functionality-List.md - 该文件包含或者分割为以下内容：

  - Storage
  - Network
  - System / Process

- @Deprecated {Something}-DevOps-List.md - 该文件包含或者分割为以下内容：

  - Builder, Task runner, Bundler, dependence management
  - Debug
  - Test, unit test, integration test, e2e test
  - Architecture, module system, State management,
  - StyleGuide, coding standards for source code in the JavaScript programming language.

- @Deprecated {Something}-Production-List.md - 该文件包含或者分割为以下内容：

  - Performance Optimization / Tunning
  - Release / Deploy
  - Accessibility / Monitor
  - RealTime
  - I18n

- @Deprecated {Something}-Internals-List.md Inner mechanism under the hood, Core/Compiler/Engine

本系列文章索引类别约定如下：

- #Article#：单篇文章，也是默认的引用类型
- #Slide#：幻灯片
- #Series#：系列文章
- #Book# 📚：书籍
- #Course# 🎥：视频教程
- #Collection# 🗃️：资源集锦
- #Code# ![code](https://ng-tech.icu/assets/code.svg): 开源的项目或者框架、库。
- #Scratch#: 从零构建某些系统
- #Tool#: 工具
- #Paper#
- #Tutorial#

目前，在知识体系中会存在多层构建的问题，对于非 #Article#、#Series# 类遵循的归纳原则就是：仅放置在最顶层与最底层，不放在中间层。

# About

## Stats | 统计

```sh
# 统计所有的有效链接数
$ wc -l **/*.md | grep -E -v "(Weekly|total|README)" | awk '{s+=$1} END {printf "%.0f", s}'
```

## Acknowledgements

- [The book of secret knowledge](https://github.com/trimstray/the-book-of-secret-knowledge): A collection of inspiring lists, manuals, cheatsheets, blogs, hacks, one-liners, cli/web tools and more.

## 版权

笔者所有文章遵循 [知识共享 署名 - 非商业性使用 - 禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh)，欢迎转载，尊重版权。您还可以前往 [NGTE Books](https://ng-tech.icu/books-gallery/) 主页浏览包含知识体系、编程语言、软件工程、模式与架构、Web 与大前端、服务端开发实践与工程架构、分布式基础架构、人工智能与深度学习、产品运营与创业等多类目的书籍列表：

[![NGTE Books](https://s2.ax1x.com/2020/01/18/19uXtI.png)](https://ng-tech.icu/books-gallery/)

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[contributors-shield]: https://img.shields.io/github/contributors/wx-chevalier/Awesome-Lists.svg?style=flat-square
[contributors-url]: https://github.com/wx-chevalier/Awesome-Lists/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/wx-chevalier/Awesome-Lists.svg?style=flat-square
[forks-url]: https://github.com/wx-chevalier/Awesome-Lists/network/members
[stars-shield]: https://img.shields.io/github/stars/wx-chevalier/Awesome-Lists.svg?style=flat-square
[stars-url]: https://github.com/wx-chevalier/Awesome-Lists/stargazers
[issues-shield]: https://img.shields.io/github/issues/wx-chevalier/Awesome-Lists.svg?style=flat-square
[issues-url]: https://github.com/wx-chevalier/Awesome-Lists/issues
[license-shield]: https://img.shields.io/github/license/wx-chevalier/Awesome-Lists.svg?style=flat-square
[license-url]: https://github.com/wx-chevalier/Awesome-Lists/blob/master/LICENSE.txt
