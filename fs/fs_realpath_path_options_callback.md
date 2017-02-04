<!-- YAML
added: v0.1.31
-->

* `path` {String | Buffer}
* `options` {String | Object}
  * `encoding` {String} 默认 = `'utf8'`
* `callback` {Function}

异步的 realpath(3)。
`callback` 有两个参数 `(err, resolvedPath)`。
可以使用 `process.cwd` 解析相对路径。

只支持可转换成 UTF8 字符串的路径。

可选的 `options` 参数用于传入回调的路径，它可以是一个字符串并指定一个字符编码，或是一个对象且由一个 `encoding` 属性指定使用的字符编码。
如果 `encoding` 设为 `'buffer'`，则返回的路径会被作为 `Buffer` 对象传入。

