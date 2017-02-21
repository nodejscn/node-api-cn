<!-- YAML
added: v0.1.25
-->

* `str` {String}

`querystring.escape()` 方法对给定的 `str` 执行 URL 百分号编码。

`querystring.escape()` 方法是供 `querystring.stringify()` 使用的，且通常不被直接使用。
它之所以对外开放，是为了在需要时可以通过给 `querystring.escape` 赋值一个函数来重写编码的实现。

