在底层,`dns.lookup()`使用操作系统设施与大多数其他程序相同。例如，`dns.lookup()`几乎总是解析给定的主机名与`ping`命令一样。在许多类POSIX操作系统中，
`dns.lookup()`函数的行为可以通过改变`nsswitch.conf(5)`并且/或`resolv.conf(5)`设置进行改变，但是需要注意改变这些文件就意味着改变所有正在这个操作系统中运行
的所有进程的行为。

尽管以异步`JavaScript`的角度来调用`dns.lookup()`,但在内部`libuv`底层线程池中却是同步的调用`getaddrinfo(3)`。因为`libuv`线程池有固定大小，它意味着,如果出于某种原因调用`getaddrinfo(3)`需要很长时间,其他操作可以运行在libuv线程池中(如文件系统操作)就会存在性能问题。为了缓解这个问题,一个可能的解决办法是增加libuv的线程池大小通过设置`'UV_THREADPOOL_SIZE'`环境变量值大于`4`(当前的默认值).更多libuv线程池信息，请查看：[here](http://docs.libuv.org/en/latest/threadpool.html)
