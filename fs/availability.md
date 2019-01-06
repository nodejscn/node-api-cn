
<!--type=misc-->

此特性取决于底层操作系统，提供了一种通知文件系统更改的方法。

* 在 Linux 系统上，使用 [`inotify(7)`]。
* 在 BSD 系统上，使用 [`kqueue(2)`]。
* 在 macOS 系统上，对文件使用 [`kqueue(2)`]，对目录使用 [`FSEvents`]。
* 在 SunOS 系统上（包括 Solaris 和 SmartOS），使用[事件端口][`event ports`]。
* 在 Windows 系统上，此特性取决于 [`ReadDirectoryChangesW`]。
* 在 Aix 系统上，此特性取决于 [`AHAFS`] 必须启动。

如果底层功能由于某些原因不可用，则 `fs.watch` 将无法运行。
例如，当使用虚拟化软件（如 Vagrant、Docker 等）时，在网络文件系统（NFS、SMB 等）或主文件系统上监视文件或目录可能是不可靠的，在某些情况下也是不可能的。

仍然可以使用 `fs.watchFile()`，因为它使用 stat 轮询 ，但这种方法较慢且不太可靠。

