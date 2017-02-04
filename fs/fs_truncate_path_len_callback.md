<!-- YAML
added: v0.8.6
-->

* `path` {String | Buffer}
* `len` {Integer} 默认 = `0`
* `callback` {Function}

异步的 truncate(2)。
完成回调只有一个可能的异常参数。
文件描述符也可以作为第一个参数传入，在这种情况下，`fs.ftruncate()` 会被调用。

