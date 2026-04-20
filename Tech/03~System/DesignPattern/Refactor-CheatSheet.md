# Clean Code, Review & Refactor | 简洁代码、审视与重构

Working Effectively with Legacy Code, by Michael Feathers. This book will give you an appreciation of what it is like to work with long-lived code bases, and how to write code now so future You (and future Your Colleagues) can be happy developers. Refactoring: Improving the Design of Existing Code, by Martin Fowler. You’ll get a whole new appreciation for the word “refactoring” after reading this book. Design Patterns: Elements of Reusable Object-Oriented Software, by Erich Gamma et al. This is also famously knows as the Gang of Four book. If you want a simpler version of this, check out Head First Design Patterns too.

- CamelCase 适用于类与接口名。
- snakeCase 适用于变量与方法名。
- SCREAMING_SNAKE_CASE 适用于常量名。
- sPoNgEbOb_SnAkE_cAsE 适用于讨厌的名字。

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.

Michael Feathers 在他的《修改代码的艺术》一书中，提出了当我们听到“遗留代码”的时候会想到什么：
如果你也和我一样，那么大抵会联想到错综复杂的、难以理清的结构，需要改变然而实际上又根本无法理解的代码；你会联想到那些不眠之夜，试图添加一个本该很容易就添加上去的特性；你会联想到自己是如何的垂头丧气，以及你的团队中的每个人对一个似乎没人管的代码库是如何打心底里感到厌烦的，这种代码简直让你生不如死。你内心深处甚至对于想一想怎样才能改善这种代码都感到痛苦。这种事情似乎太不值得我们付出努力了。

# 编码规约

这里用规约二字，而非规范，也是希望能表明，在各个团队的独特业务场景、开发语言、编码习惯下，支持对该规约的二次解释。

Data is better than code.

Store data in your state, send data over the wire, dispatch based on data.

Everything should be CQRS.

(Almost) Everything should be pubsub.

A subscriber shouldn't affect a publisher.

Communication between nodes should be communication between independent actors.

Each message should do one complete thing, and there shouldn't need to be a sequence of coupled messages.

Represent your data as closely as possible to the essential structure of the problem.

A client's representation of data should be as close as possible to that of the server.

This blurs the distinction between client and server. It allows offline-mode, reduces communication to syncing, and decentralizes.

When mating different paradigms, build one cleanly on top of the other.

Never try to make them work on some of the same primitives. Never abuse one to make the other work. For example, ducts in themselves are very general - if you want to do pubsub, that can easily be built on top of ducts, but don't pretend that pubsub is a part of the duct system.

Never misuse an abstraction.

An abstraction provides a certain set of tools; use them and only them.

Correctness is more important than performance.

Be simple and uncompromising in defining what's correct; go crazy with optimizations.

Nock is a great example of this. It contains the character of the virtual machine, but its asymptotics are bad. Add jets to fix the asymptotics.

Another example is the ACID nature of Arvo. Arvo is a pure function f(logs) of its event log, so formally Arvo is just a function run against an event log. A naive implementation has very bad asymptotics; processing each new event is O(n) in the number of historical events. Choose the function g(state,log) such that f(logs ++ log) = g(f(logs),log). Then, as long as you keep the state in memory, processing each new event is constant in the number of previous events. This still requires O(n) restart from disk, but you can also periodically (and non-blockingly) write a checkpoint of the state to disk, so that restart from disk is only linear in the number of events since the last checkpoint.

Correctness is more important than optimality.

If you don't completely understand your code and the semantics of all the code it depends on, your code is wrong.

Deterministic beats heuristic.

Heuristics are evil and should only be used where determinism is infeasible, such as in cache reclamation.

Stateless is better than stateful.

Explicit state is better than implicit state.

Referential transparency is honesty and stability.

Lack of referential transparency and other forms of disingenuousness are some of the world's big problems. Only deviate from referential transparency if absolutely necessary.

Responsibilities should be clearly separated.

This applies from kernel modules through network citizens.

Dualities must be faced head-on and analyzed differently at different layers.

Statically typed vs. dynamically typed, imperative vs. functional, code vs. data, and effectful vs. pure can all be a matter of perspective, and all relevant perspectives must have coherent answers.

One hundred lines of simplicity is better than twenty lines of complexity.

It's not enough for an abstraction to reduce code duplication; it must actually make the code simpler.

Prefer mechanical simplicity to mathematical simplicity.

Often mechanical simplicity and mathematical simplicity go together.

The Law of Leaky Abstractions is a lie; abstract airtightly.

If your abstractions are leaking, it's not due to some law of the universe; you just suck at abstracting. Usually, you didn't specify the abstraction narrowly enough.

# Attitude

Code courageously.

If you avoid changing a section of code for fear of awakening the demons therein, you are living in fear. If you stay in the comfortable confines of the small section of the code you wrote or know well, you will never write legendary code. All code was written by humans and can be mastered by humans.

It's natural to feel fear of code; however, you must act as though you are able to master and change any part of it. To code courageously is to walk into any abyss, bring light, and make it right.

No time for lazy people.

If there's clearly a right way to do something and a wrong way, do it the right way. Coding requires incredible discipline. Always follow conventions, and fire anyone who won't. Anything that can be solved by discipline is not a real problem.

"To him who knows to do good and does not do it, to him it is sin."

When a smart person makes an obviously stupid suggestion, before responding take a full 60 seconds to envision how you would implement it and what the effects would be.