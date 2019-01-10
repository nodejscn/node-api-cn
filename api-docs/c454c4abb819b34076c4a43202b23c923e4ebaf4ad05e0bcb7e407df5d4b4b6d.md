<!-- YAML
added: v0.1.27
-->

<!-- type=global -->

* {Object} 全局的命名空间对象。

在浏览器中，顶层作用域是全局作用域。 
这意味着在浏览器中 `var something` 将定义一个新的全局变量。 
在 Node.js 中，这是不同的。 
顶层作用域不是全局作用域，Node.js 模块中的 `var something` 的作用域只在该模块内。


