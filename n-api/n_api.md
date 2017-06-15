
> 稳定性: 1 - 试验的

N-API 是一个用于构建原生插件的 API。
它独立于底层的 JavaScript 运行时（除 V8 外），且作为 Node.js 自身的一部分。
这个 API 会是稳定跨越 Node.js 版本的应用二进制接口（ABI）。
它的目的是要使插件独立于底层 JavaScript 引擎的变化，使得为一个版本编译的模块可以无需再编译也能运行于以后的 Node.js 版本。

插件使用与 [C++ 插件] 章节中概述的相同的方法或工具进行构建或打包。
唯一的区别是被原生代码使用的 API 集合。
它使用的是 N-API 函数而不是 V8 或 [nan] API。

N-API 开放的 API 通常被用于创建或操作 JavaScript 值。
概念与运作通常映射 ECMA262 语言规范中定义的思想。
这些 API 有以下属性：
- 所有 N-API 的调用会返回一个 `napi_status` 类型的状态码。
  这个状态码表示 API 的调用是否成功或失败。
- API 的返回值通过一个外部的参数传递。
- 所有 JavaScript 值抽象于 `napi_value` 类型。
- 如果出现一个错误状态码，可以使用 `napi_get_last_error_info` 获取更多的信息。
  详见 [错误处理] 章节。

N-API 文档的结构如下：

* [基本的 N-API 数据类型]
* [错误处理]
* [对象的生命周期管理]
* [模块注册]
* [处理 JavaScript 值]
* [处理 JavaScript 值 - 抽象操作]
* [处理 JavaScript 属性]
* [处理 JavaScript 函数]
* [对象封装]
* [异步操作]

N-API 是一个 C 语言的 API，它能确保应用二进制接口（ABI）在不同 Node.js 版本与不同编译器级别之间保持稳定。
但是在许多情况下，C++ 的 API 更容易使用。
为了支持这些情况，我们期望有一个或多个 C++ 封装的模块提供可内联的 C++ API。
用这些模块构建的二进制文件会依赖于 N-API C 的符号文件。
这些模块不是 N-API 的一部分，也不是 Node.js 的一部分。
例子可见 [node-api]。

为了使用 N-API 函数，需要引入 [node_api.h] 文件。
例如：
```C
#include <node_api.h>
```

因为该特性是试验性的，所以需要使用命令行选项 [`--napi-modules`] 启用：

```bash
--napi-modules
```

