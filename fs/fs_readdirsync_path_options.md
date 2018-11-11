<!-- YAML
added: v0.1.21
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22020
    description: New option `withFileTypes` was added.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
  * `encoding` {string} 默认为 `'utf8'`。
  * `withFileTypes` {boolean} 默认为 `false`。
* 返回: {string[]|Buffer[]|fs.Dirent[]}

同步的 readdir(3). 

`options` 参数用于返回的文件名。
它可以是一个字符串，指定字符编码。
也可以是一个对象，其中 `encoding` 属性指定字符编码。
如果 `encoding` 设为 `'buffer'`，则返回的文件名会是 `Buffer` 对象。

如果 `options.withFileTypes` 设为`true`，则返回包含 [`fs.Dirent`] 对象的数组。

