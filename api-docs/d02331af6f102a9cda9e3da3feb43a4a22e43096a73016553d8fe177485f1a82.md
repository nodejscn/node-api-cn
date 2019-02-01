<!-- YAML
added: v0.1.25
-->

* `str` {string}

`querystring.escape()` 方法以对 URL 查询字符串的特定要求进行了优化的方式对给定的 `str` 执行 URL 百分比编码。

`querystring.escape()` 方法由 `querystring.stringify()` 使用，通常不会直接使用。 
它的导出主要是为了允许应用程序代码在必要时通过将 `querystring.escape` 指定给替代函数来提供替换的百分比编码实现。

