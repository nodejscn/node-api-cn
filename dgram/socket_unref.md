<!-- YAML
added: v0.9.1
-->

默认情况下，只要socket是打开的，绑定一个socket将导致它阻塞Node.js进程退出。使用`socket.unref()`方法可以从保持Node.js进程活动的引用计数中排除socket，从而允许进程退出，尽管这个socket仍然在侦听。

多次调用`socket.unref()`方法将不会有任何新增的作用。

`socket.unref()`方法返回当前socket的引用，因此可以链式调用。
