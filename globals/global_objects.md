
<!--introduced_in=v0.10.0-->
<!-- type=misc -->

全局变量在所有模块中都可使用。
以下变量虽然看起来像全局变量，但实际上不是。
它们的作用域只在模块内，详见 [module文档][module system documentation]：

- [`__dirname`]
- [`__filename`]
- [`exports`]
- [`module`]
- [`require()`]

下面列出的对象都是针对 Node.js 的。
有些[内置对象][built-in objects]是 JavaScript 语言本身的一部分，它们也是全局的。

