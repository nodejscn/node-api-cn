
为了支持 [`Worker`] 线程，插件需要清理可能分配的任何资源（当存在这样的线程时）。 
这可以通过使用 `AddEnvironmentCleanupHook()` 函数来实现：

```c++
void AddEnvironmentCleanupHook(v8::Isolate* isolate,
                               void (*fun)(void* arg),
                               void* arg);
```

此函数添加了一个钩子，该钩子将在给定的 Node.js 实例关闭之前运行。 
如有必要，可以在运行之前使用 `RemoveEnvironmentCleanupHook()` 删除此类挂钩，它们具有相同的签名。

为了从多个 Node.js 环境加载，例如主线程和工作线程，插件还需要：
- 是一个 N-API 插件，或
- 如上所述，使用 `NODE_MODULE_INIT()` 声明为上下文感知。

