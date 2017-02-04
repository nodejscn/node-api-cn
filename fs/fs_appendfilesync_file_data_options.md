<!-- YAML
added: v0.6.7
-->

* `file` {String | Buffer | Number} 文件名或文件描述符
* `data` {String | Buffer}
* `options` {Object | String}
  * `encoding` {String | Null} 默认 = `'utf8'`
  * `mode` {Integer} 默认 = `0o666`
  * `flag` {String} 默认 = `'a'`

[`fs.appendFile()`] 的同步版本。
返回 `undefined`。

