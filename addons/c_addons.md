
<!--introduced_in=v0.10.0-->
<!-- type=misc -->

插件是用 C++ 编写的动态链接的共享对象。
[`require()`][require] 函数可以加载插件作为普通的 Node.js 模块。
插件提供了一个 JavaScript 和 C/C++ 库之间的接口。

有三种实现插件的选择：Node-API、nan、或者内部 V8、libuv 和 Node.js 库的直接使用。 
除非需要未被 Node-API 暴露的功能的直接访问，否则使用 Node-API。 
查看[使用 Node-API 的 C/C++ 插件][_n-api]获取 Node-API 的更多信息。

当不使用 Node-API 时，实现插件是复杂的，涉及多个组件和 API 的知识：

* [V8]：Node.js 用于提供 JavaScript 实现的 C++ 库。
  V8 提供了用于创建对象、调用函数等的机制。
  V8 的 API 文档主要在 `v8.h` 头文件中（Node.js 源码树中的 `deps/v8/include/v8.h`），也有[在线的文档][v8-docs]。

* [libuv]：实现 Node.js 事件循环、工作线程、以及平台的所有异步行为的 C 库。
  它也作为一个跨平台的抽象库，让所有的主流操作系统对许多常用的系统任务（例如与文件系统、套接字、定时器、以及系统事件的交互）具有简单的、类 POSIX 的访问。
  libuv 还提供一个类似 POSIX 线程的线程抽象，用于更复杂的需要超越标准的事件循环的异步插件。
  插件作者应该通过 libuv 将工作分流到非阻塞的系统操作、工作线程、或者一个自定义的 libuv 线程的使用来避免因 I/O 或者其他的时间密集型任务而阻塞事件循环。
  
* 内部的 Node.js 库。Node.js 自身导出了插件可以使用的 C++ API，其中最重要的是 `node::ObjectWrap` 类。

* Node.js 包含其他的静态链接库，例如 OpenSSL。
  这些其他的库位于 Node.js 源码树中的 `deps/` 目录中。
  只有 libuv、OpenSSL、V8 和 zlib 符号是被 Node.js 有意地重新导出，并且可以被插件不同程度地使用。
  查看[链接到 Node.js 包含的库][Linking to libraries included with Node.js]获取其他的信息。

以下所有的示例均可[下载][download]，并且可被用作一个插件的起点。

