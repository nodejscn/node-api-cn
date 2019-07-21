<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL|FileHandle} 文件名或 `FileHandle`。
* `data` {string|Buffer}
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `'utf8'`。
  * `mode` {integer} **默认值:** `0o666`。
  * `flag` {string} 参阅[支持的文件系统标志][support of file system `flags`]。默认值: `'a'`。
* 返回: {Promise}

异步地将数据追加到文件，如果文件尚不存在则创建该文件。 
`data` 可以是字符串或 [`Buffer`]。
`Promise` 将会在成功时解决，且不带参数。

如果 `options` 是字符串，则它指定字符编码。

`path` 可以指定为已打开用于追加（使用 `fsPromises.open()`）的 `FileHandle`。

