<!-- YAML
added: v10.0.0
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31030
    description: 参数 `data` 不再强制转换不支持的输入为字符串。
-->

* `file` {string|Buffer|URL|FileHandle} 文件名或 `FileHandle`。
* `data` {string|Buffer|Uint8Array}
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `'utf8'`。
  * `mode` {integer} **默认值:** `0o666`。
  * `flag` {string} 参见[文件系统 `flag` 的支持][support of file system `flags`]。默认值: `'w'`。
* 返回: {Promise}

异步地将数据写入到一个文件，如果文件已存在则覆盖该文件。 
`data` 可以是字符串或 buffer。 
`Promise` 将会在成功时解决，且不带参数。

如果 `data` 是 buffer，则 `encoding` 选项会被忽略。

如果 `options` 是字符串，则它指定字符编码。

指定的 `FileHandle` 必须支持写入。

在同一个文件上多次使用 `fsPromises.writeFile()` 且不等待 `Promise` 被解决（或被拒绝）是不安全的。

