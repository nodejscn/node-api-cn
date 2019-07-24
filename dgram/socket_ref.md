<!-- YAML
added: v0.9.1
-->

默认情况下，绑定一个 socket 会在 socket 运行时阻止 Node.js 进程退出。
`socket.unref()` 方法用于将 socket 从维持 Node.js 进程的引用列表中解除。
`socket.ref()` 方法用于将 socket 重新添加到这个引用列表中，并恢复其默认行为。

多次调用 `socket.ref()` 不会有额外的作用。

`socket.ref()` 方法返回一个对 socket 的引用，所以可以链式调用。

