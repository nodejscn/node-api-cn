<!-- YAML
added: v0.1.31
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
* 返回: {string|Buffer}

同步的 readlink(2)。
返回符号链接的字符串值。

可选的 `options` 参数可以是指定编码的字符串，也可以是具有 `encoding` 属性的对象，该属性指定用于传递给回调的链接路径的字符编码。 
如果 `encoding` 设置为 `'buffer'`，则返回的链接路径将作为 `Buffer` 对象传入。


