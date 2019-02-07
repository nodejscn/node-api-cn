<!-- YAML
added: v0.1.29
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: The `data` parameter can now be any `TypedArray` or a
                 `DataView`.
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: The `data` parameter can now be a `Uint8Array`.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `file` parameter can be a file descriptor now.
-->

* `file` {string|Buffer|URL|integer} 文件名或文件描述符。
* `data` {string|Buffer|TypedArray|DataView}
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `'utf8'`。
  * `mode` {integer} **默认值:** `0o666`。
  * `flag` {string} 参阅[支持的文件系统标志][support of file system `flags`]。**默认值:** `'w'`。

返回 `undefined`。

有关详细信息，参阅此 API 的异步版本的文档：[`fs.writeFile()`]。

