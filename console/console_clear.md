<!-- YAML
added: v8.3.0
-->

当 `stdout` 是一个 TTY 时，调用 `console.clear()` 将尝试清除 TTY。 当 `stdout` 不是一个TTY时，该方法什么都不做。

*注意*：`console.clear()` 的具体行为可能因操作系统和终端类型而异。 对于大多数Linux操作系统，`console.clear()` 与 `clear` shell 命令行为类似。 在Windows上，`console.clear()` 将只清除当前终端视图中Node.js二进制文件的输出。
