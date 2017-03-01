
“Hello World” 示例是一个简单的插件，用 C++ 编写，相当于以下 JavaScript 代码：

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
  args.GetReturnValue().Set(String::NewFromUtf8(isolate, "world"));
}

void init(Local<Object> exports) {
  NODE_SET_METHOD(exports, "hello", Method);
}

NODE_MODULE(addon, init)

}  // namespace demo
```

注意，所有的 Node.js 插件必须导出一个如下模式的初始化函数：

```cpp
void Initialize(Local<Object> exports);
NODE_MODULE(module_name, Initialize)
```

`NODE_MODULE` 后面没有分号，因为它不是一个函数（详见 `node.h`）。

`module_name` 必须匹配最终的二进制文件名（不包括 .node 后缀）。

在 `hello.cc` 示例中，初始化函数是 `init`，插件模块名是 `addon`。

