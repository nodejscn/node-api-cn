<!-- YAML
added: v0.1.30
-->

* `path` {String | Buffer}
* `callback` {Function}

异步的 lstat(2)。
回调获得两个参数 `(err, stats)`，其中 `stats` 是一个 [`fs.Stats`] 对象。
`lstat()` 与 [`stat()`] 类似，除非 `path` 是一个符号链接，则自身就是该链接，它指向的并不是文件。

