<!-- YAML
added: v0.7.2
-->

关闭父进程与子进程之间的 IPC 通道，一旦没有其他的连接使其保持活跃，则允许子进程正常退出。
调用该方法后，则父进程和子进程上各自的 `subprocess.connected` 和 `process.connected` 属性都会被设为 `false`，且进程之间不能再传递消息。

当进程中没有正被接收的消息时，就会触发 `'disconnect'` 事件。
这经常在调用 `subprocess.disconnect()` 后被立即触发。

当子进程是一个 Node.js 实例时（例如使用 [`child_process.fork()`] 衍生），也可以在子进程中调用 `process.disconnect()` 方法来关闭 IPC 通道。

