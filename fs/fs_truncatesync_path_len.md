<!-- YAML
added: v0.8.6
-->

* `path` {string|Buffer|URL}
* `len` {integer} 默认为 `0`。

同步的 truncate(2)。
返回 `undefined`。

第一个参数也可以是一个文件描述符，在这种情况下，`fs.ftruncate()` 会被调用。
但这种用法已被废弃，不建议使用。

