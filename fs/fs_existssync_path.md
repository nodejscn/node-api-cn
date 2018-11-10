<!-- YAML
added: v0.1.21
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* 返回: {boolean}

如果路径存在，则返回 `true`，否则返回 `false`。

详见异步版本的接口 [`fs.exists()`]。

虽然 `fs.exists()` 是废弃的，但 `fs.existsSync()` 不是废弃的。
`fs.exists()` 的回调函数接收的参数与其他 Node.js 回调不一致，`fs.existsSync()` 没有使用回调。

