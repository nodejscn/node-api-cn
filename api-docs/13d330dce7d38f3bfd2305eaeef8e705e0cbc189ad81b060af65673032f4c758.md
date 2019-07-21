<!-- YAML
added: v10.0.0
changes:
  - version: v10.5.0
    pr-url: https://github.com/nodejs/node/pull/20220
    description: Accepts an additional `options` object to specify whether
                 the numeric values returned should be bigint.
-->

* `path` {string|Buffer|URL}
* `options` {Object}
  * `bigint` {boolean} 返回的 [`fs.Stats`] 对象中的数值是否应为 `bigint` 型。**默认值:** `false`。
* 返回: {Promise}

异步的 lstat(2)。
`Promise` 会被解决并带上用于给定的符号链接 `path` 的 [`fs.Stats`] 对象。

