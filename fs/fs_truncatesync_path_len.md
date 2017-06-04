<!-- YAML
added: v0.8.6
-->

* `path` {string|Buffer}
* `len` {integer} 默认 = `0`

同步的 truncate(2)。
返回 `undefined`。
文件描述符也可以作为第一个参数传入，在这种情况下，`fs.ftruncateSync()` 会被调用。

