<!-- YAML
added: v0.5.1
-->

* `id` {string}
* 返回: {Object} 已解析的模块的 `module.exports`

`module.require` 方法提供了一种类似 `require()` 从原始模块被调用的加载模块的方式。

注意，为了做到这个，需要获得一个 `module` 对象的引用。
因为 `require()` 会返回 `module.exports`，且 `module` **只**在一个特定的模块代码中有效，所以为了使用它，必须明确地导出。

