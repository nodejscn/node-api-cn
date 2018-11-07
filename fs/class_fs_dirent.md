<!-- YAML
added: v10.10.0
-->

当调用 [`fs.readdir()`] 或 [`fs.readdirSync()`] 且 `withFileTypes` 选项设为 `true` 时，
返回的数组填充的是 `fs.Dirent` 对象而不是字符串或 `Buffer`。


