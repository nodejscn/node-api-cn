
[`child_process.spawn()`]、[`child_process.fork()`]、[`child_process.exec()`] 和 [`child_process.execFile()`] 函数都遵循 Node.js API 惯用的异步编程模式。

每个函数都返回 [`ChildProcess`] 实例。
这些实例实现了 Node.js [`EventEmitter`] API，允许父进程注册监听器函数，在子进程生命周期期间，当特定的事件发生时会调用这些函数。

[`child_process.exec()`] 和 [`child_process.execFile()`] 函数可以额外指定一个可选的 `callback` 函数，当子进程结束时会被调用。

