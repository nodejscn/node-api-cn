<!-- YAML
added: v7.1.0
-->

如果Node.js进程是由IPC channel(see the [Child Process][] documentation) 方式创建的，`process.channel`属性保存IPC channel的引用。
如果IPC channel不存在，此属性值为`undefined。
