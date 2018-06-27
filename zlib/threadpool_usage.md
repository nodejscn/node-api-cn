
Note that all zlib APIs except those that are explicitly synchronous use libuv's
threadpool. This can lead to surprising effects in some applications, such as
subpar performance (which can be mitigated by adjusting the [pool size][])
and/or unrecoverable and catastrophic memory fragmentation.

