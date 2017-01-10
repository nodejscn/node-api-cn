<!-- YAML
added: v0.8.6
-->

* `path` {String | Buffer}
* `len` {Integer} default = `0`
* `callback` {Function}

Asynchronous truncate(2). No arguments other than a possible exception are
given to the completion callback. A file descriptor can also be passed as the
first argument. In this case, `fs.ftruncate()` is called.

