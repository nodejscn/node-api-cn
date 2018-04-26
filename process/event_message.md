<!-- YAML
added: v0.5.10
-->

如果 Node.js 进程是由 IPC 通道的方式创建的（详见[子进程]和[集群]文档），当子进程收到父进程发送的消息时(消息通过 [`childprocess.send()`] 发送），会触发 `'message'` 事件。

通过下列参数触发回调：
* `message`{Object} 解析的 JSON 对象或原始值。
* `sendHandle` {Handle object} 一个 [`net.Socket`] 或 [`net.Server`] 对象，或 `undefined`。

*注意*: 这个消息经过序列化和解析，可能与原初发送的消息不完全一样。
