
* `callback`: `void (*)(void*)` - A pointer to the function to call at exit.
* `args`: `void*` - A pointer to pass to the callback at exit.

Registers exit hooks that run after the event loop has ended but before the VM
is killed.

AtExit takes two parameters: a pointer to a callback function to run at exit,
and a pointer to untyped context data to be passed to that callback.

Callbacks are run in last-in first-out order.

The following `addon.cc` implements AtExit:

```cpp
// addon.cc
#undef NDEBUG
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
  AtExit(sanity_check);
  AtExit(at_exit_cb2, cookie);
  AtExit(at_exit_cb2, cookie);
  AtExit(at_exit_cb1, exports->GetIsolate());
}

NODE_MODULE(addon, init);

}  // namespace demo
```

Test in JavaScript by running:

```js
// test.js
const addon = require('./build/Release/addon');
```

[bindings]: https://github.com/TooTallNate/node-bindings
[download]: https://github.com/nodejs/node-addon-examples
[Embedder's Guide]: https://developers.google.com/v8/embed
[examples]: https://github.com/nodejs/nan/tree/master/examples/
[installation instructions]: https://github.com/nodejs/node-gyp#installation
[libuv]: https://github.com/libuv/libuv
[Linking to Node.js' own dependencies]: #addons_linking_to_node_js_own_dependencies
[Native Abstractions for Node.js]: https://github.com/nodejs/nan
[node-gyp]: https://github.com/nodejs/node-gyp
[require]: globals.html#globals_require
[v8-docs]: https://v8docs.nodesource.com/
