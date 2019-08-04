<!-- YAML
added: v0.9.1
-->

默认情况下，只要 socket 是打开的，绑定一个 socket 将导致它阻塞 Node.js 进程退出。
使用 `socket.unref()` 方法可以从保持 Node.js 进程活动的引用计数中排除 socket，从而允许进程退出，尽管这个 socket 仍然在侦听。

多次调用 `socket.unref()` 方法将不会有任何新增的作用。

`socket.unref()` 方法返回当前 socket 的引用，因此可以链式调用。
