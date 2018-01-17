<!-- YAML
added: v0.7.7
-->

如果 Node.js 进程是由 IPC 通道的方式创建的（详见[子进程]和[集群]文档），当 IPC 通道关闭时，会触发`'disconnect'`事件。
