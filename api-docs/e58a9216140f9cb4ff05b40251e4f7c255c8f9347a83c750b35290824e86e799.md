<!-- YAML
added: v10.0.0
-->
* `atime` {number|string|Date}
* `mtime` {number|string|Date}
* 返回: {Promise}

更改 `FileHandle` 指向的对象的文件系统时间戳，然后在成功时解决 `Promise` 且不带参数。

此函数在 7.1 之前的 AIX 版本上不起作用，它将会解决 `Promise` 并带上使用 `UV_ENOSYS` 代码的错误。

