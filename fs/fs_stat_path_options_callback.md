<!-- YAML
added: v0.0.2
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
  - version: v10.5.0
    pr-url: https://github.com/nodejs/node/pull/20220
    description: Accepts an additional `options` object to specify whether
                 the numeric values returned should be bigint.
-->

* `path` {string|Buffer|URL}
* `options` {Object}
  * `bigint` {boolean} 在返回的[`fs.Stats`][] 对象中的数字类型值是否为`bigint`. **Default:** `false`.
* `callback` {Function}
  * `err` {Error}
  * `stats` {fs.Stats}

异步的 stat(2). 回调函数中包含两个参数 `(err, stats)` ，其中
`stats` 为 [`fs.Stats`][] 对象。

如果发生了错误， `err.code` 将会为 [Common System Errors][]中的某个值。

不推荐在调用`fs.open()`, `fs.readFile()` or `fs.writeFile()` 前通过使用 `fs.stat()` 
来检查某个文件是否存在。对于这种情况，开发者应当通过直接open/read/write文件并检测产生的异常来
判断文件是否可用。

如果不需要操作文件只是想获取文件是否可用，推荐使用[`fs.access()`]。

