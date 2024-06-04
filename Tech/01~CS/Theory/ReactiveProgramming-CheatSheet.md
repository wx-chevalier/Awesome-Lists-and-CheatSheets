# Reactive Programming CheatSheet

Reactive Programming is an asynchronous programming paradigm concerned with data streams and the propagation of change.

React to User's Input X, and respond ASAP，而非简单地 Response to X。响应一般来说，对应的英文为 Response、动词为 Respond、形容词为 Responsive。在 The Reactive Manifesto 中的 Reactive 实际上是指一个副词，表示系统总是会积极主动、甚至是智能地对内外的变化做出反应，其中包括：

React to user：Respond ASAP，尽可能快速地对用户的请求给出应答——即时响应性，这也是最终目的和核心商业价值。
React to load，尽可能地对上游给出的压力做出反应，包括智能限流、回压、百分比丢弃等策略，为的是尽可能地降低对用户体验的损害，同时保护系统。
React to failure，尽可能地在系统发生失败时，对失败进行妥善处理，而非不受控的级联失败。

# 反应式系统特性

即时响应性:：只要有可能，系统就会及时地做出响应。即时响应是可用性和实用性的基石，而更加重要的是，即时响应意味着可以快速地检测到问题并且有效地对其进行处理。即时响应的系统专注于提供快速而一致的响应时间，确立可靠的反馈上限，以提供一致的服务质量。这种一致的行为转而将简化错误处理、建立最终用户的信任并促使用户与系统作进一步的互动。
回弹性：系统在出现失败时依然保持即时响应性。这不仅适用于高可用的、任务关键型系统——任何不具备回弹性的系统都将会在发生失败之后丢失即时响应性。回弹性是通过复制、遏制、隔离以及委托来实现的。失败的扩散被遏制在了每个组件内部，与其他组件相互隔离，从而确保系统某部分的失败不会危及整个系统，并能独立恢复。每个组件的恢复都被委托给了另一个（外部的）组件，此外，在必要时可以通过复制来保证高可用性。（因此）组件的客户端不再承担组件失败的处理。
弹性：系统在不断变化的工作负载之下依然保持即时响应性。反应式系统可以对输入（负载）的速率变化做出反应，比如通过增加或者减少被分配用于服务这些输入（负载）的资源。这意味着设计上并没有争用点和中央瓶颈，得以进行组件的分片或者复制，并在它们之间分布输入（负载）。通过提供相关的实时性能指标，反应式系统能支持预测式以及反应式的伸缩算法。这些系统可以在常规的硬件以及软件平台上实现成本高效的弹性。
消息驱动：反应式系统依赖异步的消息传递，从而确保了松耦合、隔离、位置透明的组件之间有着明确边界。这一边界还提供了将失败作为消息委托出去的手段。使用显式的消息传递，可以通过在系统中塑造并监视消息流队列，并在必要时应用回压，从而实现负载管理、弹性以及流量控制。使用位置透明的消息传递作为通信的手段，使得跨集群或者在单个主机中使用相同的结构成分和语义来管理失败成为了可能。非阻塞的通信使得接收者可以只在活动时才消耗资源，从而减少系统开销。

任务划分
Scheduler 调度器
Context 支持：Coroutine Context 和 Reactor Context
但是有几点是目前 Coroutine 是做不到的：

Reactive 几乎所有的语言都支持，但是协程未必所有语言都支持，JavaScript 好像就没有
Reactive 的编程体验是一致的：不管你使用任何语言，使用 Reactive，代码就得这样写，每一个人都能编写，而且容易阅读
Reactor 的 Operator：Reactive 提供了大量操作方法，各种数学操作简单明了，RxJava 的 https://github.com/akarnokd/RxJava2Extensions Reactor 的 addons https://github.com/reactor/reactor-addons 相反使用协程你需要自己搞定 Java 同学一直头疼的空指针问题，在 Reactive 中也非常容易地规避。这些 Operator 方法都非常使用，而且使用流畅。

Akka Stream: Akka 比较老牌，Actor 模式大家都知道，Akka Stream 主要是瞄准 Reactive 的，而且扩展也非常多 https://github.com/akka/alpakka 就是非常复杂，普通 Java 程序员上手太慢，如果你喜欢 Scala 那就另当别论啦。
Reactor：最年轻的，所以通过一个 Adapter，可以将 RxJava 和 Akka Stream 都能转换到 Reactor 上。Reactor 最大的优势是和 Spring 社区的整合，如果你已经使用 Spring Framework 啦，那最好使用 Reactor，你坐享 Spring 带来的 Reactive 成果就可以啦，什么 Reactive JPA，R2DBC, Webflux，包括 RSocket，全部 ready 啦。另外个人认为，Spring 相关产品的 API 设计都是最佳的，学习和使用成本都是最低的。
