
Node.js 插件可能需要在多个上下文中多次加载的环境。
比如，[Electron] 的运行时会在单个进程中运行多个 Node.js 实例。
每个实例都有它自己的 `require()` 缓存，因此当通过 `require()` 进行加载时，每个实例需要一个原生的插件才能正常运行。
从插件程序的角度来看，这意味着它必须支持多次初始化。

可以使用 `NODE_MODULE_INITIALIZER` 宏来构建上下文感知的插件，它扩展为 Node.js 函数的名字使得 Node.js 能在加载时找到。
可以按如下例子初始化一个插件：

```cpp
using namespace v8;

extern "C" NODE_MODULE_EXPORT void
NODE_MODULE_INITIALIZER(Local<Object> exports,
                        Local<Value> module,
                        Local<Context> context) {
  /* Perform addon initialization steps here. */
}
```

另一个选择是使用 `NODE_MODULE_INIT()` 宏，这也可以用来构建上下文感知的插件。
但和 `NODE_MODULE()` 不一样的是，它可以基于一个给定的函数来构建一个插件，`NODE_MODULE_INIT()` 充当了这种跟有函数体的给定函数的声明。

可以在调用 `NODE_MODULE_INIT()` 之后在函数体内部使用以下三个变量：
* `Local<Object> exports`
* `Local<Value> module`
* `Local<Context> context`

这种构建上下文感知的插件的方式顺带了管理全局静态数据的职责。
由于插件可能被多次加载，可能甚至来自不同的线程，插件中任何的全局静态数据必须加以保护，并且不能包含任何对 JavaScript 对象持久性的引用。
因为 JavaScript 对象只在一个上下文中有效，从错误的上下文或者另外的线程中访问有可能会导致崩溃。

可以通过执行以下步骤来构造上下文感知的插件以避免全局静态数据：

* 定义一个类，该类会保存每个插件实例的数据，并且具有以下形式的静态成员：
    ```cpp
    static void DeleteInstance(void* data) {
      // 将 `data` 转换为该类的实例并删除它。
    }
    ```
* 在插件的初始化过程中堆分配此类的实例。
  这可以使用 `new` 关键字来完成。
* 调用 `node::AddEnvironmentCleanupHook()`，将上面创建的实例和指向 `DeleteInstance()` 的指针传给它。 
  这可以确保实例会在销毁环境之后被删除。
* 将类的实例保存在 `v8::External`中。
* 通过将 `v8::External` 传给 `v8::FunctionTemplate::New()` 或 `v8::Function::New()`（用以创建原生支持的 JavaScript 函数）来将其传给暴露给 JavaScript 的所有方法。 
  `v8::FunctionTemplate::New()` 或 `v8::Function::New()` 的第三个参数接受 `v8::External`，并使用 `v8::FunctionCallbackInfo::Data()` 方法使其在原生回调中可用。

这确保了每个扩展实例数据到达每个能被 JavaScript 访问的绑定。每个扩展实例数据也必须通过其创建的任何异步回调函数。

下面的例子说明了一个上下文感知的插件的实现：

```cpp
#include <node.h>

using namespace v8;

class AddonData {
 public:
  explicit AddonData(Isolate* isolate):
      call_count(0) {
    // 确保在清理环境时删除每个插件实例的数据。
    node::AddEnvironmentCleanupHook(isolate, DeleteInstance, this);
  }

  // 每个插件的数据。
  int call_count;

  static void DeleteInstance(void* data) {
    delete static_cast<AddonData*>(data);
  }
};

static void Method(const v8::FunctionCallbackInfo<v8::Value>& info) {
  // 恢复每个插件实例的数据。
  AddonData* data =
      reinterpret_cast<AddonData*>(info.Data().As<External>()->Value());
  data->call_count++;
  info.GetReturnValue().Set((double)data->call_count);
}

// context-aware 初始化
NODE_MODULE_INIT(/* exports, module, context */) {
  Isolate* isolate = context->GetIsolate();

  // 为此插件实例创建一个新的 `AddonData` 实例，并将其生命周期与 Node.js 环境的生命周期联系起来。
  AddonData* data = new AddonData(isolate, exports);
  // 在 `v8::External` 中包裹数据，这样我们就可以将它传递给我们暴露的方法。
  Local<External> external = External::New(isolate, data);

  // 把 `Method` 方法暴露给 JavaScript，
  // 并确保其接收我们通过把 `external` 作为 `FunctionTemplate` 构造函数第三个参数时创建的每个插件实例的数据。
  exports->Set(context,
               String::NewFromUtf8(isolate, "method", NewStringType::kNormal)
                  .ToLocalChecked(),
               FunctionTemplate::New(isolate, Method, external)
                  ->GetFunction(context).ToLocalChecked()).FromJust();
}
```

