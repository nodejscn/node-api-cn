
stat 对象中的时间有以下语义：

* `atime` "访问时间" - 文件数据最近被访问的时间。
  会被 mknod(2)、 utimes(2) 和 read(2) 系统调用改变。
* `mtime` "修改时间" - 文件数据最近被修改的时间。
  会被 mknod(2)、 utimes(2) 和 write(2) 系统调用改变。
* `ctime` "变化时间" - 文件状态最近更改的时间（修改索引节点数据）
  会被 chmod(2)、 chown(2)、 link(2)、 mknod(2)、 rename(2)、 unlink(2)、 utimes(2)、 read(2) 和 write(2) 系统调用改变。
* `birthtime` "创建时间" -  文件创建的时间。
  当文件被创建时设定一次。
  在创建时间不可用的文件系统中，该字段可能被替代为 `ctime` 或 `1970-01-01T00:00Z`（如 Unix 的纪元时间戳 `0`）。
  注意，该值在此情况下可能会大于 `atime` 或 `mtime`。
  在 Darwin 和其它的 FreeBSD 衍生系统中，如果 `atime` 被使用 utimes(2) 系统调用显式地设置为一个比当前 `birthtime` 更早的值，也会有这种情况。

在 Node.js v0.12 之前的版本中，`ctime` 在 Windows 系统中保存 `birthtime`。
注意，在 v0.12 中，`ctime` 不是“创建时间”，并且在 Unix 系统中，它从来都不是。

