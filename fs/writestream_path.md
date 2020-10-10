<!-- YAML
added: v0.1.93
-->

流正在写入的文件的路径，由 [`fs.createWriteStream()`] 的第一个参数指定。 
如果 `path` 传入字符串，则 `writeStream.path` 将是字符串。 
如果 `path` 传入 `Buffer`，则 `writeStream.path` 将是 `Buffer`。

