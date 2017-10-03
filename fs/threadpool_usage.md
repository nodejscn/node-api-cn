
Note that all file system APIs except `fs.FSWatcher()` and those that are
explicitly synchronous use libuv's threadpool, which can have surprising and
negative performance implications for some applications, see the
[`UV_THREADPOOL_SIZE`][] documentation for more information.

