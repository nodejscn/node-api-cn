
注意，所有文件系统 API 中，除了 `fs.FSWatcher()` 和那些显式同步的方法之外，都使用了 libuv 的线程池，这对于某些应用程序可能会产生出乎意料问题和负面的性能影响，详见 [`UV_THREADPOOL_SIZE`] 文档。
