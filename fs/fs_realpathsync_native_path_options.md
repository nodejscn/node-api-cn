<!-- YAML
added: v9.2.0
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} 默认为 `'utf8'`。
* Returns: {string|Buffer}

同步的 realpath(3)。

只支持可转换成 UTF8 字符串的路径。

`options` 参数用于传入回调的路径，它可以是一个字符串并指定一个字符编码，或是一个对象且由一个 `encoding` 属性指定使用的字符编码。
如果 `encoding` 设为 `'buffer'`，则返回的路径会被作为 `Buffer` 对象传入。


