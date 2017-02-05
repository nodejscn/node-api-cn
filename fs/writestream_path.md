<!-- YAML
added: v0.1.93
-->

流正在写入的文件的路径，指定在 `fs.createWriteStream()` 的第一个参数。
如果 `path` 传入的是一个字符串，则 `writeStream.path` 是一个字符串。
如果 `path` 传入的是一个 `Buffer`，则 `writeStream.path` 是一个 `Buffer`。

