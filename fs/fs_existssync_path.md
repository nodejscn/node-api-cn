<!-- YAML
added: v0.1.21
-->

* `path` {String | Buffer}

[`fs.exists()`] 的同步版本。
如果文件存在，则返回 `true`，否则返回 `false`。

注意，虽然 `fs.exists()` 是废弃的，但 `fs.existsSync()` 不是。
（`fs.exists()` 的回调接收的参数与其他 Node.js 回调不一致，`fs.existsSync()` 不使用回调。）

