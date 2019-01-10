<!-- YAML
added: v10.10.0
-->

当在 `withFileTypes` 选项设置为 `true` 的情况下调用 [`fs.readdir()`] 或 [`fs.readdirSync()`] 时，生成的数组将填充 `fs.Dirent` 对象，而不是字符串或 `Buffer`。

