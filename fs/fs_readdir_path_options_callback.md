<!-- YAML
added: v0.1.8
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22020
    description: 添加新的选项 `withFileTypes`。
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5616
    description: 添加 `options` 参数。
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
  * `withFileTypes` {boolean} **默认值:** `false`。
* `callback` {Function}
  * `err` {Error}
  * `files` {string[]|Buffer[]|fs.Dirent[]}

异步的 readdir(3)。
读取目录的内容。
回调有两个参数 `(err, files)`，其中 `files` 是目录中文件的名称的数组（不包括 `'.'` 和 `'..'`）。

可选的 `options` 参数可以是字符串（指定字符编码）、或具有 `encoding` 属性（指定用于传给回调的文件名的字符编码）的对象。 
如果 `encoding` 被设置为 `'buffer'`，则返回的文件名会作为 `Buffer` 对象传入。

如果 `options.withFileTypes` 被设置为 `true`，则 `files` 数组会包含 [`fs.Dirent`] 对象。

