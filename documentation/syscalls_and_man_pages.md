
系统调用定义了用户程序和底层操作系统之间的接口，例如 [open(2)](http://man7.org/linux/man-pages/man2/open.2.html)、[read(2)](http://man7.org/linux/man-pages/man2/read.2.html)。
Node 函数只是简单地包装了系统调用，例如 `fs.open()`。
与之对应的帮助文档描述了系统调用的工作方式。

**警告：**有些系统调用是 BSD 系统特有的，例如 [lchown(2)](http://man7.org/linux/man-pages/man2/lchown.2.html)。
这意味着 `fs.chown()` 只适用于 Mac OS X 和其他的 BSD 衍生系统，在 Linux 上不可用。

大部分 Unix 的系统调用都有对应的 Windows 版本，但 Windows 版本运行起来可能与 Linux 和 OS X 的有些差异。
有些 Unix 系统调用无法在 Windows 中找到对应的操作语义，详见[议题4760](https://github.com/nodejs/node/issues/4760)。

