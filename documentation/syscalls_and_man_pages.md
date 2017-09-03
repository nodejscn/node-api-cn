
系统调用定义了用户程序和底层操作系统之间的接口，例如 open(2)、 read(2)。
Node 函数只是简单地封装了系统调用，例如 `fs.open()`。
相应的帮助文档会描述系统调用是如何工作的。

有些系统调用是 BSD 系统特有的，例如 lchown(2)。
这意味着 `fs.lchown()` 只适用于 macOS 和其他 BSD 衍生系统，在 Linux 上不可用。

大部分 Unix 系统调用都有对应的 Windows 版本，但 Windows 版本运行起来可能与 Linux 和 macOS 的有些差异。
有些 Unix 系统调用无法在 Windows 中找到对应的操作语义，详见[议题4760]。

