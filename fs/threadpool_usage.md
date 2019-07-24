
所有的文件系统 API，除了 `fs.FSWatcher()` 和那些显式同步的之外，都使用 libuv 的线程池，这对某些应用程序可能会产生意外和负面的性能影响。 
有关更多信息，参阅 [`UV_THREADPOOL_SIZE`] 文档。

