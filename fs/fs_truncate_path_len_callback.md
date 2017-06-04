<!-- YAML
added: v0.8.6
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
-->

* `path` {string|Buffer}
* `len` {integer} 默认 = `0`
* `callback` {Function}

异步的 truncate(2)。
完成回调只有一个可能的异常参数。
文件描述符也可以作为第一个参数传入，在这种情况下，`fs.ftruncate()` 会被调用。

