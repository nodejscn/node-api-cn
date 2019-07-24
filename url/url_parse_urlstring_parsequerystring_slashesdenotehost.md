<!-- YAML
added: v0.1.25
changes:
  - version: v9.0.0
    pr-url: https://github.com/nodejs/node/pull/13606
    description: The `search` property on the returned URL object is now `null`
                 when no query string is present.
-->

* `urlString` {string} 要解析的 URL 字符串。
* `parseQueryString` {boolean} 如果设为 `true`，则返回的 URL 对象的 `query` 属性会是一个使用 [`querystring`] 模块的 `parse()` 生成的对象。
  如果设为 `false`，则 `query` 会是一个未解析未解码的字符串。
  默认为 `false`。
* `slashesDenoteHost` {boolean} 如果设为 `true`，则 `//` 之后至下一个 `/` 之前的字符串会解析作为 `host`。
  例如，`//foo/bar` 会解析为 `{host: 'foo', pathname: '/bar'}` 而不是 `{pathname: '//foo/bar'}`。
  默认为 `false`。

解析 URL 字符串并返回 URL 对象。

如果 `urlString` 不是字符串，则抛出`TypeError`。

如果 `auth` 属性存在但无法解码，则抛出 `URIError`。

