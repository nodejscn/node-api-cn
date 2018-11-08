<!-- YAML
added: v0.1.93
-->

* {string|Buffer}

流正在读取的文件的路径，由 `fs.createReadStream()` 的第一个参数指定。
如果 `path` 传入的是字符串，则 `readStream.path` 是一个字符串。
如果 `path` 传入的是 `Buffer`，则 `readStream.path` 是一个 `Buffer`。

