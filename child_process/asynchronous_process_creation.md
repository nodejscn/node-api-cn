
[`child_process.spawn()`]、[`child_process.fork()`]、[`child_process.exec()`] 和 [`child_process.execFile()`] 方法都遵循其他 Node.js API 惯用的异步编程模式。

每个方法都会返回 [`ChildProcess`] 实例。
这些对象实现了 Node.js 的 [`EventEmitter`] API，使得父进程可以注册监听器函数（当在子进程的生命周期中发生特定事件时会被调用）。

[`child_process.exec()`] 和 [`child_process.execFile()`] 方法还可以指定可选的 `callback` 函数（当子进程终止时会被调用）。


