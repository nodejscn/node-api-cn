<!-- YAML
added: v0.0.2
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
-->

* `path` {string|Buffer|URL}
* `callback` {Function}

异步的 stat(2)。
回调有两个参数 `(err, stats)` 其中 `stats` 是一个 [`fs.Stats`] 对象。

如果发生错误，则 `err.code` 会是[常见系统错误]之一。

不建议在调用 `fs.open()` 、`fs.readFile()` 或 `fs.writeFile()` 之前使用 `fs.stat()` 检查一个文件是否存在。
作为替代，用户代码应该直接打开/读取/写入文件，当文件无效时再处理错误。

如果要检查一个文件是否存在且不操作它，推荐使用 [`fs.access()`]。

