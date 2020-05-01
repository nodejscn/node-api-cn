<!-- YAML
added: v10.10.0
-->

目录项（可以是文件或目录中的子目录）的表示，通过读取 [`fs.Dir`] 返回。
目录项是文件名和文件类型对的组合。

此外，当调用 [`fs.readdir()`] 或 [`fs.readdirSync()`]（`withFileTypes` 选项设置为 `true`）时，则生成的数组会使用 `fs.Dirent` 对象（而不是字符串或 `Buffer`）填充。

