<!-- YAML
added: v0.7.2
-->

关闭父进程与子进程之间的 IPC 通道，一旦没有其他的连接使其保持活跃，则允许子进程正常退出。
调用该方法后，父进程和子进程上各自的 `subprocess.connected` 和 `subprocess.connected` 属性都会被设为 `false`，且进程之间不能再传递消息。

当正在接收的进程中没有消息时，就会触发 `'disconnect'` 事件。
这经常在调用 `subprocess.disconnect()` 后立即被触发。

注意，当子进程是一个 Node.js 实例时（例如通过 [`child_process.fork()`] 衍生的），可以在子进程内调用 `process.disconnect()` 方法来关闭 IPC 通道。

<a name="child_process_child_kill_signal"></a>
