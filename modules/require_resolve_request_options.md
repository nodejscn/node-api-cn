<!-- YAML
added: v0.3.0
changes:
  - version: v8.9.0
    pr-url: https://github.com/nodejs/node/pull/16397
    description: The `paths` option is now supported.
-->

* `request` {string} 需要解析的模块路径。
* `options` {Object}
  * `paths` {Array} 解析模块的起点路径。此参数存在时，将使用这些路径而非默认解析路径。
    注意此数组中的每一个路径都被用作模块解析算法的起点，意味着 `node_modules` 层级将从这里开始查询。
* Returns: {string}

使用内部的 `require()` 机制查询模块的位置,
此操作只返回解析后的文件名，不会加载该模块。

