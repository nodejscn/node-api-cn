
<!--type=misc-->

该特性依赖于底层操作系统提供的一种方法来通知文件系统的变化。

* 在 Linux 系统中，使用 [`inotify`]。
* 在 BSD 系统中，使用 [`kqueue`]。
* 在 macOS 系统中，对文件使用 [`kqueue`]，对目录使用 [`FSEvents`]。
* 在 SunOS 系统（包括 Solaris 和 SmartOS）中，使用 [`event ports`]。
* 在 Windows 系统中，该特性依赖 [`ReadDirectoryChangesW`]。
* 在 Aix 系统中，该特性依赖 [`AHAFS`] 必须是启动的。

如果底层功能因某些原因不可用，则 `fs.watch` 也无法正常工作。
例如，当使用虚拟化软件如 Vagrant、Docker 等时，在网络文件系统（NFS、SMB 等）或主文件系统中监视文件或目录可能是不可靠的。

It is still possible to use `fs.watchFile()`, which uses stat polling, but
this method is slower and less reliable.

