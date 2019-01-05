
`atimeMs`、`mtimeMs`、`ctimeMs` 以及 `birthtimeMs` 属性是是保存相应时间（以毫秒为单位）的[数字][MDN-Number]。
它们的精确度取决于平台。
`atime`、`mtime`、`ctime` 以及 `birthtime` 是对应时间的 [`Date`][MDN-Date] 对象。
`Date` 值和数字值没有关联性。
对数字值重新赋值、或者改变 `Date` 值，都不会影响到对应的属性。

stat 对象中的时间具有以下语义：

* `atime` "访问时间" - 上次访问文件数据的时间。由 mknod(2)、 utimes(2) 和 read(2) 系统调用更改。
* `mtime` "修改时间" - 上次修改文件数据的时间。由 mknod(2)、 utimes(2) 和 write(2) 系统调用更改。
* `ctime` "变化时间" - 上次更改文件状态的时间（修改索引节点数据）。由 chmod(2)、 chown(2)、 link(2)、 mknod(2)、 rename(2)、 unlink(2)、 utimes(2)、 read(2) 和 write(2) 系统调用更改。
* `birthtime` "创建时间" - 文件创建的时间。
  创建文件时设置一次。
  在不支持创建时间的文件系统上，该字段可能被替代为 `ctime` 或 `1970-01-01T00:00Z`（如 Unix 纪元时间戳 `0`）。
  在这种情况下，该值可能大于 `atime` 或 `mtime`。
  在 Darwin 和其他的 FreeBSD 衍生系统上，如果使用 utimes(2) 系统调用将 `atime` 显式地设置为比 `birthtime` 更早的值，也会有这种情况。

在 Node.js 0.12 之前，`ctime` 在 Windows 上保存 `birthtime`。
从 0.12 开始，`ctime` 不再是“创建时间”，而在 Unix 系统上则一直都不是。

