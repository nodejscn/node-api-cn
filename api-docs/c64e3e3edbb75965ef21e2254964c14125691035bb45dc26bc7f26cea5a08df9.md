<!-- YAML
added: v0.1.25
-->
* `str` {string}

`querystring.unescape()` 方法在给定的 `str` 上执行 URL 百分比编码字符的解码。

`querystring.unescape()` 方法由 `querystring.parse()` 使用，通常不会直接使用它。 
它的导出主要是为了允许应用程序代码在必要时通过将 `querystring.unescape` 分配给替代函数来提供替换的解码实现。

默认情况下，`querystring.unescape()` 方法将尝试使用 JavaScript 内置的 `decodeURIComponent()` 方法进行解码。 
如果失败，将使用更安全的不会丢失格式错误的 URL 的等价方法。

