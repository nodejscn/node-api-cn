<!-- YAML
added: v0.1.21
-->

* `fd` {integer}

同步的 close(2)。返回 `undefined`。

通过任何其他 `fs` 操作在当前正在使用的任何文件描述符（`fd`）上调用 `fs.closeSync()` 可能导致未定义的行为。


