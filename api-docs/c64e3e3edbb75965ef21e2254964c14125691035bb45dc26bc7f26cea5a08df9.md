<!-- YAML
added: v0.1.25
-->
* `str` {string}

对给定的 `str` 进行解码。

该方法是提供给 `querystring.parse()` 使用的，通常不直接使用。
它之所以对外开放，是为了在需要时可以通过给 `querystring.unescape` 赋值一个函数来重写解码的实现。

默认使用 JavaScript 内置的 `decodeURIComponent()` 方法来解码。

