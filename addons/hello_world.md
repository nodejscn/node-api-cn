
这个“你好世界”的示例是一个简单的用 C++ 编写的插件，它相当于以下的 JavaScript 代码：

```js
module.exports.hello = () => 'world';
```

首先，创建 `hello.cc` 文件：

```cpp
// hello.cc
#include <node.h>

namespace demo {

using v8::FunctionCallbackInfo;
using v8::Isolate;
using v8::Local;
using v8::Object;
using v8::String;
using v8::Value;

void Method(const FunctionCallbackInfo<Value>& args) {
  Isolate* isolate = args.GetIsolate();
  args.GetReturnValue().Set(String::NewFromUtf8(
      isolate, "world").ToLocalChecked());
}

void Initialize(Local<Object> exports) {
  NODE_SET_METHOD(exports, "hello", Method);
}

NODE_MODULE(NODE_GYP_MODULE_NAME, Initialize)

}  // namespace demo
```

所有的 Node.js 插件必须遵循以下的模式导出一个初始化函数：

```cpp
void Initialize(Local<Object> exports);
NODE_MODULE(NODE_GYP_MODULE_NAME, Initialize)
```

`NODE_MODULE` 后面没有分号，因为它不是一个函数（查看 `node.h`）。

`module_name` 必须匹配最终的二进制文件名（不包括 `.node` 后缀）。

在该 `hello.cc` 示例中，初始化函数是 `Initialize`，并且该插件的模块名是 `addon`。

当使用 `node-gyp` 构建插件时，使用宏 `NODE_GYP_MODULE_NAME` 作为 `NODE_MODULE()` 的第一个参数会确保最终的二进制文件的名称会被传给 `NODE_MODULE()`。

