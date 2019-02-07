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
  * `encoding` {string} **默认值:** `'utf8'`。
  * `withFileTypes` {boolean} **默认值:** `false`。
* 返回: {string[]|Buffer[]|fs.Dirent[]}

同步的 readdir(3)。

可选的 `options` 参数可以是指定编码的字符串，也可以是具有 `encoding` 属性的对象，该属性指定用于传给回调的文件名的字符编码。 
如果 `encoding` 设置为 `'buffer'`，则返回的文件名是 `Buffer` 对象。

如果 `options.withFileTypes` 设置为 `true`，则返回的结果将包含 [`fs.Dirent`] 对象。

