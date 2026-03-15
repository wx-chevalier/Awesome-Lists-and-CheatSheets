# Spring CheatSheet | Spring 概念、使用与实践

Spring 的设计目标是为我们提供一个一站式的轻量级应用开发平台，抽象了应用开发中遇到的共性问题。作为平台，它考虑到了企业应用资源的使用，比如数据的持久化、数据集成、事务处理、消息中间件、分布式式计算等高效可靠处理企业数据方法的技术抽象。开发过程中的共性问题，Spring 封装成了各种组件，而且 Spring 通过社区，形成了一个开放的生态系统，比如 Spring Security 就是来源于一个社区贡献。

使用 Spring 进行开发，对开发人员比较轻量，可以使用 POJO 和 JavaBean 的开发方式，使应用面向接口开发，充分支持了面向对象的设计方法。通过 IOC 容器减少了直接耦合，通过 AOP 以动态和非侵入的方式增加了服务的功能，为灵活选取不同的服务实现提供了基础，这也是 Spring 的核心。轻量级是相对于传统 J2EE 而言的，传统的 J2EE 开发，需要依赖按照 J2EE 规范实现的 J2EE 应用服务器，设计和实现时，需要遵循一系列的接口标准，这种开发方式耦合性高，使应用在可测试性和部署上都有影响，对技术的理解和要求相对较高。

# 架构与生态圈

