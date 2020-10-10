<!-- YAML
added: v10.0.0
changes:
  - version: v10.5.0
    pr-url: https://github.com/nodejs/node/pull/20220
    description: 接受额外的 `options` 对象，用于指定返回的数值是否为 bigint。
-->

* `path` {string|Buffer|URL}
* `options` {Object}
  * `bigint` {boolean} 返回的 [`fs.Stats`] 对象中的数值是否应为 `bigint` 型。**默认值:** `false`。
* 返回: {Promise}

`Promise` 会被解决并带上 [`fs.Stats`] 对象（用于给定的 `path`）。

