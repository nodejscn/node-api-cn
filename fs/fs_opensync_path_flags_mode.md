<!-- YAML
added: v0.1.21
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `flags` {string|number} 请参阅[文件系统标志的支持][support of file system `flags`]。
* `mode` {integer} 默认为 `0o666`。
* 返回: {number}

返回文件描述符。

详见异步的方法 [`fs.open()`]。

