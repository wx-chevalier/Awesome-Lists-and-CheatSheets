[![Awesome](https://parg.co/UvS)](https://github.com/wx-chevalier/Awesome-Lists)

<p align="center">
  <a href="https://github.com/wx-chevalier/Developer-Zero-To-Mastery">
    <img src="header.svg" alt="Logo" style="width: 100vw;height: 400px" />
  </a>

  <p align="center">
    <a href="./README.md">中文版本</a>
    <span style="margin:0 8px;">|</span>
    <a href="./README-en.md">English Version</a>
  </p>
</p>

Awesome-Lists 是横跨了编程语言与理论、Web 与大前端、服务端开发与基础架构、云计算与大数据、数据科学与人工智能、产品设计等多个领域的，包括了文章、书籍、课程、案例、开源项目等多种类型的资料索引。Awesome-Lists 记录了笔者在日常阅读、学习与实践中发掘的优秀的资料，其按照[知识图谱](https://github.com/wx-chevalier/Developer-Zero-To-Mastery)中定义的各个领域的知识体系分门别类地存放；笔者会不断更新其中链接，去芜存菁，去重留一，希望为同仁提供优秀的、有价值的、尽可能精简的资料索引。

![awesome coder](https://user-images.githubusercontent.com/5803001/43364904-59f5bda6-9356-11e8-9ab3-ae073d08bb9e.png)

# Preface | 前言

梭罗在《瓦尔登湖》中写道：知道自己知道什么，也知道自己不知道什么，这就是真正的知识。知我所知是对于自己能力的正确认识，知我所不知则能为自己未来的路明确些方向。站在巨人的肩膀上窥探大道三千，才能触类旁通，他山之石，可以攻玉。相较于其他很多的 Awesome-\* 项目，笔者认为 AwesomeList 更为纯粹，其中收录的文章链接都是笔者阅读、筛选之后，按照 [IT 技术图谱与知识架构](https://parg.co/UHY)归档留存。在碎片化学习的同时，也能够建立系统化的知识。

当然，AwesomeList 包含了笔者正在使用的，或者关注到的技术，自然无法做到没有遗漏，也是仅代表笔者的个人看法。

## Index | 索引

为了便于知识归纳，AwesomeList 在 [Specials](./Specials) 目录中准备了多个专题的集锦，它们包括：

- [Awesome CS Collections](./Specials/Awesome-CS-Collections.md)

- [Build Your Own X From Scratch](./Specials/Build-Your-Own-X-From-Scratch.md)

# About | 关于

## Stats | 统计

```sh
# 统计所有的有效链接数
$ wc -l **/*.md | grep -E -v "(Weekly|total|README)" | awk '{s+=$1} END {printf "%.0f", s}'
```

## Convention | 约定

本系列文章目录层次如下：

- {Something}-List.md - 该文件包含或者分割为以下内容：

  - Overview & Case Study & CheatSheet
  - Resource & Book & Collection
  - Tutorial & Learning Path

- {Something}-Syntax-List.md - 该文件包含或者分割为以下内容：

  - Variable & Expression
  - Control flow & Error Handler
  - Function & Functional Programming
  - Class & Object
  - MetaProgramming

- {Something}-DataStructure-List.md - 该文件包含或者分割为以下内容：

  - Basic Type
  - Indexed Collection
  - Keyed Collection

- {Something}-Functionality-List.md - 该文件包含或者分割为以下内容：

  - Storage
  - Network
  - System / Process

- {Something}-DevOps-List.md - 该文件包含或者分割为以下内容：

  - Builder, Task runner, Bundler, dependence management
  - Debug
  - Test, unit test, integration test, e2e test
  - Architecture, module system, State management,
  - StyleGuide, coding standards for source code in the JavaScript programming language.

- {Something}-Production-List.md - 该文件包含或者分割为以下内容：

  - Performance Optimization / Tunning
  - Release / Deploy
  - Accessibility / Monitor
  - RealTime
  - I18n

- {Something}-OpenSource-List.md - Awesome tools, frameworks, projects

- {Something}-Internals-List.md Inner mechanism under the hood, Core/Compiler/Engine

本系列文章索引类别约定如下：

- #Article#：单篇文章，也是默认的引用类型
- #Slide#：幻灯片
- #Series#：系列文章
- #Book#：书籍
- #Course#：视频教程
- #Collection#：资源集锦
- #Project#: 开源的项目或者框架、库。

## 版权

笔者所有文章遵循 [知识共享 署名 - 非商业性使用 - 禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh)，欢迎转载，尊重版权。您还可以前往 [NGTE Books](https://ng-tech.icu/books/) 主页浏览包含知识体系、编程语言、软件工程、模式与架构、Web 与大前端、服务端开发实践与工程架构、分布式基础架构、人工智能与深度学习、产品运营与创业等多类目的书籍列表：

[![NGTE Books](https://s2.ax1x.com/2020/01/18/19uXtI.png)](https://ng-tech.icu/books/)
