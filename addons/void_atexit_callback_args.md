
* `callback`: `void (*)(void*)` - 一个退出时调用的函数的指针。
* `args`: `void*` - 一个退出时传递给回调的指针。

注册的 AtExit 钩子会在事件循环结束之后但虚拟机被终止之前退出。

AtExit 有两个参数：一个退出时运行的回调函数的指针，和一个要传入回调的无类型的上下文数据的指针。

回调按照后进先出的顺序运行。

以下 `addon.cc` 实现了 AtExit：

```cpp
// addon.cc
#include <assert.h>
#include <stdlib.h>
#include <node.h>

namespace demo {

using node::AtExit;
using v8::HandleScope;
using v8::Isolate;
using v8::Local;
using v8::Object;

static char cookie[] = "yum yum";
static int at_exit_cb1_called = 0;
static int at_exit_cb2_called = 0;

static void at_exit_cb1(void* arg) {
  Isolate* isolate = static_cast<Isolate*>(arg);
  HandleScope scope(isolate);
  Local<Object> obj = Object::New(isolate);
  assert(!obj.IsEmpty()); // assert VM is still alive
  assert(obj->IsObject());
  at_exit_cb1_called++;
}

static void at_exit_cb2(void* arg) {
  assert(arg == static_cast<void*>(cookie));
  at_exit_cb2_called++;
}

static void sanity_check(void*) {
  assert(at_exit_cb1_called == 1);
  assert(at_exit_cb2_called == 2);
}

void init(Local<Object> exports) {
  AtExit(at_exit_cb2, cookie);
  AtExit(at_exit_cb2, cookie);
  AtExit(at_exit_cb1, exports->GetIsolate());
  AtExit(sanity_check);
}

NODE_MODULE(addon, init)

}  // namespace demo
```

测试：

```js
// test.js
require('./build/Release/addon');
```

