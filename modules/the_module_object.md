<!-- YAML
added: v0.1.16
-->

<!-- type=var -->
<!-- name=module -->

* {Object}

在每个模块中，`module` 自由变量是一个对表示当前模块的对象的引用。
为方便起见，`module.exports` 还可以通过 `exports` 模块全局地访问 。
`module` 实际上不是一个全局变量，而是每个模块本地的。

