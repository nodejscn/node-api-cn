<!-- YAML
added: v0.8.6
-->

* `path` {String | Buffer}
* `len` {Integer} default = `0`

Synchronous truncate(2). Returns `undefined`. A file descriptor can also be
passed as the first argument. In this case, `fs.ftruncateSync()` is called.

