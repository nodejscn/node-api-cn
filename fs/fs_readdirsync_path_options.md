<!-- YAML
added: v0.1.21
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22020
    description: 添加新的选项 `withFileTypes`。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
  * `withFileTypes` {boolean} **默认值:** `false`。
* 返回: {string[]|Buffer[]|fs.Dirent[]}

同步的 readdir(3)。

可选的 `options` 参数可以是字符串（指定字符编码）、或具有 `encoding` 属性（指定用于返回的文件名的字符编码）的对象。 
如果 `encoding` 被设置为 `'buffer'`，则返回的文件名会作为 `Buffer` 对象传入。

如果 `options.withFileTypes` 被设置为 `true`，则结果会包含 [`fs.Dirent`] 对象。

