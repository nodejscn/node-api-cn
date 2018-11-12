<!-- YAML
added: v0.8.6
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
-->

* `path` {string|Buffer|URL}
* `len` {integer} 默认为 `0`。
* `callback` {Function}
  * `err` {Error}

异步的 truncate(2)。
完成回调只有一个可能的异常参数。

第一个参数也可以是一个文件描述符，在这种情况下，`fs.ftruncate()` 会被调用。
但这种用法已被废弃，不建议使用。

