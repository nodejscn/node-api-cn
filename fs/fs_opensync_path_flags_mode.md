<!-- YAML
added: v0.1.21
changes:
  - version: v11.1.0
    pr-url: https://github.com/nodejs/node/pull/23767
    description: 参数 `flags` 是可选的，并且默认为 `'r'`。
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/18801
    description: 支持 `as` 和 `as+` 标志。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `path` {string|Buffer|URL}
* `flags` {string|number} **默认值:** `'r'`。参见[文件系统 `flag` 的支持][support of file system `flags`]。
* `mode` {string|integer} **默认值:** `0o666`。
* 返回: {number}

返回表示文件描述符的整数。

详见此 API 的异步版本的文档：[`fs.open()`]。

