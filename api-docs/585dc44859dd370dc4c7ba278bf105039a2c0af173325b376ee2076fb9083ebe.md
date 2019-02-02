<!-- YAML
added: v0.5.8
-->

`tty.WriteStream` 类是 [`net.Socket`] 的子类，表示 TTY 的可写端。 
在正常情况下，[`process.stdout`] 和 [`process.stderr`] 将是为 Node.js 进程创建的唯一 `tty.WriteStream` 实例，并且没有理由创建其他实例。

