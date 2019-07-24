<!-- YAML
added: v0.5.8
-->

`tty.ReadStream` 类是 [`net.Socket`] 的子类，表示 TTY 的可读端。 
在正常情况下，[`process.stdin`] 将是 Node.js 进程中唯一的 `tty.ReadStream` 实例，并且没有理由创建其他实例。

