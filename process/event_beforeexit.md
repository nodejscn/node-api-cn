<!-- YAML
added: v0.11.12
-->

* `exitCode` {integer} 进程的退出码，详见 [`process.exitCode`]。

当 Node.js 清空了事件循环且不再添加额外的工作时触发。
正常情况下，如果不再添加额外的工作，则 Node.js 进程会退出。
如果 `'beforeExit'` 事件注册的监听器中含有异步调用，则 Node.js 进程会继续运行。

如果进程被显式地终止，比如调用 [`process.exit()`] 或抛出未捕获的异常，则不会触发 `'beforeExit'` 事件。

除非需要添加额外的工作，否则不要使用 `'beforeExit'` 事件代替 `'exit'` 事件。
