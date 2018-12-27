<!-- YAML
added: v0.5.10
-->

* `message` { Object | boolean | number | string | null } 发送的消息。
* `sendHandle` {net.Server|net.Socket} 

如果 Node.js 进程是使用 IPC 通道衍生的（详见[子进程][Child Process]和[集群][Cluster]文档），则当子进程接收到父进程使用 [`childprocess.send()`] 发送的消息时触发。

消息会进行序列化和解析，收到的消息可能与发送的不完全一样。

