<!-- YAML
added: v0.1.16
-->

<!-- type=var -->
<!-- name=module -->

* {Object}

在每个模块中，`module` 的自由变量是一个指向表示当前模块的对象的引用。
为了方便，`module.exports` 也可以通过全局模块的 `exports` 对象访问。
`module` 实际上不是全局的，而是每个模块本地的。

