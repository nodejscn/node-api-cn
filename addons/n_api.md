
> Stability: 2 - Stable

N-API是用于构建本机插件的API。它独立于底层JavaScript运行时（例如V8），并作为Node.js本身的一部分进行维护。此API将是跨Node.js版本的应 Application Binary Interface（ABI）稳定版。它旨在将Addons与底层JavaScript引擎中的更改隔离开来，并允许为一个版本编译的模块在更高版本的Node.js上运行而无需重新编译。插件使用本文档中概述的相同方法/工具（node-gyp等）构建/打包。唯一的区别是原始代码使用的API集。不使用V8或Native [Abstractions for Node.js API](https://github.com/nodejs/nan)，而是使用N-API中可用的功能。


要在上面的“Hello world”示例中使用N-API，请使用以下内容替换`hello.cc`的内容。所有其他说明保持不变。

```cpp
// hello.cc using N-API
#include <node_api.h>

namespace demo {

napi_value Method(napi_env env, napi_callback_info args) {
  napi_value greeting;
  napi_status status;

  status = napi_create_string_utf8(env, "hello", NAPI_AUTO_LENGTH, &greeting);
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

可用功能和使用文档在这里 [C/C++ Addons - N-API](n-api.html).

