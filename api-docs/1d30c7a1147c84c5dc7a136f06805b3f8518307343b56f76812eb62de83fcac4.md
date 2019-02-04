<!-- YAML
added: v8.3.0
-->

当 `stdout` 是 TTY 时，调用 `console.clear()` 将尝试清除 TTY。 
当 `stdout` 不是 TTY 时，此方法不执行任何操作。

`console.clear()` 的具体操作可能因操作系统和终端类型而异。 
对于大多数 Linux 操作系统，`console.clear()` 的操作与 `clear` 的 shell 命令类似。 
在 Windows 上，`console.clear()` 将仅清除当前终端视图中 Node.js 二进制文件的输出。

