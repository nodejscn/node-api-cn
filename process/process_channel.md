<!-- YAML
added: v7.1.0
-->

* {Object}

如果 Node.js 进程是由 IPC 通道（参阅[子进程][Child Process]文档）方式创建的，`process.channel` 属性保存 IPC 通道的引用。
如果 IPC 通道不存在，则此属性值为 `undefined`。
