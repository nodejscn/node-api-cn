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
  * `bigint` {boolean} [`fs.Stats`] 对象返回的数值是否为长整数型。默认为 `false`。
* 返回: {fs.Stats}


同步的 fstat(2)。

