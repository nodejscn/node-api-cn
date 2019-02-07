
`atimeMs`、`mtimeMs`、`ctimeMs` 和 `birthtimeMs` 属性是保存相应时间（以毫秒为单位）的[数值][MDN-Number]。
它们的精度取决于平台。
`atime`、`mtime`、`ctime` 和 `birthtime` 是对应时间的 [`Date`][MDN-Date] 对象。
`Date` 值和数值没有关联性。
赋值新的数值、或者改变 `Date` 值，都不会影响到对应的属性。

stat 对象中的时间具有以下语义：

* `atime` "访问时间" - 上次访问文件数据的时间。由 mknod(2)、 utimes(2) 和 read(2) 系统调用更改。
* `mtime` "修改时间" - 上次修改文件数据的时间。由 mknod(2)、 utimes(2) 和 write(2) 系统调用更改。
* `ctime` "更改时间" - 上次更改文件状态（修改索引节点数据）的时间。由 chmod(2)、 chown(2)、 link(2)、 mknod(2)、 rename(2)、 unlink(2)、 utimes(2)、 read(2) 和 write(2) 系统调用更改。
* `birthtime` "创建时间" - 创建文件的时间。当创建文件时设置一次。
  在不支持创建时间的文件系统上，该字段可能改为保存 `ctime` 或 `1970-01-01T00:00Z`（即 Unix 纪元时间戳 `0`）。
  在这种情况下，该值可能大于 `atime` 或 `mtime`。
  在 Darwin 和其他的 FreeBSD 衍生系统上，也可能使用 utimes(2) 系统调用将 `atime` 显式地设置为比 `birthtime` 更早的值。

在 Node.js 0.12 之前，`ctime` 在 Windows 上保存 `birthtime`。
从 0.12 开始，`ctime` 不再是“创建时间”，而在 Unix 系统上则从来都不是。

