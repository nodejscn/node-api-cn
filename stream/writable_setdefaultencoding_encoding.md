<!-- YAML
added: v0.11.15
changes:
  - version: v6.1.0
    pr-url: https://github.com/nodejs/node/pull/5040
    description: This method now returns a reference to `writable`.
-->

* `encoding` {string} 新的默认字符编码。
* 返回: {this}

`writable.setDefaultEncoding()` 方法能为[可写流]设置默认的 `encoding`。

