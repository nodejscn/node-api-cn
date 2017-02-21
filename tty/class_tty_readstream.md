<!-- YAML
added: v0.5.8
-->

`tty.ReadStream` 类是 `net.Socket` 的一个子类，表示一个 TTY 的可读部分。
正常情况下，`process.stdin` 是一个 Node.js 进程中唯一的 `tty.ReadStream` 实例，没有理由创建更多的实例。

