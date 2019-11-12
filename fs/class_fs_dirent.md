<!-- YAML
added: v10.10.0
-->

目录项的表示形式，通过从 [`fs.Dir`] 中读取而返回。

此外，当使用 `withFileTypes` 选项设置为 `true` 调用 [`fs.readdir()`] 或 [`fs.readdirSync()`] 时，生成的数组将会填充 `fs.Dirent` 对象，而不是字符串或 `Buffer`。

