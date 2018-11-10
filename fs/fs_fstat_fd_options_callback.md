<!-- YAML
added: v0.1.95
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
  - version: v10.5.0
    pr-url: https://github.com/nodejs/node/pull/20220
    description: Accepts an additional `options` object to specify whether
                 the numeric values returned should be bigint.
-->

* `fd` {integer}
* `options` {Object}
  * `bigint` {boolean} [`fs.Stats`] 对象返回的数值是否为长整数型。默认为 `false`。
* `callback` {Function}
  * `err` {Error}
  * `stats` {fs.Stats}


异步的 fstat(2)。
回调有两个参数 `(err, stats)`，其中 `stats` 是一个 [`fs.Stats`] 对象。
`fstat()` 与 [`stat()`] 区别是，文件是通过文件描述符 `fd` 指定的。

