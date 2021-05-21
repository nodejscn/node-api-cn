<!-- YAML
added: v0.3.0
changes:
  - version: v8.9.0
    pr-url: https://github.com/nodejs/node/pull/16397
    description: 选项 `paths` 现在是被支持的。
-->

* `request` {string} 要解析的模块路径。
* `options` {Object}
  * `paths` {string[]} 从中解析模块位置的路径。 
    如果存在，则这些路径（而不是默认的解析路径）会被使用，但是 [GLOBAL_FOLDERS]（例如 `$HOME/.node_modules`）除外，它们始终被包含。 
    这些路径的每一个被用作模块解析算法的一个起点，这意味着 `node_modules` 层级被从此位置开始检查。
* 返回: {string}

使用内部的 `require()` 机制查找一个模块的位置，但是不会加载该模块，只是返回解析后的文件名。

如果该模块不能被找到，则一个 `MODULE_NOT_FOUND` 错误被抛出。

