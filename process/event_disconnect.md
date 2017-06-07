<!-- YAML
added: v0.7.7
-->

如果Node.js进程是由IPC channel的方式创建的(see the [Child Process][]
and [Cluster][] documentation)，当IPC channel关闭时，会触发`'disconnect'`事件。
