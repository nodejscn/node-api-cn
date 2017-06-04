<!-- YAML
added: v0.1.95
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
-->

* `fd` {integer}
* `callback` {Function}

异步的 fstat(2)。
回调获得两个参数 `(err, stats)`，其中 `stats` 是一个 [`fs.Stats`] 对象。
`fstat()` 与 [`stat()`] 类似，除了文件是通过文件描述符 `fd` 指定的。

