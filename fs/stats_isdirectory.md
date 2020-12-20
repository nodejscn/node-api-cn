<!-- YAML
added: v0.1.10
-->

* 返回: {boolean}

如果 `fs.Stats` 对象描述文件系统目录，则返回 `true`。

如果 `fs.Stats` 对象来自 [`fs.lstat()`]，则此方法会始终返回 `false`。
这是因为 [`fs.lstat()`] 返回关于符号链接本身（而不是其解析的路径）的信息。


