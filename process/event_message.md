<!-- YAML
added: v0.5.10
-->

如果 Node.js 进程是由 IPC 通道的方式创建的（详见[子进程]和[集群]文档），当子进程收到父进程的的消息时（消息通过 [`childprocess.send()`] 发送），会触发 `'message'` 事件。

`'message'` 事件监听器的回调函数中被传递的参数如下：
* `message`{Object} 解析的 JSON 对象或原始值。
* `sendHandle` {Handle object} 一个 [`net.Socket`] 或 [`net.Server`] 对象，或 `undefined`。


