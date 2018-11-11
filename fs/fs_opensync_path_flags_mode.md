<!-- YAML
added: v0.1.21
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `flags` {string|number} 详见[支持的文件系统标志][support of file system `flags`]。
* `mode` {integer} 默认为 `0o666`。
* 返回: {number}

返回表示文件描述符的整数。

详见异步版本的接口：[`fs.open()`]。

