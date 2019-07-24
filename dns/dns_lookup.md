在底层,`dns.lookup()`使用操作系统设施与大多数其他程序相同。例如，`dns.lookup()`几乎总是解析给定的主机名与`ping`命令一样。在许多类POSIX操作系统中，
`dns.lookup()`函数的行为可以通过改变`nsswitch.conf(5)`并且/或`resolv.conf(5)`设置进行改变，但是需要注意改变这些文件就意味着改变所有正在这个操作系统中运行
的所有进程的行为。

尽管以异步`JavaScript`的角度来调用`dns.lookup()`,但在内部`libuv`底层线程池中却是同步的调用`getaddrinfo(3)`。
This can have surprising negative performance
implications for some applications, see the [`UV_THREADPOOL_SIZE`][]
documentation for more information.

Note that various networking APIs will call `dns.lookup()` internally to resolve
host names. If that is an issue, consider resolving the hostname to and address
using `dns.resolve()` and using the address instead of a host name. Also, some
networking APIs (such as [`socket.connect()`][] and [`dgram.createSocket()`][])
allow the default resolver, `dns.lookup()`, to be replaced.