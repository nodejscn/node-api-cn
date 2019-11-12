<!-- YAML
added: v12.12.0
-->

* 返回: {Promise} 包含 {fs.Dirent|null}。

通过 readdir(3) 异步地读取下一个目录项作为 [`fs.Dirent`]。

读取完成之后，将会返回一个 `Promise`，它被解决时将会返回 [`fs.Dirent`] 或 `null`（如果没有更多的目录项要读取）。

此函数返回的目录项不遵循操作系统的底层目录机制所提供的特定顺序。

