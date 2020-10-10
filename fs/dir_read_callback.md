<!-- YAML
added: v12.12.0
-->

* `callback` {Function}
  * `err` {Error}
  * `dirent` {fs.Dirent|null}

通过 readdir(3) 异步地读取下一个目录项作为 [`fs.Dirent`]。

读取完成之后，则会调用 `callback`（传入 [`fs.Dirent`] 或 `null`（如果读取不到目录项））。

此函数返回的目录项不遵循操作系统的底层目录机制所提供的特定顺序。
遍历目录时添加或删除的目录项可能会或可能不会包含在遍历的结果中。

