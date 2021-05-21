
> 稳定性: 2 - 稳定的

Node-API 是一个用于构建原生插件的 API。
它独立于底层的 JavaScript 运行时（例如 V8），并且被维护作为 Node.js 自身的一部分。
此 API 在所有版本的 Node.js 都是稳定的应用程序二进制接口（ABI）。
它旨在隔离插件与底层 JavaScript 引擎中的更改，并且允许为一个版本编译的模块运行在更高版本的 Node.js 上无需重新编译。
插件被本文档中概述的相同方法或者工具（node-gyp 等）所构建或者打包。
唯一的区别是被原生代码所使用的 API 集。
不是使用 V8 或者 [Node.js 的原生抽象][Native Abstractions for Node.js]，而是使用 Node-API 中可用的函数。

创建和维护一个受益于 Node-API 提供的 ABI 稳定性的插件会带来某些[实现的注意事项][_implementation_considerations]。

要在上面的“你好世界”示例中使用 Node-API，则替换 `hello.cc` 的内容为以下的内容。
所有的其他指令保持不变。

```cpp
// 使用 Node-API 的 hello.cc
#include <node_api.h>

namespace demo {

napi_value Method(napi_env env, napi_callback_info args) {
  napi_value greeting;
  napi_status status;

  status = napi_create_string_utf8(env, "world", NAPI_AUTO_LENGTH, &greeting);
  if (status != napi_ok) return nullptr;
  return greeting;
}

napi_value init(napi_env env, napi_value exports) {
  napi_status status;
  napi_value fn;

  status = napi_create_function(env, nullptr, 0, Method, nullptr, &fn);
  if (status != napi_ok) return nullptr;

  status = napi_set_named_property(env, exports, "hello", fn);
  if (status != napi_ok) return nullptr;
  return exports;
}

NAPI_MODULE(NODE_GYP_MODULE_NAME, init)

}  // namespace demo
```

可用的函数以及如何使用它们的文档在[使用 Node-API 的 C/C++ 插件][_n-api]。

