<!-- YAML
added: v0.1.95
changes:
  - version: v10.5.0
    pr-url: https://github.com/nodejs/node/pull/20220
    description: Accepts an additional `options` object to specify whether
                 the numeric values returned should be bigint.
-->

* `fd` {integer}
* `options` {Object}
  * `bigint` {boolean} 返回的 [`fs.Stats`] 对象中的数值是否应为 `bigint` 型。**默认值:** `false`。
* 返回: {fs.Stats}


同步的 fstat(2)。

