
Note that all zlib APIs except those that are explicitly synchronous use libuv's
threadpool, which can have surprising and negative performance implications for
some applications, see the [`UV_THREADPOOL_SIZE`][] documentation for more
information.

