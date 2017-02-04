<!-- YAML
added: v0.1.8
-->

* `file` {String | Buffer | Integer} 文件名或文件描述符
* `options` {Object | String}
  * `encoding` {String | Null} 默认 = `null`
  * `flag` {String} 默认 = `'r'`

[`fs.readFile`] 的同步版本。
返回 `file` 的内容。

如果指定了 `encoding` 选项，则该函数返回一个字符串，否则返回一个 buffer。

