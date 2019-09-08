<!-- YAML
added: v0.5.8
-->

* 继承自: {net.Socket}

代表 TTY 的可读端。 
在正常情况中，[`process.stdin`] 将会是 Node.js 进程中唯一的 `tty.ReadStream` 实例，并且没有理由创建其他的实例。

