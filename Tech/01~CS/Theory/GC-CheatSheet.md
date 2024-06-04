# Overview | 概述

Application memory management involves supplying the memory needed for a program’s objects and data structures from the limited resources available, and recycling that memory for reuse when it is no longer required. Because application programs cannot in general predict in advance how much memory they are going to require, they need additional code to handle their changing memory requirements.

基于引用计数与基于 trace 这两大类别的自动内存管理方式最大的不同之处在于：前者只需要局部信息，而后者需要全局信息。引用计数方式最基本的形态就是让每个被管理的对象与一个引用计数器关联在一起，该计数器记录着该对象当前被引用的次数，每当创建一个新的引用指向该对象时其计数器就加 1，每当指向该对象的引用失效时计数器就减 1。当该计数器的值降到 0 就认为对象死亡。每个计数器只记录了其对应对象的局部信息——被引用的次数，而没有（也不需要）一份全局的对象图的生死信息。由于只维护局部信息，所以不需要扫描全局对象图就可以识别并释放死对象；但也因为缺乏全局对象图信息，所以无法处理循环引用的状况。更高级的引用计数实现会引入“弱引用”的概念来打破某些已知的循环引用，但那是另一个话题了。

在实际实现中，引用计数存在什么地方是个有趣的话题。可以侵入式的存在对象内，例如 CPython 就把引用计数存在每个受自动内存管理的 Python 对象的对象头里（PyObject 的 ob_refcnt 字段），或者 COM 的 IUnknown::AddRef()/Release()；也可以非侵入式的存在对象外面，例如 C++11 标准库里的 std::shared_ptr。计数器的管理（自增/自减）可能由人工完成，例如老的 Objective-C，或者是从 C++里使用 COM，等等；也可能是自动管理，例如 CPython、使用“自动引用计数”（ARC）的 Objective-C、C++/CX 的“hat”、前面提到的 C++11 的 std::shared_ptr 等等。如果能自动管理，那么必然有一套明确的规则说明何种情况下一个引用会被认为失效；以 std::shared_ptr 为例的话，其析构函数被调用（例如离开作用域时）或者其指向别的对象时，原本指向的对象的引用计数就会减 1。

Tracing GC 与引用计数正好相反，需要全局的对象图信息，从对象图的“根”（也就是必然活的引用）出发扫描出去，基于引用的可到达性来判断对象的生死。这使得对象的生死状态只能批量的被识别出来，然后批量释放死对象。Tracing GC 不显式维护对象的引用计数，只在 trace 的时候才能回答“有”还是“没有”活引用指向某个对象。实际上，在内存充裕的前提下，tracing GC 的整体开销比引用计数方式更低一些，所以吞吐量（throughput）高一些。因为引用计数方式通常需要统计冗余的局部信息，而 tracing GC 则可以通过全局信息一口气批量判断对象的生死；如果是带整理的 tracing GC，则其内存分配通常也会更快。不过 tracing GC 通常会比引用计数方式的延迟（latency）大一些，而且内存越紧张的时候 tracing GC 的效率反而越低，所以在内存不太充裕的地方使用引用计数仍然是个合理的选择（例如 iOS5 上的 ARC）。

## Tasks | 任务

Allocation

When the program requests a block of memory, the memory manager must allocate that block out of the larger blocks it has received from the operating system. The part of the memory manager that does this is known as the allocator. There are many ways to perform allocation, a few of which are discussed in Allocation techniques.
Recycling

When memory blocks have been allocated, but the data they contain is no longer required by the program, then the blocks can be recycled for reuse. There are two approaches to recycling memory: either the programmer must decide when memory can be reused (known as manual memory management); or the memory manager must be able to work it out (known as automatic memory management).

## Metric | 指标

CPU overhead

The additional time taken by the memory manager while the program is running.
Pause times

The time it takes for the memory manager to complete an operation and return control to the program.

This affects the program’s ability to respond promptly to interactive events, and also to any asynchronous event such as a network connection.

Memory overhead

How much space is wasted for administration, rounding (known as internal fragmentation), and poor layout (known as external fragmentation).

# Challenge | 挑战

The basic problem in managing memory is knowing when to keep the data it contains, and when to throw it away so that the memory can be reused.

Premature frees and dangling pointers

Many programs give up memory, but attempt to access it later and crash or behave randomly. This condition is known as a premature free, and the surviving reference to the memory is known as a dangling pointer. This is usually confined to manual memory management.
Memory leak

Some programs continually allocate memory without ever giving it up and eventually run out of memory. This condition is known as a memory leak.
External fragmentation

A poor allocator can do its job of giving out and receiving blocks of memory so badly that it can no longer give out big enough blocks despite having enough spare memory. This is because the free memory can become split into many small blocks, separated by blocks still in use. This condition is known as external fragmentation.
Poor locality of reference

Another problem with the layout of allocated blocks comes from the way that modern hardware and operating system memory managers handle memory: successive memory accesses are faster if they are to nearby memory locations. If the memory manager places far apart the blocks a program will use together, then this will cause performance problems. This condition is known as poor locality of reference.
Inflexible design

Memory managers can also cause severe performance problems if they have been designed with one use in mind, but are used in a different way. These problems occur because any memory management solution tends to make assumptions about the way in which the program is going to use memory, such as typical block sizes, reference patterns, or lifetimes of objects. If these assumptions are wrong, then the memory manager may spend a lot more time doing bookkeeping work to keep up with what’s happening.
Interface complexity

If objects are passed between modules, then the interface design must consider the management of their memory.

## Maunal & Atomic

Manual memory management is where the programmer has direct control over when memory may be recycled. Usually this is either by explicit calls to heap management functions (for example, malloc and free(2) in C), or by language constructs that affect the control stack (such as local variables).

some manual memory managers perform better when there is a shortage of memory. 不过开发者必须编写大量的额外的内存管理相关的代码，并且极有可能过量分配内存或者造成其他的错误。

Automatic memory management is a service, either as a part of the language or as an extension, that automatically recycles memory that a program would not otherwise use again. Automatic memory managers (often known as garbage collectors, or simply collectors) usually do their job by recycling blocks that are unreachable from the program variables (that is, blocks that cannot be reached by following pointers). memory may be retained because it is reachable, but won’t be used again;
automatic memory managers (currently) have limited availability.
