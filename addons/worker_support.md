<!-- YAML
changes:
  - version: v14.8.0
    pr-url: https://github.com/nodejs/node/pull/34572
    description: Cleanup hooks may now be asynchronous.
-->

为了从多个 Node.js 环境加载，例如主线程和工作线程，插件还需要：

* 是一个 N-API 插件，或
* 如上所述，使用 `NODE_MODULE_INIT()` 声明为上下文感知。

为了支持 [`Worker`] 线程，插件需要清理可能分配的任何资源（当存在这样的线程时）。 
这可以通过使用 `AddEnvironmentCleanupHook()` 函数来实现：

```cpp
void AddEnvironmentCleanupHook(v8::Isolate* isolate,
                               void (*fun)(void* arg),
                               void* arg);
```

此函数添加了一个钩子，该钩子将在给定的 Node.js 实例关闭之前运行。 
如有必要，可以在运行之前使用 `RemoveEnvironmentCleanupHook()` 删除此类挂钩，它们具有相同的签名。
回调以后进先出的顺序运行。

If necessary, there is an additional pair of `AddEnvironmentCleanupHook()`
and `RemoveEnvironmentCleanupHook()` overloads, where the cleanup hook takes a
callback function. This can be used for shutting down asynchronous resources,
such as any libuv handles registered by the addon.

以下的 `addon.cc` 使用 `AddEnvironmentCleanupHook`：

```cpp
// addon.cc
#include <assert.h>
#include <stdlib.h>
#include <node.h>

using node::AddEnvironmentCleanupHook;
using v8::HandleScope;
using v8::Isolate;
using v8::Local;
using v8::Object;

// 注意：在实际的应用程序中，请勿依赖静态/全局的数据。
static char cookie[] = "yum yum";
static int cleanup_cb1_called = 0;
static int cleanup_cb2_called = 0;

static void cleanup_cb1(void* arg) {
  Isolate* isolate = static_cast<Isolate*>(arg);
  HandleScope scope(isolate);
  Local<Object> obj = Object::New(isolate);
  assert(!obj.IsEmpty());  // 断言 VM 仍然存在。
  assert(obj->IsObject());
  cleanup_cb1_called++;
}

static void cleanup_cb2(void* arg) {
  assert(arg == static_cast<void*>(cookie));
  cleanup_cb2_called++;
}

static void sanity_check(void*) {
  assert(cleanup_cb1_called == 1);
  assert(cleanup_cb2_called == 1);
}

// 将此插件初始化为上下文感知的。
NODE_MODULE_INIT(/* exports, module, context */) {
  Isolate* isolate = context->GetIsolate();

  AddEnvironmentCleanupHook(isolate, sanity_check, nullptr);
  AddEnvironmentCleanupHook(isolate, cleanup_cb2, cookie);
  AddEnvironmentCleanupHook(isolate, cleanup_cb1, isolate);
}
```

通过运行以下命令在 JavaScript 中进行测试：

```js
// test.js
require('./build/Release/addon');
```



