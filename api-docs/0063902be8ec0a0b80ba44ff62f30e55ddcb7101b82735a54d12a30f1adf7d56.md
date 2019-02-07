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
  * `bigint` {boolean} 返回的 [`fs.Stats`] 对象中的数值是否应为 `bigint` 型。**默认值:** `false`。
* `callback` {Function}
  * `err` {Error}
  * `stats` {fs.Stats}


异步的 fstat(2)。
回调会传入两个参数 `(err, stats)`，其中 `stats` 是 [`fs.Stats`] 对象。
`fstat()` 与 [`stat()`] 相同，除了文件是由文件描述符 `fd` 指定。

