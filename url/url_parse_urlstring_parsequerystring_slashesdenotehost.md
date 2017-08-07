<!-- YAML
added: v0.1.25
-->

* `urlString` {string} 要解析的 URL 字符串。
* `parseQueryString` {boolean} 如果为 `true`，则 `query` 属性总会通过 [`querystring`] 模块的 `parse()` 方法生成一个对象。
  如果为 `false`，则返回的 URL 对象上的 `query` 属性会是一个未解析、未解码的字符串。
  默认为 `false`。
* `slashesDenoteHost` {boolean} 如果为 `true`，则 `//` 之后至下一个 `/` 之前的字符串会被解析作为 `host`。
  例如，`//foo/bar` 会被解析为 `{host: 'foo', pathname: '/bar'}` 而不是 `{pathname: '//foo/bar'}`。
  默认为 `false`。

`url.parse()` 方法会解析一个 URL 字符串并返回一个 URL 对象。

如果`urlString`不是字符串将会抛出`TypeError`。

如果`auth`属性存在但无法编码则抛出`URIError`。

