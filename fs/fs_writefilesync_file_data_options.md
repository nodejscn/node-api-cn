<!-- YAML
added: v0.1.29
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: The `data` parameter can now be any `TypedArray` or a
                 `DataView`.
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: 参数 `data` 现在可以是一个 `Uint8Array`。
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: 参数 `file` 现在可以是一个文件描述符。
-->

* `file` {string|Buffer|URL|integer} 文件名或文件描述符。
* `data` {string|Buffer|TypedArray|DataView}
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `'utf8'`。
  * `mode` {integer} 默认为 `0o666`。
  * `flag` {string} 详见[支持的文件系统标志][support of file system `flags`]。默认为 `'w'`。

返回 `undefined`。

详见异步版本的接口：[`fs.writeFile()`]。

