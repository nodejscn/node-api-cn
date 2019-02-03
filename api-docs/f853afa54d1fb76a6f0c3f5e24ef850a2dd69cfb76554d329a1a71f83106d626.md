<!-- YAML
added: v0.5.10
-->

* `message` { Object | boolean | number | string | null } 已解析的 JSON 对象或可序列化的原始值。
* `sendHandle` {net.Server|net.Socket} 一个 [`net.Server`] 或 [`net.Socket`] 对象，或未定义。

如果使用 IPC 通道衍生 Node.js 进程（参阅[子进程][Child Process]和[集群][Cluster]文档），则只要子进程收到父进程使用 [`childprocess.send()`] 发送的消息，就会触发 `'message'` 事件。

消息会进行序列化和解析。 
生成的消息可能与最初发送的消息不同。


