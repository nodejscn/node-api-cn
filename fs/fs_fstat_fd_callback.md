<!-- YAML
added: v0.1.95
-->

* `fd` {Integer}
* `callback` {Function}

异步的 fstat(2)。
回调获得两个参数 `(err, stats)`，其中 `stats` 是一个 [`fs.Stats`] 对象。
`fstat()` 与 [`stat()`] 类似，除了文件是通过文件描述符 `fd` 指定的。

