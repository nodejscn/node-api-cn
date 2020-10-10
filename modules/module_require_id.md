<!-- YAML
added: v0.5.1
-->

* `id` {string}
* 返回: {any} 导出的模块内容。


`module.require()` 方法提供了一种加载模块的方法，就像从原始模块调用 `require()` 一样。

为了做到这个，需要获得一个 `module` 对象的引用。
因为 `require()` 会返回 `module.exports`，且 `module` 通常只在一个特定的模块代码中有效，所以为了使用它，必须显式地导出。

