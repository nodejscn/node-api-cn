<!-- YAML
added: v0.1.31
-->

* `path` {String | Buffer}
* `options` {String | Object}
  * `encoding` {String} 默认 = `'utf8'`
* `callback` {Function}

异步的 readlink(2)。
回调有两个参数  `(err, linkString)`。

可选的 `options` 参数用于传入回调的链接路径，它可以是一个字符串并指定一个字符编码，或是一个对象且由一个 `encoding` 属性指定使用的字符编码。
如果 `encoding` 设为 `'buffer'`，则返回的链接路径会被作为 `Buffer` 对象传入。

