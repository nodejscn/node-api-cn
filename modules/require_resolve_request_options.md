<!-- YAML
added: v0.3.0
changes:
  - version: v8.9.0
    pr-url: https://github.com/nodejs/node/pull/16397
    description: The `paths` option is now supported.
-->

* `request` {string} 需要解析的模块路径。
* `options` {Object}
  * `paths` {string[]} 从中解析模块位置的路径。 
    如果存在，则使用这些路径而不是默认的解析路径，但 [GLOBAL_FOLDERS] 除外，例如 `$HOME/.node_modules`，它们总是包含在内。 
    这些路径中的每一个都用作模块解析算法的起点，这意味着从该位置开始检查 `node_modules` 层次结构。
* 返回: {string}

使用内部的 `require()` 机制查询模块的位置，此操作只返回解析后的文件名，不会加载该模块。

