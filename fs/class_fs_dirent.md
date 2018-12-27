<!-- YAML
added: v10.10.0
-->

当调用 [`fs.readdir()`] 或 [`fs.readdirSync()`] 且 `withFileTypes` 设为 `true` 时，
返回的数组会填充 `fs.Dirent` 而不是字符串或 `Buffer`。


