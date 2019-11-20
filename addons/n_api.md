
> 稳定性: 2 - 稳定

N-API 是用于构建本机插件的API。
它独立于底层 JavaScript 运行时（例如 V8），并作为 Node.js 本身的一部分进行维护。
此 API 将是跨 Node.js 版本的应用程序二进制接口（Application Binary Interface，ABI）稳定版。
它旨在将插件与底层 JavaScript 引擎中的更改隔离开来，并允许为一个版本编译的模块在更高版本的 Node.js 上运行而无需重新编译。
插件使用本文档中概述的相同方法/工具（node-gyp 等）构建/打包。
唯一的区别是原始代码使用的 API 集。
不使用 V8 或 [Node.js 的原生抽象][Native Abstractions for Node.js]，而是使用 N-API 中可用的功能。

创建和维护受益于 N-API 提供的 ABI 稳定性的插件会带来某些[实现的注意事项][_implementation_considerations]。

要在上面的 “Hello world” 示例中使用 N-API，请使用以下内容替换 `hello.cc` 的内容。
所有其他说明保持不变。

```cpp
// hello.cc using N-API
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

可用的函数和使用文档请参阅[具有 N-API 的 C/C++ 插件][_n-api]。

