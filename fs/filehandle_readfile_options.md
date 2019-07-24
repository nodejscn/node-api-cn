<!-- YAML
added: v10.0.0
-->
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `null`
  * `flag` {string} 参阅[支持的文件系统标志][support of file system `flags`]。**默认值:** `'r'`。
* 返回: {Promise}

异步地读取文件的全部内容。

`Promise` 被解决时会带上文件的内容。
如果没有指定字符编码（使用 `options.encoding`），则数据会以 `Buffer` 对象返回。
否则，数据将会是一个字符串。

如果 `options` 是字符串，则它指定字符编码。

当 `path` 是目录时，`fsPromises.readFile()` 的行为是特定于平台的。
在 macOS、Linux 和 Windows 上，promise 将会被拒绝并带上一个错误。
在 FreeBSD 上，则将会返回目录内容的表示。

`FileHandle` 必须支持读取。

如果对文件句柄进行了一次或多次 `filehandle.read()` 调用，然后再调用 `filehandle.readFile()`，则将从当前位置读取数据，直到文件结束。 
它并不总是从文件的开头读取。

