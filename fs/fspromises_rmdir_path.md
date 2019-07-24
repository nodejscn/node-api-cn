<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* 返回: {Promise}

删除 `path` 指定的目录，然后在成功时解决 `Promise` 且不带参数。

在文件（而不是目录）上使用 `fsPromises.rmdir()` 会导致 `Promise` 被拒绝，在 Windows 上会带上 `ENOENT` 错误，而在 POSIX 上则会带上 `ENOTDIR` 错误。

