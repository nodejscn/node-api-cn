
把 JavaScript 函数传入到一个 C++ 函数并在那里执行它们，这在插件里是常见的做法。
以下例子描述了如何调用这些回调：

```cpp
// addon.cc
#include <node.h>

namespace demo {

using v8::Function;
using v8::FunctionCallbackInfo;
using v8::Isolate;
using v8::Local;
using v8::Null;
using v8::Object;
using v8::String;
using v8::Value;

void RunCallback(const FunctionCallbackInfo<Value>& args) {
  Isolate* isolate = args.GetIsolate();
  Local<Function> cb = Local<Function>::Cast(args[0]);
  const unsigned argc = 1;
  Local<Value> argv[argc] = { String::NewFromUtf8(isolate, "hello world") };
  cb->Call(Null(isolate), argc, argv);
}

void Init(Local<Object> exports, Local<Object> module) {
  NODE_SET_METHOD(module, "exports", RunCallback);
}

NODE_MODULE(addon, Init)

}  // namespace demo
```

注意，该例子使用了一个带有两个参数的 `Init()`，它接收完整的 `module` 对象作为第二个参数。
这使得插件可以用一个单一的函数完全地重写 `exports`，而不是添加函数作为 `exports` 的属性。

为了验证它，运行以下 JavaScript：

```js
// test.js
const addon = require('./build/Release/addon');

addon((msg) => {
  console.log(msg);
// 打印: 'hello world'
});
```

注意，在这个例子中，回调函数是被同步地调用。

