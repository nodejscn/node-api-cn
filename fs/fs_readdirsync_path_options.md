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
* `options` {string|Object}
  * `encoding` {string} 默认为 `'utf8'`。
  * `withFileTypes` {boolean} 默认为 `false`。
* 返回: {string[]|Buffer[]|fs.Dirent[]}

同步的 readdir(3)。读取目录的内容。

如果 `options` 是一个字符串，则指定字符编码。
如果 `encoding` 设为 `'buffer'`，则返回的文件名是 `Buffer`。

如果 `withFileTypes` 设为 `true`，则 `files` 数组中的元素是 [`fs.Dirent`]。

