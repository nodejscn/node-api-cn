
There are environments in which Node.js addons may need to be loaded multiple
times in multiple contexts. For example, the [Electron][] runtime runs multiple
instances of Node.js in a single process. Each instance will have its own
`require()` cache, and thus each instance will need a native addon to behave
correctly when loaded via `require()`. From the addon's perspective, this means
that it must support multiple initializations.

A context-aware addon can be constructed by using the macro
`NODE_MODULE_INITIALIZER`, which expands to the name of a function which Node.js
will expect to find when it loads an addon. An addon can thus be initialized as
in the following example:

```cpp
using namespace v8;

extern "C" NODE_MODULE_EXPORT void
NODE_MODULE_INITIALIZER(Local<Object> exports,
                        Local<Value> module,
                        Local<Context> context) {
  /* Perform addon initialization steps here. */
}
```

Another option is to use the macro `NODE_MODULE_INIT()`, which will also
construct a context-aware addon. Unlike `NODE_MODULE()`, which is used to
construct an addon around a given addon initializer function,
`NODE_MODULE_INIT()` serves as the declaration of such an initializer to be
followed by a function body.

The following three variables may be used inside the function body following an
invocation of `NODE_MODULE_INIT()`:
* `Local<Object> exports`,
* `Local<Value> module`, and
* `Local<Context> context`

The choice to build a context-aware addon carries with it the responsibility of
carefully managing global static data. Since the addon may be loaded multiple
times, potentially even from different threads, any global static data stored
in the addon must be properly protected, and must not contain any persistent
references to JavaScript objects. The reason for this is that JavaScript
objects are only valid in one context, and will likely cause a crash when
accessed from the wrong context or from a different thread than the one on which
they were created.

The context-aware addon can be structured to avoid global static data by
performing the following steps:
* defining a class which will hold per-addon-instance data. Such
a class should include a `v8::Persistent<v8::Object>` which will hold a weak
reference to the addon's `exports` object. The callback associated with the weak
reference will then destroy the instance of the class.
* constructing an instance of this class in the addon initializer such that the
`v8::Persistent<v8::Object>` is set to the `exports` object.
* storing the instance of the class in a `v8::External`, and
* passing the `v8::External` to all methods exposed to JavaScript by passing it
to the `v8::FunctionTemplate` constructor which creates the native-backed
JavaScript functions. The `v8::FunctionTemplate` constructor's third parameter
accepts the `v8::External`.

This will ensure that the per-addon-instance data reaches each binding that can
be called from JavaScript. The per-addon-instance data must also be passed into
any asynchronous callbacks the addon may create.

The following example illustrates the implementation of a context-aware addon:

```cpp
#include <node.h>

using namespace v8;

class AddonData {
 public:
  AddonData(Isolate* isolate, Local<Object> exports):
      call_count(0) {
    // Link the existence of this object instance to the existence of exports.
    exports_.Reset(isolate, exports);
    exports_.SetWeak(this, DeleteMe, WeakCallbackType::kParameter);
  }

  ~AddonData() {
    if (!exports_.IsEmpty()) {
      // Reset the reference to avoid leaking data.
      exports_.ClearWeak();
      exports_.Reset();
    }
  }

  // Per-addon data.
  int call_count;

 private:
  // Method to call when "exports" is about to be garbage-collected.
  static void DeleteMe(const WeakCallbackInfo<AddonData>& info) {
    delete info.GetParameter();
  }

  // Weak handle to the "exports" object. An instance of this class will be
  // destroyed along with the exports object to which it is weakly bound.
  v8::Persistent<v8::Object> exports_;
};

static void Method(const v8::FunctionCallbackInfo<v8::Value>& info) {
  // Retrieve the per-addon-instance data.
  AddonData* data =
      reinterpret_cast<AddonData*>(info.Data().As<External>()->Value());
  data->call_count++;
  info.GetReturnValue().Set((double)data->call_count);
}

// Initialize this addon to be context-aware.
NODE_MODULE_INIT(/* exports, module, context */) {
  Isolate* isolate = context->GetIsolate();

  // Create a new instance of AddonData for this instance of the addon.
  AddonData* data = new AddonData(isolate, exports);
  // Wrap the data in a v8::External so we can pass it to the method we expose.
  Local<External> external = External::New(isolate, data);

  // Expose the method "Method" to JavaScript, and make sure it receives the
  // per-addon-instance data we created above by passing `external` as the
  // third parameter to the FunctionTemplate constructor.
  exports->Set(context,
               String::NewFromUtf8(isolate, "method", NewStringType::kNormal)
                  .ToLocalChecked(),
               FunctionTemplate::New(isolate, Method, external)
                  ->GetFunction(context).ToLocalChecked()).FromJust();
}
```

