<!-- YAML
added: v0.1.92
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`.
-->

* `data` {string | Buffer | TypedArray | DataView}
* `inputEncoding` {string} `data` 字符串的[字符编码][encoding]。

使用给定的 `data` 更新哈希的内容，该数据的字符编码在 `inputEncoding` 中给出。
如果未提供 `encoding`，并且 `data` 是字符串，则强制执行 `'utf8'` 的编码。 
如果 `data` 是一个 [`Buffer`]、`TypedArray` 或 `DataView`，则 `inputEncoding` 会被忽略。

在流式传输时，可以使用新数据多次调用此方法。

