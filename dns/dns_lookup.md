
在底层，[`dns.lookup()`] 使用的操作系统设施与大多数其他程序相同。
例如，[`dns.lookup()`] 几乎总是解析给定的主机名，与 `ping` 命令一样。
在大多数类 POSIX 操作系统中，[`dns.lookup()`] 函数的行为可以通过改变 nsswitch.conf(5) 和/或 resolv.conf(5) 的设置进行改变，但是需要注意改变这些文件就意味着改变所有正在这个操作系统中运行的所有程序的行为。

尽管以异步 JavaScript 的角度来调用 `dns.lookup()`，但在内部 libuv 底层线程池中却是同步的调用 `getaddrinfo(3)`。
这可能会对某些应用程序产生令人惊讶的负面性能影响，有关详细信息，请参阅 [`UV_THREADPOOL_SIZE`] 文档。

各种网络 API 将会在内部调用 `dns.lookup()` 来解析主机名。 
如果这是一个问题，请考虑使用 `dns.resolve()` 并使用地址而不是主机名来将主机名解析为地址。 
此外，某些网络 API（例如 [`socket.connect()`] 和 [`dgram.createSocket()`] 允许替换默认解析器 `dns.lookup()`。

