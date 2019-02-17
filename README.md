![awesome coder](https://user-images.githubusercontent.com/5803001/43364904-59f5bda6-9356-11e8-9ab3-ae073d08bb9e.png)

[中文版本](./README.md) | [English Version](./README-en.md)

# Awesome List | 精而全的技术开发学习与实践资料索引

`Copyright © 王下邀月熊 - WxChevalier` [![Awesome](https://parg.co/UvS)](https://github.com/wxyyxc1992/Awesome-Lists)

AwesomeList 是记录了笔者在日常阅读、学习与实践中发掘的优秀的资料，其按照[知识图谱](https://wxyyxc1992.github.io/home/#/perspective)中定义的各个领域的知识体系分门别类地存放；笔者会不断更新其中链接，去芜存菁，去重留一，希望为同仁提供优秀的、有价值的、尽可能精简的资料索引。

![default](https://i.postimg.cc/y1QXgJ6f/image.png)

# Nav | 导航

Finally, Let these lists speak for themselves:

- If you wan't to learn Web Development, you may like [DOM List](./Web/Syntax/DOM/DOM-List.md), [CSS List](./Web/Syntax/CSS/CSS-List.md), [React List](./Web/Framework/React/React-List.md), [Redux List](./Web/Framework/Redux/Redux-List.md), [Vue List](./Web/Framework/Vue/Vue-List.md), [PWA List](./Web/Tuning/PWA/Web-PWA-List.md), [Web Performance List](./Web/Tuning/Performance/Web-Performance-List.md), [WebAssembly List](), etc.

- If you wan't to learn Java, Go, MicroService... you may like [Java List](./Web/Syntax/DOM/DOM-List.md), [JVM List](./ProgrammingLanguage/Java/JVM/JVM-List.md), [Go List](./ProgrammingLanguage/Go/Go-List.md), [MicroService List](./Backend/MicroService/MicroService-List.md), [Spring List](./Backend/WebFramework/Java/Spring/Spring-List.md), [DevOps List](./Backend/DevOps/DevOps-List.md), etc.

- 如果想了解分布式系统、虚拟化调度、数据库、分布式存储、分布式计算、操作系统等领域的知识，可以参阅 [Docker List](./Infrastructure/Virtualization/Container/Docker/Docker-List.md), [Kubernetes List](./Infrastructure/Virtualization/Orchestration/Kubernetes/Kubernetes-List.md), [Linux List](./Infrastructure/OS/Linux/Linux-List.md), [HTTP List](./Infrastructure/Network/HTTP/HTTP-List.md), [Distributed System List](./Infrastructure/DistributedSystem/DistributedSystem-List.md), [Blockchain List](./Infrastructure/DistributedSystem/Blockchain/Blockchain-List.md), [Flink List](./Infrastructure/DistributedComputing/Streaming/Flink/Flink-List.md), [Kafka List](./Infrastructure/DistributedComputing/MOM/Kafka-List.md), [Database List](./Infrastructure/Database/Database-List.md), [MySQL List](./Infrastructure/Database/RDB/MySQL/MySQL-List.md), [PostgreSQL List](./Infrastructure/Database/RDB/PostgreSQL/PostgreSQL-List.md), etc.

- If you wan't to learn AI, DeepLearning, TensorFlow... you may like [DataScienceAI Book List](./DataScienceAI/DataScienceAI-Book-List.md), [DataScienceAI Course List](./DataScienceAI/DataScienceAI-Course-List.md), [Machine Learning List](./DataScienceAI/MachineLearning/MachineLearning-List.md), [Deep Learning List](./DataScienceAI/DeepLearning/DeepLearning-List.md), [NLP List](./DataScienceAI/NLP/NLP-List.md), [TensorFlow List](./DataScienceAI/Toolkit/TensorFlow/TensorFlow-List.md), [PyTorch List](./DataScienceAI/Toolkit/PyTorch/PyTorch-List.md), etc.

建议前往 [xCompass](https://wxyyxc1992.github.io/home/#/search) 交互式地检索、查找需要的文章/链接/书籍/课程，或者直接浏览本仓库的目录以了解更多内容，也可以使用 [alfred-sg](https://github.com/wxyyxc1992/Soogle/tree/master/alfred-sg) 在 MAC 设备上进行快速检索。

# Preface | 前言

梭罗在《瓦尔登湖》中写道：知道自己知道什么，也知道自己不知道什么，这就是真正的知识。知我所知是对于自己能力的正确认识，知我所不知则能为自己未来的路明确些方向。站在巨人的肩膀上窥探大道三千，才能触类旁通，他山之石，可以攻玉。相较于其他很多的 Awesome-\* 项目，笔者认为 AwesomeList 更为纯粹，其中收录的文章链接都是笔者阅读、筛选之后，按照 [IT 技术图谱与知识架构](https://parg.co/UHY)归档留存。在碎片化学习的同时，也能够建立系统化的知识。

当然，AwesomeList 包含了笔者正在使用的，或者关注到的技术，自然无法做到没有遗漏，也是仅代表笔者的个人看法。

## Index | 索引

为了便于知识归纳，AwesomeList 在 [Specials](./Specials) 目录中准备了多个专题的集锦，它们包括：

- [Awesome CS Collections](./Specials/Awesome-CS-Collections.md)

- [Build Your Own X From Scratch](./Specials/Build-Your-Own-X-From-Scratch.md)

## Credits | 参考

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

- #Article# ：单篇文章，也是默认的引用类型
- #Slide#：幻灯片
- #Series#：系列文章
- #Book#：书籍
- #Course#：视频教程
- #Resource#：资源集锦
- #Project#: 开源的项目或者框架、库。

## 版权

![](https://parg.co/bDY) ![](https://parg.co/bDm)

笔者所有文章遵循 [知识共享 署名 - 非商业性使用 - 禁止演绎 4.0 国际许可协议](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh)，欢迎转载，尊重版权。如果觉得本系列对你有所帮助，欢迎给我家布丁买点狗粮(支付宝扫码)~

![](https://github.com/wxyyxc1992/OSS/blob/master/2017/8/1/Buding.jpg?raw=true)
