<!-- YAML
added: v5.10.0
-->

* `prefix` {string}
* `options` {string|Object}
  * `encoding` {string} 默认为 `'utf8'`。
* 返回: {string}

返回创建的目录路径。

详见异步版本的接口：[`fs.mkdtemp()`]。


`options` 参数可以是一个字符串，指定字符编码。
也可以是一个对象，其中 `encoding` 属性指定字符编码。

