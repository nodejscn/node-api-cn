<!-- YAML
added: v0.1.25
-->
* `str` {string}

`querystring.unescape()` 方法在给定的 `str` 上执行 URL 百分比编码字符的解码。

`querystring.unescape()` 方法由 `querystring.parse()` 使用，通常不会被直接地使用。 
它的导出主要是为了允许应用程序代码在需要时通过将 `querystring.unescape` 赋值给替代函数来提供替换的解码实现。

默认情况下，`querystring.unescape()` 方法将会尝试使用 JavaScript 内置的 `decodeURIComponent()` 方法进行解码。 
如果失败，则将会使用更保险的不会因格式错误的 URL 而抛出异常的同类方法。

