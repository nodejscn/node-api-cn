
This "Hello world" example is a simple Addon, written in C++, that is the
equivalent of the following JavaScript code:

```js
module.exports.hello = () => 'world';
```

First, create the file `hello.cc`:

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

Note that all Node.js Addons must export an initialization function following
the pattern:

```cpp
void Initialize(Local<Object> exports);
NODE_MODULE(module_name, Initialize)
```

There is no semi-colon after `NODE_MODULE` as it's not a function (see
`node.h`).

The `module_name` must match the filename of the final binary (excluding
the .node suffix).

In the `hello.cc` example, then, the initialization function is `init` and the
Addon module name is `addon`.

