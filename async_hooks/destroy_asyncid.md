
* `asyncId` {number}

对应`asyncId`的资源销毁后调用。也可以从内嵌API`emitDestroy()`异步地调用。

*请注意:* 因为一些资源依赖于GC进行清理，所以如果一个`resource`对象的参照传递给了`init`，那么`destroy`就有可能不被调用，这样会导致应用程序内存泄漏。 如果资源不依赖于GC，那么这当然不是一个问题。
