<!-- YAML
added: v5.10.0
-->

* `prefix` {string}
* `options` {string|Object}
  * `encoding` {string} 默认 = `'utf8'`

[`fs.mkdtemp()`] 的同步版本。
返回创建的目录的路径。

可选的 `options` 参数可以是一个字符串并指定一个字符编码，或是一个对象且由一个 `encoding` 属性指定使用的字符编码。

