<!-- YAML
added: v0.0.2
-->

* `path` {String | Buffer}
* `callback` {Function}

异步的 stat(2)。
回调有两个参数 `(err, stats)` 其中 `stats` 是一个 [`fs.Stats`] 对象。

如果发生错误，则 `err.code` 会是[常见系统错误]之一。

不建议在调用 `fs.open()` 、`fs.readFile()` 或 `fs.writeFile()` 之前使用 `fs.stat()` 检查一个文件是否存在。
作为替代，用户代码应该直接打开/读取/写入文件，当文件无效时再处理错误。

如果要检查一个文件是否存在且不操作它，推荐使用 [`fs.access()`]。

