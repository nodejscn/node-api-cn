<!-- YAML
added: v0.5.8
-->

* 继承自: {net.Socket}

代表 TTY 的可写端。 
在正常情况中，[`process.stdout`] 和 [`process.stderr`] 将会是为 Node.js 进程创建的唯一的 `tty.WriteStream` 实例，并且没有理由创建其他的实例。

