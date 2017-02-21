<!-- YAML
added: v0.1.25
-->
* `str` {String}

`querystring.unescape()` 方法对给定的 `str` 上的 URL 百分号编码的字符执行解码。

`querystring.unescape()` 方法是供 `querystring.parse()` 使用的，且通常不被直接使用。
它之所以对外开放，是为了在需要时可以通过给 `querystring.unescape` 赋值一个函数来重写解码的实现。

`querystring.unescape()` 方法默认使用 JavaScript 内置的 `decodeURIComponent()` 方法来解码。

