
<!--introduced_in=v0.10.0-->
<!-- type=misc -->

插件是用 C++ 编写的动态链接共享对象。
[`require()`][require] 函数可以将插件加载为普通的 Node.js 模块。
插件提供了 JavaScript 和 C/C++ 库之间的接口。

实现插件有三种选择：N-API、nan、或直接使用内部的 V8、libuv 和 Node.js 库。 
除非需要直接访问 N-API 未公开的函数，否则请使用 N-API。 
有关 N-API 的更多信息，参见[具有 N-API 的 C/C++ 插件][_n-api]。

当不使用 N-API 时，实现插件很复杂，涉及多个组件和 API 的知识：

 - V8：Node.js 用于提供 JavaScript 实现的 C++ 库。
   V8 提供了用于创建对象、调用函数等的机制。
   V8 的 API 文档主要在 `v8.h` 头文件中（Node.js 源代码树中的 `deps/v8/include/v8.h`），也可以在查看[在线文档][v8-docs]。

 - [libuv]：实现了 Node.js 的事件循环、工作线程、以及平台所有的的异步行为的 C 库。
   它也是一个跨平台的抽象库，使所有主流操作系统中可以像 POSIX 一样访问常用的系统任务，比如与文件系统、socket、定时器、以及系统事件的交互。
   libuv 还提供了一个类似 POSIX 多线程的线程抽象，可被用于强化更复杂的需要超越标准事件循环的异步插件。
   建议插件开发者多思考如何通过在 libuv 的非阻塞系统操作、工作线程、或自定义的 libuv 线程中降低工作负载来避免在 I/O 或其他时间密集型任务中阻塞事件循环。

 - 内置的 Node.js 库。Node.js 自身公开了插件可以使用的 C++ API，其中最重要的是 `node::ObjectWrap` 类。

 - Node.js 包含了其他的静态链接库，如 OpenSSL。
   这些库位于 Node.js 源代码树中的 `deps/` 目录。
   只有 libuv、OpenSSL、V8 和 zlib 符号是被 Node.js 有目的地重新公开，并且可以被插件在不同程度上使用。
   更多信息可查看[链接到 Node.js 自带的库][Linking to libraries included with Node.js]。

以下所有示例均可供[下载][download]，并可用作学习插件的起点。

