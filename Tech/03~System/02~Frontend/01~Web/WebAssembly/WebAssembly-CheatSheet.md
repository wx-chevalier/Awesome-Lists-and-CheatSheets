# WebAssembly CheatSheet

WebAssembly 是一种新的字节码格式，主流浏览器都已经支持 WebAssembly。和 JS 需要解释执行不同的是，WebAssembly 字节码和底层机器码很相似可快速装载运行，因此性能相对于 JS 解释执行大大提升。也就是说 WebAssembly 并不是一门编程语言，而是一份字节码标准，需要用高级编程语言编译出字节码放到 WebAssembly 虚拟机中才能运行，浏览器厂商需要做的就是根据 WebAssembly 规范实现虚拟机。

# Linear Memory

These languages also needed to be able to use memory differently from how JavaScript uses memory. They needed to be able to directly manage their memory—to say which bytes go together.

This is because languages like C and C++ have a low-level feature called pointers. You can have a variable that doesn’t have a value in it, but instead has the memory address of the value. So if you’re going to support pointers, the program needs to be able to write and read from particular addresses.

But you can’t have a program you downloaded from the web just accessing bytes in memory willy-nilly, using whatever addresses they want. So in order to create a secure way of giving access to memory, like a native program is used to, we had to create something that could give access to a very specific part of memory and nothing else.

To do this, WebAssembly uses a linear memory model. This is implemented using TypedArrays. It’s basically just like a JavaScript array, except this array only contains bytes of memory. When you access data in it, you just use array indexes, which you can treat as though they were memory addresses. This means you can pretend this array is C++ memory.

# Threads

Browsers have supported parallelism via Web Workers since 2012 in Chrome 4; in fact it's normal to hear terms like 'on the main thread' etc. However, Web Workers do not share mutable data between them, instead relying on message-passing for communication. In fact, Chrome allocates a new V8 engine for each of them (called isolates). Isolates share neither compiled code nor JavaScript objects, and thus they cannot share mutable data like pthreads.

WebAssembly threads, on the other hand, are threads that can share the same Wasm memory. The underlying storage of the shared memory is accomplished with a SharedArrayBuffer, a JavaScript primitive that allows sharing a single ArrayBuffer's contents concurrently between workers. Each WebAssembly thread runs in a Web Worker, but their shared Wasm memory allows them to work much like they do on native platforms. This means that the applications that use Wasm threads are responsible for managing access to the shared memory as in any traditional threaded application. There are many existing code libraries written in C or C++ that use pthreads, and those can be compiled to Wasm and run in true threaded mode, allowing more cores to work on the same data simultaneously.
