<!-- YAML
added: v0.5.8
-->

* `fd` {number} 数字型的文件描述符。
* 返回: {boolean}

如果给定的 `fd` 与 TTY 相关联，则 `tty.isatty()` 方法返回 `true`，否则返回 `false`（包括当 `fd` 不是一个非负整数时）。

