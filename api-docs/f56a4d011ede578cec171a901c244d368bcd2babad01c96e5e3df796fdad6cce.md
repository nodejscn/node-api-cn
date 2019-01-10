
这些功能实现与dns.lookup()截然不同。它们不仅没有使用`getaddrinfo(3)`并且通过网络执行DNS查询。使用异步网络通信，并且没有使用libuv线程池。

因此,这些函数不会像使用libuv线程池的`dns.lookup()`函数一样会对其它进程有负面影响。

它们不像`dns.lookup()`一样使用相同的配置文件。例如，它们不会使用来自`/etc/hosts`配置。
