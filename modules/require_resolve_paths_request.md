<!-- YAML
added: v8.9.0
-->

* `request` {string} 被查询解析路径的模块的路径。
* 返回: {Array|null}

返回一个数组，其中包含解析 `request` 过程中被查询的路径。
如果 `request` 字符串指向核心模块（例如 `http` 或 `fs`），则返回 `null`。
