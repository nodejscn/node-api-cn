<!-- YAML
added: v0.1.93
-->

* {string|Buffer}

流正在读取的文件的路径，由 `fs.createReadStream()` 的第一个参数指定。 
如果 `path` 传入字符串，则 `readStream.path` 将是字符串。 
如果 `path` 传入 `Buffer`，则 `readStream.path` 将是 `Buffer`。

