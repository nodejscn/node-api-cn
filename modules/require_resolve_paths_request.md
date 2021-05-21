<!-- YAML
added: v8.9.0
-->

* `request` {string} 正在被获取其查找路径的模块路径。
* 返回: {string[]|null}

返回一个包含 `request` 解析期间被搜索的路径的数组，或者如果 `request` 字符串指向一个核心模块（例如 `http` 或者 `fs`）则返回 `null`。