![image](https://user-images.githubusercontent.com/5803001/42418773-d9693618-82d9-11e8-9981-328db1065def.png)

## Java Web 关键技术

Java Servlet（Java 服务器小程序）是一个基于 Java 技术的 Web 组件，运行在服务器端，它由 Servlet 容器所管理，用于生成动态的内容。Servlet 是平台独立的 Java 类，编写一个 Servlet，实际上就是按照 Servlet 规范编写一个 Java 类。Servlet 被编译为平台独立 的字节码，可以被动态地加载到支持 Java 技术的 Web 服务器中运行。

Servlet 容器也叫做 Servlet 引擎，是 Web 服务器或应用程序服务器的一部分，用于在发送的请求和响应之上提供网络服务，解码基于 MIME 的请求，格式化基于 MIME 的响应。Servlet 没有 main 方法，不能独立运行，它必须被部署到 Servlet 容器中，由容器来实例化和调用 Servlet 的方法（如 doGet()和 doPost()），Servlet 容器在 Servlet 的生命周期内包容和管理 Servlet。在 JSP 技术 推出后，管理和运行 Servlet/JSP 的容器也称为 Web 容器。

有了 Servlet 之后，用户通过单击某个链接或者直接在浏览器的地址栏中输入 URL 来访问 Servlet，Web 服务器接收到该请求后，并不是将 请求直接交给 Servlet，而是交给 Servlet 容器。Servlet 容器实例化 Servlet，调用 Servlet 的一个特定方法对请求进行处理，并产生一个响应。这个响应由 Servlet 容器返回给 Web 服务器，Web 服务器包装这个响应，以 HTTP 响应的形式发送给 Web 浏览器。

### Servlet 容器

- 通信支持：利用容器提供的方法，你能轻松的让 servlet 与 web 服务器对话，而不用自己建立 serversocket、监听某个端口、创建流等 等。容器知道自己与 web 服务器之间的协议，所以你的 servlet 不用担心 web 服务器（如 Apache）和你自己的 web 代码之间的 API，只需要考 虑如何在 servlet 中实现业务逻辑（如处理一个订单）。

- 生命周期管理：servlet 容器控制着 servlet 的生与死，它负责加载类、实例化和初始化 servlet，调用 servlet 方法，以及使 servlet 实例被垃圾回收，有了 servlet 容器，你不需要太多的考虑资源管理。

- 多线程支持：容器会自动为它所接收的每个 servlet 请求创建一个新的 java 线程。针对用户的请求，如果 servlet 已经运行完相应的 http 服务方法，这个线程就会结束。这并不是说你不需要考虑线程安全性，其实你还会遇到同步问题，不过这样能使你少做很多工作。

- 声明方式实现安全：利用 servlet 容器，你可以使用 xml 部署描述文件来配置和修改安全性，而不必将其硬编码写到 servlet 类代码中。

- JSP 支持：servlet 容器负责将 jsp 代码翻译为真正的 java 代码。

根据 Servlet 容器工作模式的不同，可以将 Servlet 容器分为以下三类：

1）独立的 Servlet 容器

当我们使用基于 Java 技术的 Web 服务器时，Servlet 容器作为构成 Web 服务器的一部分而存在。然而大多数的 Web 服务器并非基于 Java，因此，就有了下面两种 Servlet 容器的工作模式。

2）进程内的 Servlet 容器

Servlet 容器由 Web 服务器插件和 Java 容器两部分的实现组成。Web 服务器插件在某个 Web 服务器内部地址空间中打开一个 JVM（Java 虚拟机），使得 Java 容器可以在此 JVM 中加载并运行 Servlet。如有客户端调用 Servlet 的请求到来，插件取得对此请求的控 制并将它传递（使用 JNI 技术）给 Java 容器，然后由 Java 容器将此请求交由 Servlet 进行处理。进程内的 Servlet 容器对于单进程、多线程 的服务器非常适合，提供了较高的运行速度，但伸缩性有所不足。

3）进程外的 Servlet 容器

Servlet 容器运行于 Web 服务器之外的地址空间，它也是由 Web 服务器插件和 Java 容器两部分的实现组成的。Web 服务器插件和 Java 容 器（在外部 JVM 中运行）使用 IPC 机制（通常是 TCP/IP）进行通信。当一个调用 Servlet 的请求到达时，插件取得对此请求的控制并将其传递（使 用 IPC 机制）给 Java 容器。进程外 Servlet 容器对客户请求的响应速度不如进程内的 Servlet 容器，但进程外容器具有更好的伸缩性和稳定性。

## 内建模块

核心容器由 spring-core、spring-beans、spring-context、spring-context-support 和 spring-expression 模块组成：

- spring-core 和 spring-beans 提供框架的基础部分，包括 IOC 功能，BeanFactory 是一个复杂的工厂模式的实现，将配置和特定的依赖从实际程序逻辑中解耦。

- context 模块建立在 core 和 beans 模块的基础上，增加了对国际化的支持、事件广播、资源加载和创建上下文，ApplicationContext 是 context 模块的重点。

- spring-context-support 提供对常见第三个库的支持，集成到 spring 上下文中，比如缓存(ehcache,guava)、通信(javamail)、调度(commonj,quartz)、模板引擎等(freemarker,velocity)。

- spring-expression 模块提供了一个强大的表达式语言用来在运行时查询和操作对象图，这种语言支持对属性值、属性参数、方法调用、数组内容存储、集合和索引、逻辑和算数操作及命名变量，并且通过名称从 spring 的控制反转容器中取回对象。

AOP 和服务器工具

- spring-aop 模块提供面向切面编程实现，单独的 spring-aspects 模块提供了 aspectj 的集成和适用。

- spring-instrument 提供一些类级的工具支持和 ClassLoader 级的实现，用于服务器。spring-instrument-tomcat 针对 tomcat 的 instrument 实现。

消息组件

- Spring 4 包含了 spring-messaging 模块，从 spring 集成项目中抽象出来，比如 Messge、MessageChannel、MessageHandler 及其他用来提供基于消息的基础服务。

数据访问和集成层由 JDBC、ORM、OXM、JMS 和事务模块组成。

- spring-jdbc 模块提供了不需要编写冗长的 JDBC 代码和解析数据库厂商特有的错误代码的 JDBC 抽象出。

- spring-tx 模块提供可编程和声明式事务管理。

- spring-orm 模块提供了领先的对象关系映射 API 集成层，如 JPA、Hibernate 等。

- spring-oxm 模块提供抽象层用于支持 Object/XML maping 的实现，如 JAXB、XStream 等。

- spring-jms 模块包含生产和消费消息的功能，从 Spring4.1 开始提供集成 spring-messaging 模块。

Web 层包含 spring-web、spirng-webmvc、spring-websocket 和 spring-webmvc-portlet 等模块。

- spring-web 模块提供了基本的面向 web 开发的集成功能，例如多文件上传、使用 servert listeners 和 web 开发应用程序上下文初始化 IOC 容器。也包含 HTTP 客户端以及 spring 远程访问的支持的 web 相关部分。

- spring-webmvc 包含 spring 的 model-view-controller 和 REST web services 实现的 Web 应用程序。

- spring-webmvc-portlet 模块提供了 MVC 模式的 portlet 实现，protlet 与 Servlet 的最大区别是请求的处理分为 action 和 render 阶段，在一个请求中，action 阶段只执行一次，但 render 阶段可能由于用户的浏览器操作而被执行多次。

传统的 Spring MVC 基于 Servlet API 构建，使用单请求单线程处理的同步阻塞型模型；而 Spring WebFlux 则是 Reactive Stack，能够充分利用现代多核处理器的特性，从底层机制上保证了对于海量并发请求处理的能力。WebFlux 使用 Netty, Servlet 3.1+ Containers 替代传统的 Servlet Containers，使用 Reactive Stream Adapters 替代 Servlet API，使用 Spring Security Reactive 替代 Spring Security，使用 Spring Data Reactive Repositories 替代 Spring Data Repositories。

spring-test 模块支持通过组合 Junit 或 TestNG 来进行单元测试和集成测试，提供了连续的加载 ApplicationContext 并且缓存这些上下文。

## 生态圈

Spring Boot 简化新 Spring 应用的初始搭建以及开发过程，使用特定的方式进行配置，使开发人员不再需要定义样板化的配置，实现快速开发。数据访问模块，提供了对 JDBC 及 ORM 很好的支持，随着 NOSQL 和 BigData 的兴起，出现了越来越多的新技术，比如非关系型数据库、MapReduce 框架，为了让 spring 开发者能更方便地使用这些新技术，通过 Spring Data，开发者可以用 Spring 提供的相对一致的方式访问位于不同类型的数据存储中的数据。Spring Cloud Data Flow 是基于原生云对 Spring XD 的重新设计，项目目标是简化大数据应用的开发。Spring XD 的流处理和批处理模块的重构分别基于 spring boot 的 stream 和 task/batch 的微服务程序。这些程序原生的支持像 Apache YARN、Apache Mesos 和 Kubernetes 等现代运行环境，都是自动部署单元。

Spring Cloud 为分布式系统开发提供工具集，基于 Spring Boot，为基于 JVM 的云应用开发中的配置管理、服务发现、断路器、智能路由、控制总线、全局锁、决策竞选、分布式会话、集群状态管理等操作提供了一种简单的开发方式，其下有很多子项目。

- 分布式/版本化配置：Spring Cloud Config

- 服务注册和发现：Netflix Eureka 或者 Spring Cloud Eureka（对前者的二次封装）

- 路由：Spring Cloud Zuul，基于 Netflix Zuul

- service - to - service 调用：Spring Cloud Feign

- 负载均衡：Spring Cloud Ribbon 基于 Netflix Ribbon 实现

- 断路器：Spring Cloud Hystrix

- 分布式消息传递：Spring Cloud Bus

Spring Batch 简化及优化大量数据的批处理操作，支持事务、并发、流程、监控、纵向和横向扩展，提供统一的接口管理和任务管理。例如它提供了很多方法来读取大型的文件（比如 1GB 的 CSV、XML 文件），在数据库中加载或更新几万甚至几十万条记录，如果直接 select 出所有记录，以至于拖垮整个系统，而使用了 Spring Batch，框架会帮助他每次捞取一部分记录进行分页，在更新时分批进行提交。

Spring Security 是一款 Spring 的认证和安全工具。其前身是 Acegi，目标是为 Spring 应用提供一个安全服务，比如用户认证、授权等。它使用 Servlet 规范中的 Filter 保护 Web 请求并限制 URL 级别的访问，还能够使用 Spring AOP 保护方法调用——借助于对象代理和使用通知，能够确保只有具备适当权限的用户才能访问安全保护的方法。它非常灵活，能够基于各种数据存储来认证用户。它内置了多种常见的用户存储场景，如内存、关系型数据库以及 LDAP，还可以编写并插入自定义的用户存储实现。
