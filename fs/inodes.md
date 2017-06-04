
<!--type=misc-->

在 Linux 或 macOS 系统中，`fs.watch()` 解析路径到一个[索引节点]，并监视该索引节点。
如果监视的路径被删除或重建，则它会被分配一个新的索引节点。
监视器会发出一个删除事件，但会继续监视**原始的**索引节点。
新建的索引节点的事件不会被触发。
这是正常的行为。

In AIX, save and close of a file being watched causes two notifications -
one for adding new content, and one for truncation. Moreover, save and
close operations on some platforms cause inode changes that force watch
operations to become invalid and ineffective. AIX retains inode for the
lifetime of a file, that way though this is different from Linux / macOS,
this improves the usability of file watching. This is expected behavior.

