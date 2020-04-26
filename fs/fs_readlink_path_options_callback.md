<!-- YAML
added: v0.1.31
changes:
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
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
* `callback` {Function}
  * `err` {Error}
  * `linkString` {string|Buffer}

异步的 readlink(2)。
回调会传入两个参数 `(err, linkString)`。

可选的 `options` 参数可以是指定编码的字符串，也可以是具有 `encoding` 属性的对象，该属性指定用于传递给回调的链接路径的字符编码。 
如果 `encoding` 设置为 `'buffer'`，则返回的链接路径将作为 `Buffer` 对象传入。

