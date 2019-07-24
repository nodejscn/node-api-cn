<!-- YAML
added: v0.11.12
-->

当 Node.js 清空其事件循环并且没有其他工作要安排时，会触发 `'beforeExit'` 事件。 
通常，Node.js 进程将在没有调度工作时退出，但是在 `'beforeExit'` 事件上注册的监听器可以进行异步调用，从而导致 Node.js 进程继续。

调用监听器回调函数时会将 [`process.exitCode`] 的值作为唯一参数传入。

对于导致显式终止的条件，不会触发 `'beforeExit'` 事件，例如调用 [`process.exit()`] 或未捕获的异常。

除非打算安排额外的工作，否则不应将 `'beforeExit'` 用作 `'exit'` 事件的替代方案。

