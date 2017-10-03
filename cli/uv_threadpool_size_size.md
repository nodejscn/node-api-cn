
Set the number of threads used in libuv's threadpool to `size` threads.

Asynchronous system APIs are used by Node.js whenever possible, but where they
do not exist, libuv's threadpool is used to create asynchronous node APIs based
on synchronous system APIs. Node.js APIs that use the threadpool are:

- all `fs` APIs, other than the file watcher APIs and those that are explicitly
  synchronous
- `crypto.pbkdf2()`
- `crypto.randomBytes()`, unless it is used without a callback
- `crypto.randomFill()`
- `dns.lookup()`
- all `zlib` APIs, other than those that are explicitly synchronous

Because libuv's threadpool has a fixed size, it means that if for whatever
reason any of these APIs takes a long time, other (seemingly unrelated) APIs
that run in libuv's threadpool will experience degraded performance. In order to
mitigate this issue, one potential solution is to increase the size of libuv's
threadpool by setting the `'UV_THREADPOOL_SIZE'` environment variable to a value
greater than `4` (its current default value).  For more information, see the
[libuv threadpool documentation][].

[`--openssl-config`]: #cli_openssl_config_file
[Buffer]: buffer.html#buffer_buffer
[Chrome Debugging Protocol]: https://chromedevtools.github.io/debugger-protocol-viewer
[REPL]: repl.html
[SlowBuffer]: buffer.html#buffer_class_slowbuffer
[debugger]: debugger.html
[emit_warning]: process.html#process_process_emitwarning_warning_type_code_ctor
[libuv threadpool documentation]: http://docs.libuv.org/en/latest/threadpool.html
