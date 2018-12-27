<!-- YAML
added: v0.1.8
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22020
    description: New option `withFileTypes` was added.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5616
    description: The `options` parameter was added.
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} 默认为 `'utf8'`。
  * `withFileTypes` {boolean} 默认为 `false`。
* `callback` {Function}
  * `err` {Error}
  * `files` {string[]|Buffer[]|fs.Dirent[]}

异步的 readdir(3)。
读取目录的内容。
`callback` 有两个参数 `(err, files)`，其中 `files` 是目录中的文件名的数组。

如果 `options` 是一个字符串，则指定字符编码。
如果 `encoding` 设为 `'buffer'`，则返回的文件名是 `Buffer`。

如果 `withFileTypes` 设为 `true`，则 `files` 数组中的元素是 [`fs.Dirent`]。

